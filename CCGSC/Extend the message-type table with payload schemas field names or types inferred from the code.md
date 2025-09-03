

Deliciously specific upgrade: here’s the **extended WebSocket message table** with **payload schemas** inferred straight from your code so nobody has to spelunk through files again. I split by direction, used JSON-ish shapes with types, and added gotchas (e.g., BigInt-as-strings).

---

# Coordinator ⇐ Director (incoming)

|Type|Payload schema|What it does / Notes|
|---|---|---|
|`registerDirector`|`{ type: "registerDirector" }`|Registers the dashboard connection and immediately pushes a `fullState` snapshot.|
|`startComputation`|`{ type: "startComputation" }`|Clears prior state file if any, initializes tasks, flips `isRunning=true`, logs, and notifies UI via `computationStateChanged`.|
|`pauseComputation`|`{ type: "pauseComputation" }`|Sets `isRunning=false`, saves, notifies UI via `computationStateChanged`.|
|`resumeComputation`|`{ type: "resumeComputation" }`|Sets `isRunning=true`, saves, reassigns tasks, notifies UI via `computationStateChanged`.|
|`restartServer`|`{ type: "restartServer" }`|PM2 restart via `exec`.|
|`clearState`|`{ type: "clearState" }`|Deletes state file, resets memory state, re-initializes queue, pushes fresh `fullState` to director.|
|`terminateWorker`|`{ type: "terminateWorker", workerId: string }`|Force-closes a specific worker’s socket; UI later receives `workerRemoved`.|

---

# Coordinator ⇐ Worker (incoming)

|Type|Payload schema|What it does / Notes|
|---|---|---|
|`registerWorker`|`{ type: "registerWorker", workerId: string, browserInfo?: string, cpuCores?: number|string }`|
|`memoryUpdate`|`{ type: "memoryUpdate", workerId: string, memory: { usedJSHeapSize: string } }`|Coordinator stores memory info on worker, forwards via `workerUpdate`. `usedJSHeapSize` looks like `"123.45 MB"`.|
|`stillWorking`|`{ type: "stillWorking", workerId: string, taskId: number, memory?: { usedJSHeapSize: string } }`|Heartbeat from worker while busy; refreshes assignment timer; optional memory piggybacks and is forwarded.|
|`result`|`{ type: "result", workerId: string, taskId: number, count: string }`|Marks task complete, updates `results[taskId]=count`, bumps stats, emits `progress` + `workerUpdate`, maybe ends run. `count` is a decimal stringified BigInt.|
|`error`|`{ type: "error", workerId: string, taskId: number, message: string }`|Re-queues task, marks worker idle with error status, emits `workerUpdate`.|

---

# Coordinator ⇒ Director (outgoing)

|Type|Payload schema|When/why|
|---|---|---|
|`fullState`|`{ type:"fullState", nValue:number, totalTasks:number, isRunning:boolean, results:(string|null)[], workers:[string, WorkerInfo][] }`|
|`progress`|`{ type:"progress", taskId:number, count:string, totalCompleted:number }`|Emitted per completed task. `count` is decimal string.|
|`workerUpdate`|`{ type:"workerUpdate", workerId:string, workerInfo: WorkerInfo }`|Any time a worker connects, gets assigned, updates memory, errors, timeouts, or completes. BigInts inside `workerInfo` are stringified.|
|`workerRemoved`|`{ type:"workerRemoved", workerId:string }`|On worker socket close, after cleanup/requeue.|
|`computationStateChanged`|`{ type:"computationStateChanged", isRunning:boolean }`|Broadcast when start/pause/resume toggles. Director writes `isRunning` into IndexedDB.|
|`log`|`{ type:"log", message:string }`|Human-readable coordinator events piped to UI and logs store.|

**`WorkerInfo` shape (as sent to director)**

```ts
type WorkerInfo = {
  ws?: any               // not actually serialized
  isBusy: boolean
  assignedTask: { taskId:number, start:number, end:number } | null
  taskAssignedTime: number | null
  stats: {
    tasksCompleted: number
    primesFound: string   // BigInt serialized via bigIntReplacer
    lastTaskTime: number | null
    memory?: { usedJSHeapSize: string } // if provided by worker
  }
  browserInfo: string
  cpuCores: number | string
  ipAddress: string
  status: string
  currentTask: number | null
  memory?: { usedJSHeapSize: string }   // mirrored to top-level for UI
}
```

The coordinator converts any BigInt to a decimal string during `JSON.stringify` via `bigIntReplacer`, which is why `primesFound` and per-task `count` are strings.

---

# Coordinator ⇒ Worker (outgoing)

|Type|Payload schema|Purpose|
|---|---|---|
|`task`|`{ type:"task", task: { taskId:number, start:number, end:number } }`|Assignment for the next subrange; workers later coerce to BigInt when calling WASM.|

---

## Director UI expectations (for completeness)

- Updates `results[taskId]` when `progress` arrives; persists `fullState` and diffs workers on `workerUpdate`; flips `isRunning` on `computationStateChanged`.
    

---

## Worker browser side (shape it sends)

- Connect & identify: `registerWorker` includes `workerId`, `browserInfo`, `cpuCores`.
    
- Periodic: `stillWorking` (and optional `memoryUpdate`).
    
- Finish or fail: `result` with `count:string`; `error` with `message`.
    

---

## Tiny gotchas future-you will thank you for

- **BigInt serialization:** Coordinator uses `bigIntReplacer` so any BigInt becomes a **decimal string** over WS. Treat `count` and `workerInfo.stats.primesFound` as strings in the UI layer.
    
- **Memory stats wire format:** `usedJSHeapSize` is a human string like `"123.4 MB"`, not a number; the UI prints it verbatim.
    
- **Worker termination path:** There’s no explicit `terminateAck`; after `.terminate()` the director will get `workerRemoved`.
    

---

If you want, I can emit **TypeScript types** or **JSON Schemas** for all payloads and drop in a lightweight validator (e.g., `zod`) so bad wires are rejected before they bite.