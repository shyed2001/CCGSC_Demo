
[[Proposal for Thesis Research]]
[[Related Resources CCGSC_System_Design]]
[[Structure of Problem Statement and Research Question]]
[[CCGSC_Research_Proposal]]
[[CCGSC_Problem_Statement_and_Reseaarch_Question]]
[[Research Gap]]
[[Research Question]]
[[Literature Survey]]
[[Academic Writing]]
[[Thesis Report]]


---
Draft


# Crowd Cloud Grid Super-Computing System (CCGSC): A Hierarchical, Decentralized Platform for Democratizing High-Performance Computing

In the evolving landscape of distributed computing, the proposed Crowd Cloud Grid Super-Computing System (CCGSC) emerges as a innovative hierarchical platform that leverages virtual machines (VMs), containers, sandboxes, and browser-based resources across Dew, Cluster, Grid, and Cloud layers. This system addresses the limitations of traditional high-performance computing (HPC) and cloud platforms by crowdsourcing idle resources globally, enabling resilient, cost-effective supercomputing for probabilistic and massively parallel workloads. CCGSC integrates dynamic resource allocation, P2P torrent protocols for task and data sharing, and lightweight blockchain for security, allowing devices from mobiles to servers to contribute while serving personal or business needs. This essay consolidates an analysis of CCGSC's design, comparisons with alternatives, research gaps and framework, and the feasibility of browser-based worker nodes for handling ultra-massive parallel, concurrent, and multi-threaded tasks.

## Overview and Core Design of CCGSC
CCGSC is structured in layers to optimize heterogeneous devices: the Dew layer supports low-power, intermittent nodes (e.g., mobiles with offline processing via sandboxes); the Cluster layer manages dynamic VM orchestration for compute-intensive tasks; the Grid layer coordinates high-availability servers; and the Cloud/Web layer oversees global management. Resources like CPU, GPU, RAM, and storage are pooled dynamically through head nodes, using heartbeats and FIFO queues for allocation. This enables task offloading for probabilistic applications, such as Monte Carlo simulations in drug discovery or AI training, where subtasks can run independently on crowd-sourced nodes. Novel elements include full OS VMs that function as personal computers while contributing compute power, isolated via tools like Hyper-V or Docker, and P2P integration for secure, decentralized sharing without heavy overhead.

## Comparisons with Alternatives
CCGSC stands out against volunteer networks like BOINC, Golem, Akash, SONM, iExec, and Ankr, which primarily harness idle CPUs for scientific or blockchain tasks but lack CCGSC's multi-layer resilience and full VM support. For instance, BOINC excels in simplicity for volunteer computing, but CCGSC's Dew layer adds offline capabilities, and its resource pooling (e.g., GPU/RAM over P2P) broadens applicability, though at higher VM management complexity. Improvements could include Golem-like tokenomics for incentives while retaining lightweight blockchain for efficiency.

Compared to managed platforms like Google Colab, Kaggle, or Azure Notebooks—cloud-hosted Jupyter environments for ML with limited free GPUs—CCGSC offers full OS VMs for any application, not just notebooks, and crowd-sourced resources to cut costs, albeit without Colab's seamless integrations like Google Drive. Against major clouds (AWS, Azure, GCP), CCGSC decentralizes pay-per-use models, optimizing global idle resources (e.g., 50-70% of PCs worldwide per IDC reports) via incentives and offline support, with potential hybrid bursting to clouds for reliability.

Versus traditional HPC supercomputers (e.g., Summit or Fugaku using MPI), CCGSC reduces massive CapEx/OpEx by crowdsourcing VMs, though it trades low-latency interconnects for network variability. This makes CCGSC ideal for probabilistic tasks on variable nodes, filling gaps where HPC ignores crowdsourcing and clouds overlook incentives.

## Research Gaps, Framework, and Novelty
Pursuing CCGSC research is justified by its potential to democratize HPC amid surging AI/ML demands, bridging elite, expensive systems with underutilized global resources. Key gaps include: similar systems like BOINC/Golem limiting to CPU-only without GPU/RAM pooling or full VMs; clouds ignoring P2P incentives, wasting 70-80% resources; and HPC's high energy/cost without decentralization. CCGSC addresses these via AI-driven discovery (e.g., ML predicting node availability) and blockchain for trustless auth, potentially slashing CapEx by 70-90% through dynamic pooling.

The research aim is to design and evaluate CCGSC as a decentralized platform for affordable, resilient HPC. Its purpose: enable secure sharing on heterogeneous devices, supporting offline/parallel tasks to cut costs. Central question: How does CCGSC's P2P/blockchain hierarchy improve utilization over traditional systems? Problem statement: Existing platforms underuse idle resources while being costly/centralized, ill-suited for probabilistic workloads on volunteers.

Contributions include: (1) resilient multi-layer architecture; (2) 80% cost reductions via crowdsourcing; (3) enabling fields like drug discovery on low-power devices; (4) optimizing probabilistic tasks (e.g., independent simulations via Dew). Novelty lies in Dew offline + full OS VMs with P2P/blockchain, solving intermittency (offline sync), security (consensus), scalability (hierarchical MPI-like parallelism), and waste (recycling idle CPUs/GPUs/RAM). Prototype via Docker/Podman + WebAssembly, tested on LAN/WAN for throughput/latency, validates this.

## Browser-Based Worker Nodes for Massive Workloads
Extending CCGSC, browsers or clients can serve as worker nodes across platforms, creating a crowd-sourced supercomputer via WebAssembly (Wasm) for near-native execution, Web Workers for concurrency, and WebSockets/WebRTC for P2P clustering. By 2025, Wasm advancements support multithreading and WebGPU for accelerated parallelism, making browsers viable for ultra-massive workloads.

For embarrassingly parallel tasks (ultra super/high massive, e.g., Monte Carlo or raytracing), browsers excel: independent chunks distribute via P2P, with Wasm compiling C++ code and Workers parallelizing across tabs/cores. Parallel/concurrent variants use SharedArrayBuffer/Atomics for synchronization, supporting up to 50 practical Workers per tab. Multi-threaded-concurrent-parallel leverages Wasm threads (pthread) + WebSockets, ideal for Dew (local processing, online sync).

Examples include 2025's Bless Browser Node (Chrome extension for decentralized AI compute, pooling global resources for points) and VoltixAI (CPU tasks across tabs). Desktop nodes use Electron/headless browsers; mobiles as Dew helpers with IndexedDB storage. Build with Emscripten for Wasm, Comlink for communication, and IPFS for decentralized distribution.

Pros: Zero-install, cross-platform scalability to millions (e.g., 4M+ in Bless), low-cost crowdsourcing, offline resilience. Cons: Browser caps (50% CPU, sandboxes), latency for tight tasks (favor embarrassingly parallel), privacy risks (mitigated by blockchain).

## Conclusion
CCGSC represents a paradigm shift toward sustainable, accessible supercomputing, consolidating hierarchical design, P2P/blockchain novelty, and browser integration to solve high costs, waste, and exclusivity in HPC. By enabling full VMs as personal tools while crowdsourcing for probabilistic workloads, it fills critical gaps, with browser nodes amplifying reach for massive parallelism. Future prototypes and benchmarks will quantify its impact, potentially transforming fields from AI to scientific simulations.








---


A. Application Details

Application ID: 
Reference Code:
Selected Grant: 
 Title Of Proposed Research Project: ![[Title and Keywords Crowd Grid Super Computing Proposed CCGSC]]
   [[Abstract and Title Cloud-crowd Grid Super-Computing]]
 
 ## Keywords:  ![[Title and Keywords Crowd Grid Super Computing Proposed CCGSC#Keywords^]]

B. Details of Project Leaders

Name:
Nationality:
ID: 
Position:
University:
Faculty/Centre: 
Unit: Department of Computer Science & Engineering
Office Phone No. 
Mobile phone No. 
Email Address: 
Date of first appointment with this University: 
Type of Service (Permanent/Contract) : 

C. Research Information

## Research Title
 [[Title and Keywords Crowd Grid Super Computing Proposed CCGSC]]
  [[Abstract and Title Cloud-crowd Grid Super-Computing]]



C. Research Information
Research Cluster 
Sub Research Cluster
Technology and Engineering Electrical and Electronic
Researcher Cluster
Research Cluster Sub Research Cluster
Technology and Engineering Electrical and Electronic
Socio Economic Objective (SEO)
Category Group

## Executive Summary of Research Proposal




## Detail Planning:

#### Research background


## (a) Detailed proposal of research project:
1. Research background including summary of previous research related to the prototype development.



## Problem Statement

3. Description of prototype including its originality, innovativeness, special features and indicate strategies to be used that will make
the product competitive.

4. Description of the state of the art including information on similar product available in the market and existing market size.

5.  5. Describe how the developed prototype can contribute to wealth creation, enhance quality of life and create or consolidate new
	industries.

6. If development cost for the prototype is more than the PRGS ceiling, state how you plan to obtain the remaining fund.

7. Provide the activities and potential funding sources to bring the developed prototype to commercialization.
		

			
[[CCGSC_Problem_Statement_and_Reseaarch_Question]]



## (b) Objective (s) of the Research
	
This work aimed to achieve the following objectives:

1-    To come up with a new framework for assisting elderly tracking and fall detection

2-    To propose a new approach for determining the presence and location of a person

3-    To make recommendation based on the simulation and experimental result output

## (c) Methodology:


1. Description of Methodology


2. Flow Chart of Research Activities

3. Research Activities


4. Milestones and Dates


Gantt Chart of Research Activities with Milestones


(d) Expected Results/Benefit



D. Access to Equipment & Material


E. Budget


F. Declaration
1. [ ] All information stated here are accurate, KPT and IPT has right to reject or to cancel the offer without prior notice if there is any
        inaccurate information given.
2. [ ] Application of this research is presented for the Prototype Development Research Grant Scheme (PRGS).
3. [ ] Application of this research is also presented for the other research grant/s (grant's name and total amount)
4. [ ] Application of this research is subject to Ethical Committee approval.
5. [ ] Project Leader have received approved Prototype Development Research Grant Scheme (PRGS) project.



Name: Shyed Shahriar Housaini
Date: 15/07/2025


