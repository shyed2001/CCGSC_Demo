

produce a short form and another long form README and a directory tree/s (with the exact file list and “who-calls-who”) so a new contributor can grok the whole thing in under five minutes. And Also generate a  README diagram ( and mermaid) that matches this exact wiring and lists the WS message types your coordinator currently recognizes — handy for future contributors.


you got it—here’s a newcomer-friendly “grok kit” for your repo: a short README, a long README with the real wiring, an exact directory tree, a who-calls-who map, and a Mermaid diagram that also documents the WebSocket message types your coordinator understands.

---

# Short README (TL;DR)

**What this is.** A browser-based distributed compute prototype: a **Director** page starts/pauses/resumes runs; many **Worker** pages connect from anywhere and crunch tasks (WASM) in their own Web Workers; a **Coordinator** Node server assigns work and aggregates results. NGINX fronts everything and proxies `/ws` to Node.

**Run it.**

1. Start the coordinator (Node + `ws`): `node coordinator_server.js` (or PM2 via `ecosystem.config.cjs`). Coordinator listens on `ws://127.0.0.1:8080/ws`.
    
2. Serve `public/` via NGINX:
    
    - `ccgsc-director.digitalbd.org` → `public/director.html`
        
    - `ccgsc-demo.digitalbd.org` → `public/worker.html`
        
    - Both proxy `/ws` → `http://127.0.0.1:8080` (WebSocket upgrade on).
        
3. Open **Director**: it connects to `wss://ccgsc-director.digitalbd.org/ws`, registers as director, and can start/pause/resume/restart/clear state.
    
4. Open **Worker(s)**: they connect to `wss://ccgsc-demo.digitalbd.org/ws`, register with CPU/browser info, get tasks, run WASM in a Web Worker, and stream results + heartbeats/memory updates.
    

**Coordinator accepts**: `registerDirector`, `registerWorker`, `startComputation`, `pauseComputation`, `resumeComputation`, `restartServer`, `clearState`, `terminateWorker`, `memoryUpdate`, `stillWorking`, `result`, `error`.

---

# Long README (full context, exact wiring)

## Big picture

- **Director UI** (`public/director.html`, or the older `public/director.js`-driven page) opens a WebSocket to the coordinator and **sends control commands**; it stores live state/logs in **IndexedDB**, and renders aggregate progress + workers table.
    
- **Worker UI** (`public/worker.html`) connects to the coordinator, registers with **browser+CPU** info from `stats.js`, receives a **task**, and hands it to a Web Worker (`computation_worker.js`). That worker calls into the **WASM module** (`prime_library.js`) and posts back `stillWorking` and a final `result`.
    
- **Coordinator** (`coordinator_server.js`) runs a `ws` server on `/ws`, tracks connected workers, assigns tasks, handles timeouts/heartbeats, and streams **progress / full state / worker updates** back to the director. It also persists state and writes CSV logs for tasks/workers.
    
- **NGINX** terminates TLS and proxies both Director+Worker sites and WebSockets along `/ws` to the Node coordinator.
    

## Endpoints & clients

- **Director** connects to `wss://ccgsc-director.digitalbd.org/ws` (also shown in `director.html` connection code).
    
- **Worker** connects to `wss://ccgsc-demo.digitalbd.org/ws`.
    

## Storage & logs

- **IndexedDB (Director)**: object stores `state` and `logs` mirror live `fullState`, `progress`, `workerUpdate`, `workerRemoved`, and `computationStateChanged` msgs.
    
- **Files (Coordinator)**:
    
    - `computation_state.json` (snapshot state).
        
    - `task_log.csv`, `worker_log.csv` (CSV audit trails).
        

## Heartbeats, timeouts, resilience

- Heartbeat pings every `HEARTBEAT_INTERVAL`, requeue on timeout, update worker status, and reassign tasks.
    
- Worker **memoryUpdate** every 15s; coordinator forwards to director via `workerUpdate`.
    
- On **clearState**: reset memory state, rebuild queue, push fresh `fullState` to the director.
    

---

# Exact directory tree (discovered files)

```
prime_distributed_projectPrlCc1B V5(10K)/
├─ coordinator_server.js
├─ ecosystem.config.cjs
├─ prime_distributor.txt                         # nginx sites-available notes
├─ public/
│  ├─ director.html
│  ├─ director.js
│  ├─ worker.html
│  ├─ worker.js
│  ├─ stats.js
│  ├─ computation_worker.js
│  ├─ worker_bootstrap.js
│  ├─ prime_library.js                           # Emscripten glue for WASM
│  ├─ LogWorkerTaskProgressData.html
│  └─ progress_details.html
```

Evidence: coordinator path and config; NGINX doc with `root .../public` and `index director.html` / `worker.html`; public assets used/linked across worker/director HTML/JS files.

> If you expect 20 files and only 12–13 are listed here, these are the files present in the upload I can see. Drop in any missing ones and I’ll extend the tree and call-graph to match exactly.

---

# Who-calls-who (call graph, by file)

- **public/director.html**  
    → opens `WebSocket('wss://ccgsc-director.digitalbd.org/ws')` and sends `{type:'registerDirector'}`  
    → on UI actions sends `{startComputation|pauseComputation|resumeComputation|restartServer|clearState}`  
    ← receives `{log|fullState|progress|workerUpdate|workerRemoved|computationStateChanged}` and reflects them into IndexedDB and UI.
    
- **public/director.js** (older director page)  
    → same WS registration and controls  
    ← handles `{log, workerConnected, workerDisconnected, progress, complete}` for the legacy UI table/bars.
    
- **public/worker.html**  
    → imports `stats.js` to read `cpuCores` & `browserInfo`  
    → spawns `new Worker('./computation_worker.js', {type:'module'})`  
    → opens `WebSocket('wss://ccgsc-demo.digitalbd.org/ws')`, sends `{type:'registerWorker', workerId, browserInfo, cpuCores}`  
    ← on `{type:'task'}` → `postMessage({task})` into the Web Worker  
    ← from Web Worker relays `{stillWorking|result|error}` back to coordinator  
    → periodic `{type:'memoryUpdate'}` every 15s.
    
- **public/computation_worker.js** (runs in browser Web Worker)  
    → imports `prime_library.js` (Emscripten glue) and lazily initializes it  
    ← receives `{task}` from main thread; loops chunkwise; for each chunk posts `{type:'stillWorking'}`; at end posts `{type:'result', count}`.
    
- **public/worker.js** (alternate “single-thread” worker w/o sub-chunking)  
    → loads WASM and calls `wasmModule.ccall('worker_func_<id>')` then sends `{type:'result'}`; on errors sends `{type:'error'}`.
    
- **coordinator_server.js** (Node, `ws` server at `/ws`)  
    ← receives control: `{registerDirector, startComputation, pauseComputation, resumeComputation, restartServer, clearState, terminateWorker}`  
    ← receives worker telemetry: `{registerWorker, memoryUpdate, stillWorking, result, error}`  
    → sends to workers: `{type:'task', task}`  
    → sends to director: `{fullState, computationStateChanged, workerUpdate, workerRemoved, log, progress}`  
    • also: heartbeat/ping, timeouts, CSV logging, persisted state reload/save.
    

---

# Coordinator WebSocket message types (canonical list)

**Inbound → Coordinator**

- `registerDirector` (from Director)
    
- `registerWorker` (from Worker; includes workerId, cpuCores, browserInfo)
    
- `startComputation`
    
- `pauseComputation`
    
- `resumeComputation`
    
- `restartServer` _(present in Director UI; coordinator logs use `exec`)_
    
- `clearState` (reset state & push new `fullState`)
    
- `terminateWorker` (forcefully close a worker)
    
- `memoryUpdate` (browser JS heap usage → reflected to director)
    
- `stillWorking` (heartbeat-with-task)
    
- `result` (final chunk count for a task)
    
- `error` (task failed; requeue).
    

**Outbound ← Coordinator**

- To **Director**:  
    `fullState`, `computationStateChanged`, `workerUpdate`, `workerRemoved`, `log`, `progress`.  
    _(The legacy director also handled `workerConnected/workerDisconnected`/`complete` in its JS; the current coordinator emits logs and `computationStateChanged` instead of a dedicated `complete` event)._
    
- To **Worker**:  
    `task` (assignment with `{taskId,start,end}`).
    

---

# README diagram (Mermaid)

```mermaid
flowchart LR
  subgraph Browser[Worker Browser]
    WUI[worker.html] -- postMessage{task} --> WW[computation_worker.js]
    WW -- "ccall(...)\nprime_library.wasm" --> WASM[prime_library.js]
    WUI <-- "status / result / error / stillWorking" --> WW
    WUI -- "registerWorker,\nstillWorking,\nresult,error,\nmemoryUpdate" --> WSSW
  end

  subgraph Browser2[Director Browser]
    DUI[director.html or director.js]
    DUI -- "registerDirector,\nstart/pause/resume,\nclearState,restartServer,\nterminateWorker" --> WSSD
    DUI <-- "fullState,\nprogress,\nworkerUpdate,\nworkerRemoved,\ncomputationStateChanged,\nlog" -- WSSD
  end

  subgraph Nginx[NGINX TLS/Proxy]
    WSSD[(/ws)]:::ws
    WSSW[(/ws)]:::ws
  end

  subgraph Node[Coordinator (Node ws)]
    COORD[coordinator_server.js]
  end

  WSSD --> COORD
  WSSW --> COORD
  COORD -- "task" --> WSSW

  classDef ws fill:#eef,stroke:#66f,stroke-width:1px;
```

**Notes**

- Director WS URL: `wss://ccgsc-director.digitalbd.org/ws`.
    
- Worker WS URL: `wss://ccgsc-demo.digitalbd.org/ws`.
    
- NGINX proxies `/ws` to `127.0.0.1:8080` with Upgrade headers.
    

---

# Contribution-oriented quickstart (for new devs)

1. **Coordinator**
    
    - Start dev: `node coordinator_server.js` (WS on `127.0.0.1:8080/ws`).
        
    - What it does: splits `[1..N]` into `TOTAL_TASKS`, enqueues, assigns, persists, logs CSVs, heartbeats, timeouts.
        
2. **Director**
    
    - Open `public/director.html` locally (or via `ccgsc-director...`). It registers and pulls `fullState` immediately, then you can start/pause/resume/clear.
        
    - IndexedDB mirrors state & logs so the UI can redraw from local cache.
        
3. **Workers**
    
    - Open `public/worker.html` on any device; it registers with ID + browser stats and periodically sends `memoryUpdate`.
        
    - The compute happens in a Web Worker (`computation_worker.js`) calling WASM (`prime_library.js`) with BigInt-safe `ccall`.
        
4. **Ops**
    
    - NGINX site blocks in `prime_distributor.txt` show the proxying pattern and web roots for director/worker sites.
        

---

## Appendix: “who recognizes what” cheat-sheet

**Director sends:** `registerDirector`, `startComputation`, `pauseComputation`, `resumeComputation`, `restartServer`, `clearState`, `terminateWorker`.

**Worker sends:** `registerWorker`, `stillWorking`, `result`, `error`, `memoryUpdate`.

**Coordinator sends:**

- To **Director**: `fullState`, `progress`, `workerUpdate`, `workerRemoved`, `computationStateChanged`, `log`.
    
- To **Worker**: `task`.
    

---

Want me to bundle this into actual `README.md` + `README_full.md` files and drop the Mermaid diagram in the short one as well as a `docs/` call-graph? I can also extend the message-type table with payload schemas (field names/types) inferred from the code so future contributors don’t have to spelunk.
