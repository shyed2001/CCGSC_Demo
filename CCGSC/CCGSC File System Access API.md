

[[Related Resources CCGSC]]
[[Related Resources Browsers]]
[[Related Resources CCGSC_System_Design]]



- **File System Access API:**
    
    - **What it is:** A new API that, with explicit user permission, allows a web app to read and write to the user's local file system.        
    - **Why it's essential:** This breaks the browser out of its traditional file-access sandbox. It's revolutionary for browser-based #IDEs (opening a project folder), video editors, and scientific tools that need to process large local datasets.
Although programmers, devs, advanced users, and task offloaders may use this or not (That group of users are considered to ne advanced users and they should use PC/Desktop Win/Linux apps and or CLI tools with SSH etc) but for web workers and spatially web workers on mobile --- 
Will not incorporating that feature on mobile devices make this app insecure and dangerous for contributors ? 

Short answer: excluding the File System Access API for mobile workers is safer. It reduces attack surface. It does not make contributors less safe.

# Definitions

- **File System Access API**: lets a _top-level_ page, with explicit user gesture, read/write user-selected files or folders. Not callable from Web Workers without a UI gesture in a window.
    
- **OPFS (Origin-Private File System)**: sandboxed storage scoped to your origin. No user picker. Safer for caches than real file access.
    

# Risks to avoid

- Phishing the picker to exfiltrate user files.
    
- Persisting sensitive task inputs/outputs to user-visible disk.
    
- Supply-chain JS invoking the picker path.
    

# Policy for CCGSC

- **Workers (browser/mobile)**: **No File System Access**. Use memory, OPFS, or IndexedDB only. Clear after task.
    
- **Uploaders/Admin tools (desktop web only)**: File access allowed behind explicit user action. Separate origin and build.
    
- **Native desktop app/CLI**: Preferred for advanced users needing true filesystem access.
    

# Safe implementation

**Role split**

- `workers.yourdomain`: worker UI. No file-picker code. Strict CSP. COOP/COEP for SAB.
    
- `console.yourdomain`: uploader console. File-picker allowed.
    

**Headers (worker origin)**

- `Content-Security-Policy: default-src 'self'; script-src 'self'; object-src 'none'; connect-src 'self' wss:; img-src 'self' data:; frame-ancestors 'none'`
    
- `Cross-Origin-Opener-Policy: same-origin`
    
- `Cross-Origin-Embedder-Policy: require-corp`
    

**Data handling (workers)**

- Stream inputs to WASM/WebGPU. Keep in RAM when possible.
    
- If caching is needed, use **OPFS or IndexedDB**, not user files.
    
- Wipe caches on completion or after TTL.
    
- Never request or hint at `showOpenFilePicker` / `showDirectoryPicker`.
    

**Code guards**

- Build-time: exclude picker imports from worker bundle.
    
- Runtime: feature-flag by role; block any UI that could trigger file dialogs in worker origin.
    

**Mobile specifics**

- Mobile browser support for the picker is fragmented. OPFS/IndexedDB are the portable options.
    
- Constrain task chunk sizes; avoid large persistent caches to prevent quota prompts.
    

# Why this is safer

- Workers cannot open user files at all.
    
- All storage stays origin-sandboxed (OPFS/IndexedDB).
    
- Even if a module is malicious, it runs in a Worker/WASM sandbox with no file handles.
    

# When to allow real file access

- Only in the **uploader console** for power users who choose local datasets and understand the prompt.
    
- Prefer the **desktop app/CLI** for heavy I/O pipelines.
    

# Minimal checklist

-  Separate origins by role.
    
-  CSP with no third-party scripts on worker origin.
    
-  No file-picker code paths shipped to worker bundle.
    
-  Workers use OPFS/IndexedDB only, with TTL cleanup.
    
-  Periodic “Clear local data” control in UI.
    

Confirm two choices so I lock policies:

1. Approve **“no File System Access on worker origin”** and **OPFS/IndexedDB-only** for caches, yes/no?
    
2. Do you want a **desktop uploader app/CLI** as the recommended path for advanced users needing local file access, yes/no?