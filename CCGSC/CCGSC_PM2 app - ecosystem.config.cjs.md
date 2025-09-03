

 <%

// ============================================================================
// file path: prime_distributed_projectPrlCc1B%20V5%2810K%29/ecosystem.config.cjs
// PURPOSE: PM2 process manager configuration for your CCGSC coordinator (Node.js).
// LANGUAGE MODE: CommonJS (CJS). PM2 loads this file with Node's CJS loader.
// DSA NOTE: This config is a plain JavaScript object literal. The top-level
//           "module.exports" is a single object with one property: "apps",
//           which is an ARRAY of PROCESS DESCRIPTOR OBJECTS. PM2 iterates this
//           array to spawn and supervise each entry (process).
// CONTROL FLOW (at runtime):
//   1) You run "pm2 start ecosystem.config.cjs".
//   2) PM2 loads Node, requires() this file, and reads module.exports.
//   3) For each object in exports.apps[], PM2 forks/spawns a process according
//      to the descriptor (script, mode, env, logs, etc.).
//   4) PM2 supervises lifecycle (start, restart on crash, logging, etc.).
//   5) Your NGINX reverse proxy (based on your sites-available config) talks
//      to the coordinator on 127.0.0.1:8080 (/ws), so "script" MUST launch the
//      WebSocket server. Data flows: Browser <-> NGINX (TLS) <-> PM2/Node app.
// FILESYSTEM NOTE (logs):
//   - Ensure the log directory exists and is writable by the "user" below:
//       sudo mkdir -p /var/log/coordinator && sudo chown -R www-data:www-data /var/log/coordinator
// SECURITY/OPS NOTE:
//   - Running as "www-data" helps keep permissions consistent with NGINX,
//     but you must start PM2 under a user with the rights to setuid/setgid or
//     configure a systemd unit that runs PM2 as root and spawns "www-data" apps.
// ============================================================================

module.exports = {                                // CommonJS export. PM2 reads this object.
  apps : [{                                       // "apps" = ARRAY of process descriptors (can run many apps).
    name      : "coordinator",                    // Human-friendly name in "pm2 ls" / logs.
    script    : "coordinator_server.js",          // Entry point file for Node. Must start your WSS on 127.0.0.1:8080/ws.
                                                  // (Your coordinator uses ESM imports; ensure package.json has "type":"module".)

    watch     : false,                            // File-watch restarts OFF (safer in prod; avoids restart storms).
                                                  // In dev, turning this true can auto-restart on code changes.

    user      : "www-data",                       // PM2 will drop privileges/run the app as this system user.
                                                  // Why: Aligns file/dir permissions with NGINX + least-privilege.

    // --- CLUSTER MODE (OPTIONAL) ---
    // instances : "max",                         // If uncommented: spawn one Node worker per CPU core.
                                                  // PM2 will round-robin (or sticky for WS) across processes.
    // exec_mode : "cluster",                     // Use Node's cluster under PM2; enables multi-core parallelism.
                                                  // IMPORTANT for WebSockets: if you front this with NGINX, consider
                                                  // "pm2 start ecosystem.config.cjs --sticky" or "pm2 set pm2:sticky true"
                                                  // to enable sticky sessions so a WS client stays on the same worker.

    // --- LOGGING (FILES) ---
    output    : "/var/log/coordinator/out.log",   // STDOUT log path (application "console.log" output).
    error     : "/var/log/coordinator/error.log", // STDERR log path (stack traces, errors).
                                                  // You had alternates below; keep one set active.

    // output    : "/pm2Logs/coordinator/out.log",// (ALT) If you prefer a custom log root, create and chown it.
    // error     : "/pm2Logs/coordinator/error.log",

    // --- ENVIRONMENT VARIABLES (RUNTIME) ---
    env       : {                                 // Map<string, string> passed to the process environment.
      NODE_ENV: "production",                     // Signals prod behavior (e.g., no hot reloaders, prod logging).
                                                  // Your code can read process.env.NODE_ENV to toggle behavior.
    },

    // --- OPTIONAL TUNING (commented; enable if desired) ---
    // max_memory_restart : "1G",                 // Auto-restart if RSS exceeds limit (memory leak guard).
    // merge_logs         : true,                 // Combine logs from all instances (when cluster mode is on).
    // time               : true,                 // Prepend human-readable time to each log line (PM2 managed).
    // log_date_format    : "YYYY-MM-DD HH:mm Z", // Custom timestamp format in logs.
    // node_args          : ["--enable-source-maps"], // Helpful for stack traces with ESM/transpiled code.
    // kill_timeout       : 5000,                 // Grace period (ms) before PM2 SIGKILL after SIGINT/SIGTERM.
    // listen_timeout     : 8000,                 // Time to consider app "online" (useful if boot takes time).
  }]
};

// ============================================================================
// The block below is your ALTERNATE / EARLIER MULTI-APP CONFIG kept as a
// commented reference. It shows (1) coordinator in cluster mode + (2) a
// local static HTTP server (Python) bound to 127.0.0.1, meant to be fronted
// by NGINX only. I've expanded comments to explain every field.
// ============================================================================

/*
module.exports = {                                // (ALT) Export a DIFFERENT config with TWO apps.
  apps : [{                                       // (ALT) First app descriptor: coordinator (Node).
    name   : "coordinator",                       // (ALT) PM2 name in the process list.
    script : "coordinator_server.js",             // (ALT) Entry point for the coordinator WS server.

    // ⬇️ *** CHANGE THIS LINE TO FALSE *** ⬇️   // (ALT) You already set watch:false in prod above.
    watch  : false,                               // (ALT) Disable auto-restarts on file changes.

    // Add the user directive for correct file permissions
    user   : "www-data",                          // (ALT) Run as www-data for permission alignment.

    // --- ADD THESE TWO LINES ---                // (ALT) Enable multi-core scaling via cluster mode.
    instances : "max",                            // (ALT) One worker per CPU core. Can be a number (e.g., 4).
    exec_mode : "cluster",                        // (ALT) PM2 clusters Node; better parallel request handling.
                                                  // NOTE: For websockets, use sticky sessions (via PM2/NGINX).

    env    : {
      NODE_ENV: "development",                    // (ALT) Dev flavor; you may flip to "production" for prod.
    }
  }, {
    // (ALT) Second app descriptor: a tiny STATIC FILE SERVER for the /public folder.
    //       Useful if you didn't want NGINX to serve files directly, but here you
    //       bind ONLY to localhost and have NGINX proxy to it (safer than 0.0.0.0).
    name   : "http-server",                       // (ALT) A friendly name for the static server.
    script : "python3" || "python",               // (ALT) PM2 can run non-Node scripts; it launches Python.
                                                  //       The "||" here is plain JS: resolves to "python3" if truthy
                                                  //       else "python" — effectively picks "python3".

    //args   : "-m http.server 8008 --bind 0.0.0.0", // (ALT) PUBLIC bind (NOT recommended; exposes port).
    args   : "-m http.server 8008 --bind 127.0.0.1", // (ALT) Bind ONLY to localhost; NGINX is the public face.

    // Note: We bind to 127.0.0.1 now because only Nginx will talk to this server, not the public internet.
    cwd    : "./public",                          // (ALT) Current working dir: where Python will serve files from.
    watch  : false,                               // (ALT) No need to restart Python when files change in prod.

    env    : {
      NODE_ENV: "development",                    // (ALT) Environment for this helper app; not critical.
    }
  }]
}
*/

// ============================================================================
// END OF FILE NOTES:
// - Data Structure (DSA): "apps" is an Array; each member is an Object
//   with keys PM2 understands. There are no algorithms here—PM2 is the
//   orchestrator. Your execution logic/algorithms live in coordinator_server.js.
// - Data Flow:
//   * Inbound WS from browsers -> NGINX TLS vhosts -> proxy to 127.0.0.1:8080/ws.
//   * PM2 owns the Node worker(s) that accept those WS connections.
//   * Logs stream from process stdout/stderr into the log files configured above.
// - Control Flow:
//   * pm2 start|restart|reload|stop affects processes defined in this file.
//   * Cluster mode (if enabled) fans out work across CPU cores; for WebSockets
//     use sticky sessions to keep a client pinned to one worker.
// - Operational Commands (for reference):
//     pm2 start ecosystem.config.cjs
//     pm2 reload coordinator                  # zero-downtime (when cluster)
//     pm2 restart coordinator                 # hard restart
//     pm2 logs coordinator                    # tail logs
//     pm2 startup systemd && pm2 save         # boot-time autostart
// ============================================================================

 %>
