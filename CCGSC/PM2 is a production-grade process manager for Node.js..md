


# PM2 and the things it touches (and the things that touch it)

PM2 is a production-grade **process manager** for Node.js. It keeps your apps alive, scales them across CPU cores, rolls them without downtime, manages logs, and bootstraps on OS startup. Think of it as the steady hands underneath your Node servers while NGINX or a load balancer plays maître d’.

PM2 Runtime (the OSS CLI/daemon) is free. There’s also a paid SaaS—**PM2 Plus/Enterprise**—for hosted monitoring and alerting; the runtime stays open-source. ([pm2.keymetrics.io](https://pm2.keymetrics.io/?utm_source=chatgpt.com "PM2 - Home"), [pm2.io](https://pm2.io/pricing?utm_source=chatgpt.com "Pricing"))

Below is a comprehensive, practitioner-friendly deep dive you can drop straight into CCGSC and any serious Node stack.

---

## 1) Core definitions & concepts

**What PM2 is:** a daemon + CLI that starts, restarts, scales, and monitors processes and their logs. Install with `npm i -g pm2`, then `pm2 start app.js`. ([pm2.keymetrics.io](https://pm2.keymetrics.io/docs/usage/pm2-doc-single-page/?utm_source=chatgpt.com "Single Page Doc - PM2"))

**Fork vs Cluster mode**

- **Fork:** one Node process per app. Simple, great for CPU-light tasks.
    
- **Cluster:** PM2 spins **N workers** (e.g., `instances: "max"`) using Node’s `cluster` module to share one port and use all CPU cores—no app code changes needed. For network servers this boosts throughput and resilience. ([pm2.keymetrics.io](https://pm2.keymetrics.io/docs/usage/cluster-mode/?utm_source=chatgpt.com "Cluster Mode - PM2"))
    

**Ecosystem file:** a JS/CJS file (`ecosystem.config.cjs|js`) that declares _what_ to run and _how_ (env vars, logs, instances, exec_mode, cwd, args). You can define multiple apps and multiple env sets (`env_production`, `env_development`) then `pm2 start ... --env production`. ([pm2.io](https://pm2.io/docs/runtime/reference/ecosystem-file/?utm_source=chatgpt.com "Ecosystem File | Reference | PM2 Documentation"), [pm2.keymetrics.io](https://pm2.keymetrics.io/docs/usage/application-declaration/?utm_source=chatgpt.com "Ecosystem File"))

**Environment handling:** PM2 merges shell env → ecosystem `env` → env override for selected profile; `pm2 restart --update-env` applies changes. ([pm2.keymetrics.io](https://pm2.keymetrics.io/docs/usage/environment/?utm_source=chatgpt.com "Environment Variables"), [pm2.io](https://pm2.io/docs/runtime/best-practices/environment-variables/?utm_source=chatgpt.com "Environment Variables | Best Practices | PM2 Documentation"), [Stack Overflow](https://stackoverflow.com/questions/33656947/passing-environment-variables-to-node-js-using-pm2?utm_source=chatgpt.com "Passing environment variables to node.js using pm2"))

**Sticky sessions:** WebSockets/long-polling often need client affinity to a single worker. You can enforce sticky sessions via PM2/Socket.IO strategies documented by Socket.IO (e.g., WebSocket-only, `@socket.io/pm2`, or LB-level stickiness). ([Socket.IO](https://socket.io/docs/v4/pm2/?utm_source=chatgpt.com "Usage with PM2"))

**Startup on boot:** `pm2 startup` (detects systemd/upstart/launchd/etc.), `pm2 save` to persist the current process list for restarts. ([pm2.keymetrics.io](https://pm2.keymetrics.io/docs/usage/startup/?utm_source=chatgpt.com "Startup Script"), [pm2.io](https://pm2.io/docs/runtime/guide/startup-hook/?utm_source=chatgpt.com "Startup Hook | Guide | PM2 Documentation"))

---

## 2) Reference architectures (how PM2 fits)

### A) Classic web service (your CCGSC coordinator)

```
[Clients]──TLS/HTTP(S)/WS──>[NGINX reverse proxy]
                                │
                                ▼
                        [PM2 cluster manager]
                           ├─ node worker #1  ┐
                           ├─ node worker #2  ├─ share one port (e.g., 127.0.0.1:8080)
                           └─ node worker #N  ┘
```

- **Flow:** NGINX terminates TLS, handles gzip, caching, static files, and proxies `/ws` to `127.0.0.1:8080` where PM2’s cluster listens.
    
- **Why PM2:** zero-downtime reloads, crash restarts, CPU scaling.
    
- **When WS is involved:** enable sticky sessions (via NGINX or Socket.IO’s PM2 integration). ([Socket.IO](https://socket.io/docs/v4/pm2/?utm_source=chatgpt.com "Usage with PM2"))
    

### B) API + worker duo

```
[Clients] → [NGINX] → [PM2 app: api-server (cluster)]
                   → [PM2 app: job-worker (fork N times)]
```

- Separate HTTP path from CPU-intensive jobs (queue worker). Use `exec_mode: fork` and `instances: N` for workers. PM2 supervises both.
    

### C) Bare-metal vs Container

- **Bare-metal/VM:** PM2 + systemd startup hook; NGINX on host.
    
- **Docker:** Either run your Node directly as PID 1 (let K8s/Compose manage it) **or** run PM2 **inside** the container to multiplex multiple workers in a single container. The latter is handy in single-container PaaS, but in “true” orchestration, let the orchestration layer manage scaling and health.
    

---

## 3) Data flow & control flow (what actually happens)

**Data flow (HTTP/WS):**  
Clients → NGINX (TLS, gzip, cache, rate limit) → PM2 master → one worker (round-robin) → your app handler → DB/cache → response. With sticky on WS, the same worker keeps the socket.

**Control flow (lifecycle):**

- **start:** `pm2 start ecosystem.config.cjs` → master forks workers → “online”.
    
- **reload:** `pm2 reload <name>` spins up new workers, drains old, zero downtime.
    
- **restart:** full bounce; clients reconnect.
    
- **autoscale:** change `instances` or `pm2 scale`.
    
- **crash:** PM2 restarts the crashed process.
    
- **boot:** systemd/launchd runs `pm2 resurrect` from the saved dump. ([pm2.keymetrics.io](https://pm2.keymetrics.io/docs/usage/startup/?utm_source=chatgpt.com "Startup Script"))
    

---

## 4) Technical innards & options you’ll actually use

**Logging**

- `output`, `error` → file paths; consider PM2’s `logrotate` module to rotate/compress.
    
- `merge_logs` when clustering to aggregate per app.
    

**Health & memory**

- `max_memory_restart: "1G"` restarts on leak.
    
- `kill_timeout`, `listen_timeout` control graceful shutdown/boot thresholds.
    

**Node flags**

- `node_args: ["--max-old-space-size=4096","--enable-source-maps"]` when needed.
    

**Environment**

- `env`, `env_production`, `--env production`, `--update-env` refresh live. ([pm2.keymetrics.io](https://pm2.keymetrics.io/docs/usage/environment/?utm_source=chatgpt.com "Environment Variables"), [pm2.io](https://pm2.io/docs/runtime/best-practices/environment-variables/?utm_source=chatgpt.com "Environment Variables | Best Practices | PM2 Documentation"))
    

**Startup**

- `pm2 startup` then `pm2 save`. PM2 detects your init system (systemd, launchd, etc.). ([pm2.keymetrics.io](https://pm2.keymetrics.io/docs/usage/startup/?utm_source=chatgpt.com "Startup Script"))
    

**Monitoring**

- `pm2 monit` (terminal UI).
    
- **PM2 Plus/Enterprise**: browser dashboard, metrics, triggers/alerts, distributed view. ([pm2.io](https://pm2.io/docs/plus/overview/?utm_source=chatgpt.com "Overview | PM2 Plus Documentation"))
    

---

## 5) Code & config snippets you can paste

**Minimal ecosystem (production, single app):**

```js
// ecosystem.config.cjs
module.exports = {
  apps: [{
    name: "coordinator",
    script: "coordinator_server.js",
    exec_mode: "cluster",        // multi-core without code change
    instances: "max",            // use all CPUs
    env_production: { NODE_ENV: "production" },
    env_development: { NODE_ENV: "development" },
    output: "/var/log/coordinator/out.log",
    error:  "/var/log/coordinator/error.log",
    max_memory_restart: "1G",
    time: true
  }]
};
```

Switch env: `pm2 start ecosystem.config.cjs --env production` ([pm2.keymetrics.io](https://pm2.keymetrics.io/docs/usage/application-declaration/?utm_source=chatgpt.com "Ecosystem File"))

**Boot persistence:**

```bash
pm2 startup
pm2 start ecosystem.config.cjs --env production
pm2 save
```

([pm2.keymetrics.io](https://pm2.keymetrics.io/docs/usage/startup/?utm_source=chatgpt.com "Startup Script"))

**Environment updates:**

```bash
# edit env in ecosystem; then
pm2 restart coordinator --update-env
```

([pm2.io](https://pm2.io/docs/runtime/best-practices/environment-variables/?utm_source=chatgpt.com "Environment Variables | Best Practices | PM2 Documentation"))

**Sticky sessions with Socket.IO (where needed):** follow Socket.IO’s PM2 guidance—choose WebSocket-only, use the PM2 adapter package, or set stickiness at the load balancer (NGINX). ([Socket.IO](https://socket.io/docs/v4/pm2/?utm_source=chatgpt.com "Usage with PM2"))

---

## 6) Security, privacy, and compliance hygiene

- **Least privilege:** run as unprivileged user (e.g., `www-data`), restrict file perms on `/var/log/coordinator/*`.
    
- **Secrets handling:** prefer env injection from a secrets manager (not hard-coded in ecosystem files or logs).
    
- **Log redaction:** avoid logging PII; adopt structured logs (JSON) + rotation/retention policy.
    
- **TLS & compression:** terminate at NGINX; PM2/Node shouldn’t deal with cert keys directly.
    
- **Boot integrity:** ensure your `pm2 startup` creates service units owned by root but runs _apps_ as limited users. ([pm2.keymetrics.io](https://pm2.keymetrics.io/docs/usage/startup/?utm_source=chatgpt.com "Startup Script"))
    
- **Compliance:** for GDPR/ISO/SOC2, document log retention & access controls, sanitize request logs, and capture explicit consent if you correlate metrics with user identifiers.
    
- **WS stickiness:** mandatory for stateful sessions; otherwise you risk mixed user/session state across workers. ([Socket.IO](https://socket.io/docs/v4/pm2/?utm_source=chatgpt.com "Usage with PM2"))
    

---

## 7) Networking, load balancing, compression

- **LB strategy:** Let NGINX handle external load balancing, gzip/brotli, caching, HTTP/2 or HTTP/3. PM2’s cluster does **in-host** balancing across cores.
    
- **WebSockets:** use stickiness; disable long-polling if you can (pure WS is simpler), or enable sticky if you keep fallbacks. ([Socket.IO](https://socket.io/docs/v4/pm2/?utm_source=chatgpt.com "Usage with PM2"))
    
- **Compression:** do it at NGINX (cleaner ops; fewer surprises).
    

---

## 8) Databases & queues with PM2

PM2 doesn’t manage DBs—but it decides **when** your Node code runs and **how many copies**. That impacts pools and migrations:

- Size DB pools with `instances` in mind.
    
- On `reload`, new workers should connect cleanly while old workers drain.
    
- Keep migrations in a separate, one-shot PM2 script or CI/CD step to avoid race conditions.
    

---

## 9) Filesystems & OS considerations

- **Logs:** put under `/var/log/<app>/`, rotate/compress, and back them up if needed.
    
- **Docker:** beware ephemeral filesystems; ship logs to stdout and let the platform aggregate, or mount a volume.
    
- **Startup hooks:** PM2 supports linux systemd, macOS launchd, BSD rc, etc. ([pm2.keymetrics.io](https://pm2.keymetrics.io/docs/usage/startup/?utm_source=chatgpt.com "Startup Script"))
    

---

## 10) Operations & SRE concerns

- **Zero-downtime deploys:** `pm2 reload <name>` after shipping new code.
    
- **Crash loops:** guard with `max_memory_restart`, circuit breakers in code, and health endpoints.
    
- **Observability:** `pm2 monit` locally; PM2 Plus for fleet-wide dashboards/alerts, and `@pm2/io` for app-level custom metrics. ([pm2.io](https://pm2.io/docs/plus/overview/?utm_source=chatgpt.com "Overview | PM2 Plus Documentation"), [GitHub](https://github.com/keymetrics/pm2-io-apm?utm_source=chatgpt.com "keymetrics/pm2-io-apm"))
    
- **Runbooks:** document `pm2 logs`, `pm2 describe`, `pm2 restart`, `pm2 save`, `pm2 unstartup`.
    

---

## 11) Compare & contrast

### PM2 vs. systemd / supervisord (bare-metal supervisors)

|Aspect|PM2|systemd / supervisord|
|---|---|---|
|Language-aware scaling|**Yes** (Node cluster)|No (one process per unit)|
|Zero-downtime reload|**Built-in**|Requires app support|
|Log management|App-level + logrotate|Journald/syslog|
|Dev ergonomics|Rich CLI, ecosystem file|Many knobs; generic|
|WebSocket stickiness|App-aware with docs|Done at LB|
|When to pick|Node-heavy fleet, simple scaling|Polyglot fleet with strict OS-native control|

### PM2 vs. forever / nodemon (dev tools)

- **forever** keeps a process alive; **nodemon** restarts on file changes. Neither offers PM2’s clustering, reloads, startup hooks, or monitoring.
    

### PM2 vs. Docker Compose / Kubernetes (orchestration)

- PM2 is a **per-host process manager**.
    
- Compose/K8s orchestrate containers across nodes, handle service discovery, autoscaling, rolling deploys.
    
- You can run PM2 _inside_ a container, but in K8s it’s usually redundant—let K8s do the scaling.
    

---

## 12) Pros & cons

**Pros**

- Easy multi-core scaling, zero-downtime reloads, strong CLI UX.
    
- Solid logging and startup integration; great for mono-host or small fleets.
    
- OSS runtime; hosted dashboards available. ([pm2.keymetrics.io](https://pm2.keymetrics.io/?utm_source=chatgpt.com "PM2 - Home"), [pm2.io](https://pm2.io/docs/plus/overview/?utm_source=chatgpt.com "Overview | PM2 Plus Documentation"))
    

**Cons**

- Not a cluster orchestrator (no multi-node scheduling).
    
- Sticky sessions add complexity for WS/long-polling. ([Socket.IO](https://socket.io/docs/v4/pm2/?utm_source=chatgpt.com "Usage with PM2"))
    
- In container-native shops, PM2 can duplicate what the platform already provides.
    

---

## 13) Best practices (field-tested)

1. **Front with NGINX** for TLS, gzip, HTTP/2/3, static files.
    
2. **Cluster + stickiness** for WS; otherwise pure HTTP can be round-robin. ([Socket.IO](https://socket.io/docs/v4/pm2/?utm_source=chatgpt.com "Usage with PM2"))
    
3. **Use `--env`** profiles and keep secrets out of the repo. ([pm2.keymetrics.io](https://pm2.keymetrics.io/docs/usage/application-declaration/?utm_source=chatgpt.com "Ecosystem File"))
    
4. **Startup + persist:** `pm2 startup && pm2 save`. ([pm2.keymetrics.io](https://pm2.keymetrics.io/docs/usage/startup/?utm_source=chatgpt.com "Startup Script"))
    
5. **Rotate logs** and cap memory (`max_memory_restart`).
    
6. **Health checks** and **graceful shutdown** in your Node app.
    
7. **One concern per app:** separate API, worker, scheduler.
    
8. **Document runbooks** for your team (start/reload/rollback).
    

---

## 14) Versions, pricing, plans

- **PM2 Runtime (CLI/daemon):** open-source, free.
    
- **PM2 Plus/Enterprise:** paid hosted monitoring; their FAQ confirms Plus has **no free plan** (pricing/details may change—check their page). ([pm2.io](https://pm2.io/pricing?utm_source=chatgpt.com "Pricing"))
    

Features for Plus/Enterprise include multi-server views, application overview, metrics, exceptions, alerts. ([pm2.io](https://pm2.io/docs/plus/overview/?utm_source=chatgpt.com "Overview | PM2 Plus Documentation"))

---

## 15) Recent trends & future directions

- **ESM/TypeScript first:** better source maps, ESM loaders (`--enable-source-maps`).
    
- **HTTP/3 & QUIC** at the edge (NGINX/Caddy), PM2 stays as the app supervisor.
    
- **Observability:** richer APM via `@pm2/io`, OpenTelemetry bridges. ([GitHub](https://github.com/keymetrics/pm2-io-apm?utm_source=chatgpt.com "keymetrics/pm2-io-apm"))
    
- **Container platforms:** many teams let K8s handle rollouts/health; PM2 remains popular where Node dominates or infra is VM-centric.
    
- **WebSockets → WebTransport** experimentation (still early), but the sticky-session story remains conceptually similar: keep state affinity.
    

---

## 16) Cost & compliance notes

- **Runtime cost:** PM2 Runtime free; infra cost is your VPS/VMs + ops time.
    
- **SaaS cost:** PM2 Plus/Enterprise is paid; review their current terms and pricing page before procurement. ([pm2.io](https://pm2.io/pricing?utm_source=chatgpt.com "Pricing"), [pm2.keymetrics.io](https://pm2.keymetrics.io/assets/terms_conditions.pdf?utm_source=chatgpt.com "General Terms and Conditions - PM2.IO"))
    
- **Compliance:** document log retention, least privilege, incident response. Avoid logging personal data; if unavoidable, obfuscate and set short retention.
    

---

## 17) When to use vs. when not to

**Use PM2 when…**

- You run Node services on VMs/bare metal and want quick **cluster-per-host** scaling and **zero-downtime** deploys.
    
- You need a **minimal ops surface** and friendly CLI.
    
- You’re building a **Socket.IO/WebSocket** app and want local multi-core performance (with stickiness).
    

**Skip PM2 when…**

- You already run **Kubernetes** or managed PaaS with native rolling deploys, HPA, sidecar logging, etc.
    
- You need **multi-language multi-node** orchestration (systemd + Consul/Nomad or K8s fits better).
    
- Your app is purely **serverless**.
    

---

## 18) Handy quick-reference (commands)

```bash
# install & basics
npm i -g pm2
pm2 start ecosystem.config.cjs --env production
pm2 status && pm2 logs coordinator

# scaling & rollout
pm2 reload coordinator          # zero-downtime
pm2 scale coordinator 8
pm2 restart coordinator --update-env

# boot persistence
pm2 startup
pm2 save

# describe & debug
pm2 describe coordinator
pm2 monit
```

---

## 19) Tags (for quick scanning)

#PM2 #NodeJS #ClusterMode #ForkMode #EcosystemFile #StickySessions #WebSockets #NGINX #Logs #Logrotate #Systemd #Startup #ZeroDowntime #Reload #Monitoring #PM2Plus #EnvironmentVariables #Production #DevOps #SRE #Observability #Security #Compliance #GDPR #Kubernetes #Docker #QueueWorkers #API #ReverseProxy #Performance #HighAvailability

---

If you want, I can tailor the ecosystem file to your exact **CCGSC** coordinator/worker split (including stickiness with your `/ws` path, logrotate policy, and memory guards) and add a one-page “Runbook.md” your team can follow blindfolded.