


# Top-level runtime & ops

   [[PM2 is a production-grade process manager for Node.js.]]
   [[CCGSC_PM2 app - ecosystem.config.cjs]]      [[CCGSC_PM2_ecosystem.config_cjs.txt]]
   
- **PM2 app**: `ecosystem.config.cjs`   runs the Node coordinator (`coordinator_server.js`) and configures log paths; cluster mode is noted (commented) if you want to turn it on later. 
    
- **NGINX sites**: two TLS virtual hosts point at your `/public` folder—one for the **Director** UI (index `director.html`), one for the **Worker** UI (index `worker.html`). Both can proxy “dynamic” routes (and WS upgrades) to the Node server on `127.0.0.1:8080`. [[NGINX CCGSC]] [[CCGSC_NGINX_Config.txt]]
    

# Coordinator backend (Node)

- **`coordinator_server.js`**:  [[coordinator_server_js.txt]]   [[coordinator_server_js]]  a WebSocket server bound locally at `ws://127.0.0.1:8080/ws`. It defines the global problem size (`N`), the number of chunks (`TOTAL_TASKS`), heartbeat/timeout, and it persists CSV logs for tasks and workers. It owns the worker registry and handles Director commands (start, pause, resume, restart).  
    It also emits state changes (e.g., `computationStateChanged`) to the Director and logs run state; you added those hooks in this file.
    

# Frontend: Director (control & dashboards)

- **`public/director.html`**: [[CCGSC_Director_html.txt]]  [[CCGSC_Director_html]]  the main dashboard. It’s a Tailwind-styled page with controls (start/pause/resume/restart) and tables/bars for worker/task status.  
    It opens a WSS connection to `wss://ccgsc-director.digitalbd.org/ws`, stores live state in **IndexedDB** (`state`, `logs` object stores), and uses a **BroadcastChannel** to notify other views.
    
- **`public/director.js`**  [[CCGSC_director_Js.txt]]   [[CCGSC_director_Js]]   (alternate/earlier controller): connects to the director WS, maintains a running total using `BigInt`, and updates the progress UI and a worker table. 
  **`public/director.js` is legacy.** Your live dashboard logic is baked into `public/director.html` (inline script), and NGINX serves that HTML directly as the Director app entry point. There’s no `<script src="director.js">` in the page, so `director.js` isn’t loaded in the current flow.

Why I called it “alternate/earlier controller”:

- The **current** Director uses an **inline controller** in `director.html` that opens the WS, writes state to IndexedDB, and renders workers/progress. You can see it connect and register here.
    
- The **older** `director.js` expects different events like `workerConnected`/`workerDisconnected`, which your coordinator no longer emits (the new protocol uses `workerUpdate`, `workerRemoved`, and `fullState`). [[CCGSC_director_Js.txt]]  [[CCGSC_director_Js]]
    
- The coordinator’s outbound messages match the **new** events your inline script handles (e.g., `progress`, `workerUpdate`, `fullState`).
    
What to do next (pick one):

- **Keep the modern inline controller** (simplest): leave `director.js` in the repo but mark it as deprecated or move it to `legacy/` so new contributors aren’t confused.
    
- **Or switch to external JS:** extract the inline logic from `director.html` into a new `public/director.controller.js` and include it with `<script src="director.controller.js" type="module"></script>`—but keep the **new** message names (`fullState`, `workerUpdate`, `workerRemoved`, `computationStateChanged`, `progress`) rather than the old ones. The current `director.js` would still need refactoring to the new protocol.
  
    

# Frontend: Worker (the browser compute node)

- **`public/worker.html`**: [[CCGSC_worker_html.txt]]   [[CCGSC_worker_html]]  the worker landing page (styled, responsive). It instructs users to keep the tab open and links to a dedicated worker tab; it’s the static container around your compute script.
    
- **`public/worker.js`**: [[CCGSC_Worker_Js.txt]]    [[CCGSC_Worker_Js]]     connects each worker tab to `wss://ccgsc-demo.digitalbd.org/ws`, registers as a worker, loads the Emscripten module (`prime_library.js`), and runs the assigned `[worker_func_${taskId}]` over BigInt ranges; results are returned over WS. [[Super Worker Nodes]]
    

# In-browser compute (WASM + Web Workers)

- **`public/computation_worker.js`**: a **Dedicated Web Worker** script. It lazily loads the WASM module once, then executes `count_primes_in_range` in cooperative sub-chunks, sending status/progress and a final total back to the main thread.
    
- **`public/worker_bootstrap.js`**: a lighter worker shell used for “one-chunk, one-call” flows (`worker_func_${id}`), posting back `{ workerId, count }`.
    
- **`public/prime_library.js`**: the Emscripten-generated glue for your WASM module; it handles streaming compilation/instantiation and exposes `ccall`.
    

# Logs & detail views (read-only, local)

- **`public/LogWorkerTaskProgressData.html`**: a live “tail” of your **IndexedDB** `logs` store, refreshed via `BroadcastChannel`. Useful for a transparent audit feed during runs.
    
- **`public/progress_details.html`**: renders a grid of **per-task** results from the `state` store for fine-grained monitoring.
    

# Client info helper

- **`public/stats.js`**: collects lightweight client info (CPU cores and browser/OS fingerprint) for display/assignment heuristics.
    

# Docs & design notes

- **`CCGSC_Research_Proposal.md`** and **`CCGSC_System_Design.md`** hold the concept, motivation, and browser-based HPC rationale you’re building toward (crowd compute, Wasm, workers, WS).
    

---

## How it all fits (execution flow)

1. **NGINX** serves your static pages in `/public` and forwards WS traffic to the local Node **coordinator**. Director and Worker get separate entry pages (two vhosts, two index files).
    
2. **Director** opens WSS to the coordinator and persists cluster state + append-only logs in **IndexedDB**; views (logs and detailed grid) listen via **BroadcastChannel**.
    
3. **Workers** connect via WSS, load **WASM** (`prime_library.js`), and compute assigned ranges (either via the page thread using `worker.js` or in a **Dedicated Worker** via `computation_worker.js`).
    
4. **Coordinator** assigns chunks, receives results, updates the run state, and logs to CSV; it also exposes control messages back to the Director (start/pause/resume/restart).
    
