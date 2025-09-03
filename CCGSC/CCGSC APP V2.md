[[0 CCGSC_Manuscript_Organizer_Dashboard]]
[[CCGSC_System_Design]]
[[CCGSC APP V1]]



CCGSC APP VERSION 2
Make a page that can connect offloads wasm tasks to web-workers from all over the world. Users -Devs Programmers will offload their task to a page or upload wasm files with glue js codes to a ccgsc page upload page platform, then those wasm tasks will be offloaded to the web-workers who were and or will be connected to the web-worker platform page. Types of tasks - massively parallel tasks, deep nested loops, massively parallel oop tasks like maybe Monte-carlo and or future event prediction, ai ml cnn ann nn gpt llm training and test, mathematics problems like prime counting etc

My plan - I will use multiple vps with 3 and or 6 cpu for concurrent and parallel processes and connections, ubuntu os servers, nginx, npm, pm2, reidis for process management, pgsql for master record, apache cassandra or that type db for all processes where needed per second, indexed db or sqllite for browser webworkers, provide and or use dbms and platform pages, and connection, log in and connection between users and workers and try to provide security, chwcks and audit and rewards for workers. Workers will be primarily web browser based workers, no download needed.

After that also make go, cgo and webview2 sqllite desktop app and

.Net Maui sqlite mobile apps too. Apps will also use browser or chromiam as workers and will also have additional capabilities as native apps.

The devs programmers will have to program code their problems, so that thay are divided into many parts or similar parts that can be replicated by wasm and js codes and offloaded to the platform with consolidating code too.

The platform will only obey the uploded js and wasm and glue js code and code logic. Data will be web links or online dbms links, dataset etc and or embedded data into wasm module or js code file.

Will not use shared array buffet and or mpi. 

How would and should i design the Backend, Logic and DBMS for that system

The design u gave -can this run Nginx and Pm2 in cluster mood with the help of Redis and can this let Users Devs Programmars uploads offload tasks WASM+JS code in all at once or in batches and as when and what needed to the upload page and that then will, be managed and orchrestarated by the platform server and the results and some need to know logas from WebWorkers and Servers can be given back to the Devs and Users. (Many workers, many users, many tasks interacting with the platform pages) Are we using WebSockets ws/wss or http/https ? in nginx and or in NodeJs ?

What if I don't want to use React and or any Js or css framework to make it heavy and slow?

Why are we using Express?

is there any better of faster alternatives? or using Next.Js and Or Express.Js will have very negligible impact on the performance on everything?

I want to take or code as long as it takes to build, but make it best, safe, efficient and user-friendly. Safe seconds of millions of users but spent some more time for the development of the platform. But make it so that it is not very complicated and not fragile and not unmaintainable. Like my current code, existing server code and setup, I want to scale up and appent and add features -- using --Nginx, NodeJS (Best or good for debugging with on Browser) , asm.js, PM2, NPM, DBMS, HTML, CSS, and maybe some more performance boosting Go/CGo, C/C++ codes and logics or some library or framework as u suggest.

What, why, when, where --- is Fastify? Why are u talking about relayes? Why do I need an API and or API server and or HTTP API ? WS relay and or uWebSockets.js), SRI, SSE, Where and how will I use them? If you want maximum performance without leaving Node, pick Fastify + uWebSockets.js. -- how, why, when, where? I also want to use HTML and Vanilla CSS, and JS if needed, for all pages needed code. Web Workers, and worker and user apps will use IndexedDB and SQLite too -- ???.

What does my current project code structure, which uses 20 uploaded files?

Existing Project Code Execution flow, Control flow, Data flow, Point of Entry, Exit point, End point/s.

and also separately tell-

Which file does what, where, when, and why?

produce a short form and another long form README and a directory tree/s (with the exact file list and “who-calls-who”) so a new contributor can grok the whole thing in under five minutes. And Also generate a README diagram ( and mermaid) that matches this exact wiring and lists the WS message types your coordinator currently recognizes — handy for future contributors.

Extend the message-type table with payload schemas (field names/types) inferred from the code so future contributors don’t have to spelunk.

So I will use NGINX, PM2 cluster mode with my 3 or 6 core server, Node.js, Fastify. How to use Redies for PM2 process management in 3 or 6 core cluster mode.

My nginx server will have a pm2 process in cluster mode with redis for cluster management. The main NodeJS Fastify app will always run using the pm2 .cjs file. The main Node.js app will use Apache Cassandra for daily use and PostgreSQL for data backup. Web-Workers will join to the public domain link a web worker pool, these web workers will get assigned WASM and or asm.js modules as part of a distributed computing node. Users-Devs-Programmers will log in and join Task offloader que-line. they will be able to aff load MaiJs code to manage all their modules and orchrestrate eberything in theit app/program-with Wasm modules and glueJs and they will upload their code into the platform (devs have the duty to break theit promlems into chunks and or many mnay repeated steps and grids and or parallel parts, so that they can get the shole thing back - the results and or mode or imulation back). The main.js code files , that are, were uploaded or being uploaded by users-devs -will be then run by the server and accordingly glue js and wasm codes will be distributed to the webweokers and the results from tose wasm and or asmjs code execution will be given back to the respective mainJs app, and the server platform nodeJs fastify app and apache cassandra will give the result back to the recpective user-devs-programmer.

So I will use NGINX, PM2 cluster mode with my 3 or 6 core server, Node.js, Fastify. How to use pm2 .cjs and Redies for PM2 process management in 3 or 6 core cluster mode.

The the platform server or servers manager_director of node.js app will be directing all the apps that was were will are uploaded to the server to run by distributed fashion by web workers.
The userDev working on the userDev dashboard as userDev_director will be able to only direct his own uploaded program process. 