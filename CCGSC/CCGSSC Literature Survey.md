


[[Thesis Report]]
[[Literature Survey]]
[[Literature Review Steps]]
[[Literature Review Checklist]]
[[CCGSSC Literature Survey]]
[[CCGSC Literature Review]]
[[Draft Literature Review]]





Peer-to-peer (P2P) supercomputing and grid computing projects harness the collective processing power of distributed networks to tackle complex computational tasks. These platforms enable individuals and organizations to contribute their computing resources, facilitating large-scale scientific research and data analysis. Below is an overview of notable projects and platforms in this domain:

**1. BOINC (Berkeley Open Infrastructure for Network Computing)**

BOINC is an open-source middleware system that supports volunteer computing and desktop grid computing. It allows researchers to utilize the idle processing power of personal computers worldwide for various scientific endeavors, including climate modeling, molecular biology, and astrophysics. Projects like SETI@home and Rosetta@home operate under the BOINC framework.

_Pros:_

- Supports a wide range of scientific projects.
    
- Open-source and highly customizable.
    

_Cons:_

- Relies heavily on volunteer participation, leading to variable resource availability.
    

**2. Golem Network**

Golem is a decentralized platform that enables users to rent out their computing power to others for tasks such as CGI rendering, machine learning, and scientific computing. It operates on blockchain technology, ensuring secure and transparent transactions between resource providers and requesters.

_Pros:_

- Decentralized and secure, leveraging blockchain technology.
    
- Provides a marketplace for computing resources, potentially reducing costs.
    

_Cons:_

- Still in development, with limited adoption and real-world applications.
    

**3. Folding@home**

Folding@home is a distributed computing project focused on simulating protein folding and molecular dynamics, aiding in disease research for conditions like Alzheimer's and cancer. Participants install a client program that runs simulations during idle periods on their computers. Notably, during the COVID-19 pandemic, Folding@home's computational power surpassed 1.5 exaFLOPS, making it one of the world's fastest computing systems. ([Wikipedia](https://en.wikipedia.org/wiki/Folding%40home?utm_source=chatgpt.com "Folding@home"))

_Pros:_

- Contributes directly to critical biomedical research.
    
- User-friendly client with minimal impact on daily computer use.
    

_Cons:_

- Limited to specific types of scientific research.
    

**4. Google Colab**

Google Colab is a free, cloud-based platform that allows users to write and execute Python code in a Jupyter notebook environment. It provides access to GPUs and TPUs, making it popular for machine learning, data analysis, and educational purposes.

_Pros:_

- Free access to powerful GPUs and TPUs.
    
- No setup required; runs entirely in the cloud.
    

_Cons:_

- Session durations are limited, which may not be suitable for long-running tasks.
    

**Other Online GPU/CPU Computing Platforms:**

**a. Amazon Web Services (AWS) Elastic Compute Cloud (EC2)**

AWS EC2 offers scalable computing capacity in the cloud, allowing users to run applications on virtual servers. It provides a wide range of instance types, including those optimized for GPU and CPU-intensive workloads.

_Pros:_

- Highly scalable with a global infrastructure.
    
- Flexible pricing models, including pay-as-you-go and reserved instances.
    

_Cons:_

- Costs can accumulate quickly without proper management.
    

**b. Microsoft Azure**

Azure provides a suite of cloud services, including virtual machines with GPU and CPU capabilities, catering to various computational needs such as AI, machine learning, and large-scale simulations.

_Pros:_

- Integration with other Microsoft services and tools.
    
- Comprehensive compliance and security features.
    

_Cons:_

- Complex pricing structure that may be challenging to navigate.
    

**c. IBM Cloud**

IBM Cloud offers virtual servers and bare metal servers with GPU options, supporting high-performance computing tasks. It also provides specialized services for AI and machine learning workloads.

_Pros:_

- Access to IBM's advanced AI tools and frameworks.
    
- Flexible configurations tailored to specific workloads.
    

_Cons:_

- May have a steeper learning curve for new users.
    

**Comparison and Considerations:**

When choosing a platform, consider factors such as cost, scalability, ease of use, and the specific computational requirements of your projects. Volunteer-based platforms like BOINC and Folding@home are excellent for contributing to scientific research without direct costs but may offer less control over computational tasks. In contrast, cloud-based services like AWS, Azure, and IBM Cloud provide scalable and flexible computing resources suitable for a wide range of applications but require careful cost management and technical expertise.

For a more in-depth analysis and recent developments in these platforms, consulting current journal articles and official documentation is recommended.



Here’s a compact, engineer-friendly briefing that compares today’s major volunteer/P2P and grid/marketplace compute platforms—with a quick table first, then deep-dives (architecture, data/control flow, scheduling, verification, security, pricing, and best-practice fit). Inline citations point to primary docs and peer-reviewed sources.

# Quick definitions

- #VolunteerComputing / DesktopGrid: public contributors donate idle CPU/GPU; projects handle scheduling/validation centrally (e.g., BOINC, Folding@home). ([boinc.berkeley.edu](https://boinc.berkeley.edu/grid_paper_04.pdf?utm_source=chatgpt.com "A System for Public-Resource Computing and Storage"))
    
- #DecentralizedComputeMarket: permissionless market where providers rent compute to requestors via crypto payments (e.g., Golem, iExec, Render, Akash). ([Golem Docs](https://docs.golem.network/docs/golem/overview?utm_source=chatgpt.com "Resource Sharing and Token Payments - Golem Network Guide"), [Akash Network](https://akash.network/?utm_source=chatgpt.com "Akash Network - Decentralized Compute Marketplace"), [iExec Documentation](https://docs.iex.ec/?utm_source=chatgpt.com "iExec Documentation HomePage"), [Render Network](https://rendernetwork.com/?utm_source=chatgpt.com "Render Network"))
    
- #HTC/#Grid: institutionally pooled clusters + pilot jobs (Open Science Grid) for high-throughput workloads. ([OSG](https://osg-htc.org/virtual-school-pilot-2020/materials/osg/files/osgvsp20-running-in-osg.pdf?utm_source=chatgpt.com "Running Jobs on the Open Science Grid"))
    
- #ManagedNotebooks/#CloudGPU: hosted VMs/TPUs with notebooks and SLAs (Colab, Kaggle, Paperspace, RunPod, Lambda, Vast.ai, CoreWeave, OCI). ([Google Research](https://research.google.com/colaboratory/faq.html?utm_source=chatgpt.com "Google Colab"), [Kaggle](https://www.kaggle.com/docs/notebooks?utm_source=chatgpt.com "Notebooks"), [DigitalOcean Docs](https://docs.digitalocean.com/products/paperspace/machines/details/pricing/?utm_source=chatgpt.com "Paperspace Pricing | DigitalOcean Documentation"), [Runpod](https://www.runpod.io/pricing?utm_source=chatgpt.com "Pricing | Runpod GPU cloud computing rates"), [Lambda](https://lambda.ai/service/gpu-cloud?utm_source=chatgpt.com "On-Demand GPU Cloud"), [Vast AI](https://vast.ai/pricing?utm_source=chatgpt.com "Pricing"), [CoreWeave Docs](https://docs.coreweave.com/?utm_source=chatgpt.com "CoreWeave Docs | CoreWeave"), [Oracle](https://www.oracle.com/cloud/compute/gpu/?utm_source=chatgpt.com "GPU, Virtual Machines and Bare Metal"))
    

---

# One-page comparison

|Platform|Model|Who supplies compute|Scheduling & trust|Typical workloads|Pricing & limits|Pros|Cons|
|---|---|---|---|---|---|---|---|
|**BOINC**|Volunteer desktop grid middleware|Public volunteers|Central server issues work; result replication + quorum validators ensure correctness|Embarrassingly parallel science (astro, bio, math), long tail HTC|Free to projects/users; you host project servers|Massive scale at low cost; mature stack; pull-based NAT-friendly|No SLA; heterogeneity/churn; you build/operate servers|
|**Folding@home**|Volunteer project atop BOINC-style ideas|Public volunteers|Assignment server → work servers; backup collection servers|Protein MD (CPU+GPU)|Free; project-managed|Exascale bursts (COVID-19); optimized GPU cores|Domain-specific; closed set of workloads|
|**Golem Network**|Decentralized compute marketplace|Permissionless providers running _yagna_|P2P agreements, payments in GLM; SDKs (JS/Python) for tasks|Batch tasks, rendering, ML experiments (GPU beta)|Pay-per-task in GLM; market-driven|Permissionless scale; pay only for use; browser/JS API|Verification & data trust is on you; evolving GPU support|
|**Open Science Grid (OSG)**|Federated HTC grid (pilot jobs)|Universities/labs|HTCondor pilot jobs lease idle slots across sites|HEP/omics/HTC batch jobs|Free to research communities|Proven throughput; institutional resources|Onboarding, VO policies; batch/HTC mindset|
|**Google Colab**|Managed notebook cloud (GPU/TPU)|Google|Google schedules; session quotas; ephemeral VMs|ML prototyping, teaching|Free tier; Pay-As-You-Go/Pro tiers; dynamic limits|Zero setup; TPUs; Drive integration|Timeouts; no hard guarantees; quota variability|
|**Kaggle Notebooks**|Hosted notebooks|Google|Ephemeral sessions; free GPUs on demand|ML competitions, small jobs|Free; usage policies apply|Free GPUs; data community|Limits; less control than a full VM|
|**Paperspace**|Cloud GPUs & notebooks|Provider DCs|On-demand VMs/“Gradient”|Training/inference & general GPU|Transparent pricing; free tiers in Gradient|Mature GPU catalog|Free tier constraints|
|**RunPod**|Cloud GPUs + serverless pods|Provider DCs|Per-second billing; serverless GPU|Training/inference/clusters|On-demand pricing (e.g., 4090/H100 posted)|Fast spin-up; serverless|Marketplace availability varies|
|**Lambda Cloud**|AI GPU cloud (A100/H100/B200)|Provider DCs|On-demand & reserved|Large-scale training|Public price cards (per-GPU/hr)|Dense multi-GPU nodes|Multi-GPU nodes cost mgmt|
|**Vast.ai**|GPU rental marketplace|Independent hosts|Spot/marketplace with real-time pricing|Rendering, ML|Real-time low prices|Very low cost potential|Heterogeneous hw; due diligence|
|**CoreWeave**|GPU hyperscaler|Provider DCs|Kubernetes-native|GenAI/HPC|Public pricing pages|Latest NVIDIA fleets|Enterprise-oriented contracts|
|**Akash Network**|Decentralized cloud|Independent providers|On-chain bids/deploys; marketplace|Containers/workloads, GPUs|Market prices; credits/promos|Open market; low prices|Operational maturity varies|
|**Oracle Cloud (OCI) GPUs**|Hyperscale cloud|Oracle DCs|VM/bare-metal, high-speed RDMA|AI/HPC|Price list by GPU family|RDMA + Blackwell/MI300X options|Enterprise cloud complexity|

Sources: BOINC paper & wiki; F@h docs; Golem docs; OSG docs; Colab/Kaggle docs; provider pricing/overview pages. ([boinc.berkeley.edu](https://boinc.berkeley.edu/grid_paper_04.pdf?utm_source=chatgpt.com "A System for Public-Resource Computing and Storage"), [foldingathome.org](https://foldingathome.org/faqs/fah-v7/v7-intermediate/servers/?utm_source=chatgpt.com "Servers"), [docs.foldingathome.org](https://docs.foldingathome.org/ws/?utm_source=chatgpt.com "Work Server documentation"), [Golem Docs](https://docs.golem.network/docs/golem/overview?utm_source=chatgpt.com "Resource Sharing and Token Payments - Golem Network Guide"), [OSG](https://osg-htc.org/virtual-school-pilot-2020/materials/osg/files/osgvsp20-running-in-osg.pdf?utm_source=chatgpt.com "Running Jobs on the Open Science Grid"), [Google Research](https://research.google.com/colaboratory/faq.html?utm_source=chatgpt.com "Google Colab"), [Kaggle](https://www.kaggle.com/docs/notebooks?utm_source=chatgpt.com "Notebooks"), [DigitalOcean Docs](https://docs.digitalocean.com/products/paperspace/machines/details/pricing/?utm_source=chatgpt.com "Paperspace Pricing | DigitalOcean Documentation"), [Runpod](https://www.runpod.io/pricing?utm_source=chatgpt.com "Pricing | Runpod GPU cloud computing rates"), [Lambda](https://lambda.ai/service/gpu-cloud?utm_source=chatgpt.com "On-Demand GPU Cloud"), [Vast AI](https://vast.ai/pricing?utm_source=chatgpt.com "Pricing"), [CoreWeave Docs](https://docs.coreweave.com/?utm_source=chatgpt.com "CoreWeave Docs | CoreWeave"), [Oracle](https://www.oracle.com/cloud/compute/gpu/?utm_source=chatgpt.com "GPU, Virtual Machines and Bare Metal"))

---

# Architecture & flow (deep dives)

## BOINC (Berkeley Open Infrastructure for Network Computing)

**What it is.** Open-source middleware to run volunteer/desktop-grid projects. Projects operate a _server complex_ around a relational DB; volunteers run clients that “pull” work through schedulers and exchange files via data servers. Validation uses replication and quorums; assimilators post-process canonical results. ([boinc.berkeley.edu](https://boinc.berkeley.edu/grid_paper_04.pdf?utm_source=chatgpt.com "A System for Public-Resource Computing and Storage"), [GitHub](https://github.com/BOINC/boinc/wiki/Design-documents?utm_source=chatgpt.com "Design documents · BOINC/boinc Wiki"), [IN2P3 Events Directory (Indico)](https://indico.in2p3.fr/event/147/contributions/19402/attachments/15866/19469/ACGRID_BOINC_II.pdf?utm_source=chatgpt.com "BOINC II - IN2P3 Events Directory (Indico)"))

**Control & data flow (ASCII):**

```
Volunteer Client  <----HTTP---->  Scheduling Server (RPC)
      |   upload/download files         |-> Validator (quorum)
      v                                  -> Assimilator -> DB
   Data Servers (uploads/downloads)      -> File Deleter (GC)
```

Key design points: pull-based NAT-friendly comms; server-side components (scheduler, data server, validators/assimilators) coordinate via a central DB; data uploads use certificates & size limits. ([boinc.berkeley.edu](https://boinc.berkeley.edu/grid_paper_04.pdf?utm_source=chatgpt.com "A System for Public-Resource Computing and Storage"))

**Verification.** Redundant dispatch (“initial replication”) and quorum agreement; application-specific validators handle stochastic outputs. ([GitHub](https://github.com/BOINC/boinc/wiki/JobReplication?utm_source=chatgpt.com "JobReplication · BOINC/boinc Wiki"), [Debian Wiki](https://wiki.debian.org/BOINC/ServerGuide/ResultManagement?utm_source=chatgpt.com "BOINC/ServerGuide/ResultManagement"), [CiteSeerX](https://citeseerx.ist.psu.edu/document?doi=cb4c5dbeb6c327cdb728f33e639facfbc0b73d2b&repid=rep1&type=pdf&utm_source=chatgpt.com "SimBA: a Discrete Event Simulator for Performance ..."))

**Scheduling/algorithms.** Clients attach to multiple projects; BOINC does local scheduling to keep devices busy and download in background; server matchmaking policies vary. ([CiteSeerX](https://citeseerx.ist.psu.edu/document?doi=a9216dac71332580b80b8ce262660e40ec7b7223&repid=rep1&type=pdf&utm_source=chatgpt.com "Local Scheduling for Volunteer Computing"), [boinc.berkeley.edu](https://boinc.berkeley.edu/boinc_papers/pcgrid_11/p2.pdf?utm_source=chatgpt.com "Emulating Volunteer Computing Scheduling Policies - BOINC"))

**Security.** Sandboxed apps; signed downloads; upload certs; threat is untrusted clients, mitigated by replication/quorums. ([boinc.berkeley.edu](https://boinc.berkeley.edu/grid_paper_04.pdf?utm_source=chatgpt.com "A System for Public-Resource Computing and Storage"))

**Use when / avoid when.**  
Use for embarrassingly parallel HTC where you can tolerate heterogeneity and no SLA. Avoid for stateful/interactive services or regulated data.

## Folding@home

**What it is.** A volunteer compute project specialized for molecular dynamics; burst to _>1 exaFLOPS_ in 2020 for COVID-19 work. ([foldingathome.org](https://foldingathome.org/2021/01/05/2020-in-review-and-happy-new-year-2021/?utm_source=chatgpt.com "2020 in review, and happy new year 2021!"), [NVIDIA Blog](https://blogs.nvidia.com/blog/foldingathome-exaflop-coronavirus/?utm_source=chatgpt.com "Folding@home Assembles an Exaflop to Fight COVID-19"))

**Architecture.** Clients contact an _Assignment Server_ (load balancer) → get a _Work Server_ for WUs; results return to the same WS, with _Collection Servers_ as backup. GPU-optimized cores and analysis pipelines. ([foldingathome.org](https://foldingathome.org/faqs/fah-v7/v7-intermediate/servers/?utm_source=chatgpt.com "Servers"), [docs.foldingathome.org](https://docs.foldingathome.org/ws/?utm_source=chatgpt.com "Work Server documentation"))

**Peer-review.** Long record in literature reviewing architecture & scientific output. ([ScienceDirect](https://www.sciencedirect.com/science/article/pii/S0006349523002011?utm_source=chatgpt.com "Folding@home: Achievements from over 20 years of ..."), [CiteSeerX](https://citeseerx.ist.psu.edu/document?doi=b5b13d2fb6590f37de4887ab2e22bad1f5a92b6c&repid=rep1&type=pdf&utm_source=chatgpt.com "Folding@home: Lessons From Eight Years of Volunteer ..."))

**Use when / avoid when.**  
Use to contribute to biomedical MD; not a general-purpose compute marketplace.

## Golem Network

**What it is.** A P2P compute marketplace; nodes run **yagna** and act as _providers_ or _requestors_; tasks submitted via Python/JS SDKs; payments in GLM. GPU provider beta ongoing. ([Golem Docs](https://docs.golem.network/docs/golem/overview?utm_source=chatgpt.com "Resource Sharing and Token Payments - Golem Network Guide"), [golem.network](https://golem.network/?utm_source=chatgpt.com "Golem Network"))

**Flow & roles (ASCII):**

```
Requestor App (JS/Python SDK)
   | negotiate offers / price, sign agreements
   v
yagna (requestor) <---- P2P ----> yagna (providers N)
   |                        |
   |<-- results, invoices --|
   v
Payment driver (GLM) on chain
```

**Hello-world (JS SDK) snippet:**

```javascript
import { TaskExecutor } from "@golem-sdk/golem-js";
const exec = await TaskExecutor.create();
const results = await exec.run(async (ctx) => await ctx.run('echo "hello"'));
await exec.shutdown();
```

(From Golem JS examples.) ([Golem Docs](https://docs.golem.network/docs/creators/javascript/examples/executing-tasks?utm_source=chatgpt.com "Executing Tasks with Golem's JavaScript API"))

**Trust & verification.** Provider–requestor agreements; payment drivers; task verification largely application-specific (replication, checksums, probabilistic tests). (See Golem overview + SDK docs.) ([Golem Docs](https://docs.golem.network/docs/golem/overview?utm_source=chatgpt.com "Resource Sharing and Token Payments - Golem Network Guide"))

**Use when / avoid when.**  
Use for batched jobs where decentralization/cost alignment matters; avoid for strict SLAs/regulatory data until you add verification/TEEs.

## Open Science Grid (OSG)

**What it is.** A federated HTC grid pooling institutional clusters. _Pilot jobs_ land on sites via compute entrypoints; pilots fetch and run end-user payloads (HTCondor). ([OSG](https://osg-htc.org/virtual-school-pilot-2020/materials/osg/files/osgvsp20-running-in-osg.pdf?utm_source=chatgpt.com "Running Jobs on the Open Science Grid"))

**Flow (ASCII):**

```
User submits to VO -> Pilot Factory -> Pilots to Site CE
Pilot starts execute daemon -> joins pool -> payload jobs match/run
```

Great for universities/VOs with HTC; not a GPU “on-demand” marketplace.

## Managed notebooks & GPU clouds

### Google Colab

Hosted Jupyter with optional GPU/TPU; dynamic usage limits; paid tiers (Pay-As-You-Go / Pro). ([Google Research](https://research.google.com/colaboratory/faq.html?utm_source=chatgpt.com "Google Colab"), [Google Colab](https://colab.research.google.com/signup?utm_source=chatgpt.com "Colab Paid Services Pricing"))  
Check GPU in a notebook:

```python
!nvidia-smi
```

Limits/quotas are intentionally unpublished and vary. ([Stack Overflow](https://stackoverflow.com/questions/61126851/how-can-i-use-gpu-on-google-colab-after-exceeding-usage-limit?utm_source=chatgpt.com "How can I use GPU on Google Colab after exceeding ..."))

### Kaggle Notebooks

Enable GPU from _Settings → Accelerator_; free usage policies. ([Kaggle](https://www.kaggle.com/docs/notebooks?utm_source=chatgpt.com "Notebooks"))

### Paperspace / RunPod / Lambda / Vast.ai / CoreWeave / OCI

- Paperspace pricing & Gradient tiers; free GPU community notebooks. ([DigitalOcean Docs](https://docs.digitalocean.com/products/paperspace/machines/details/pricing/?utm_source=chatgpt.com "Paperspace Pricing | DigitalOcean Documentation"), [Paperspace by DigitalOcean Blog](https://blog.paperspace.com/paperspace-launches-gradient-community-notebooks/?utm_source=chatgpt.com "Easily Run ML Notebooks on Free GPUs - Paperspace Blog"))
    
- RunPod on-demand and serverless GPU pricing. ([Runpod](https://www.runpod.io/pricing?utm_source=chatgpt.com "Pricing | Runpod GPU cloud computing rates"), [Runpod Documentation](https://docs.runpod.io/serverless/pricing?utm_source=chatgpt.com "Pricing"))
    
- Lambda Cloud public per-GPU pricing (A100/H100/B200). ([Lambda](https://lambda.ai/service/gpu-cloud?utm_source=chatgpt.com "On-Demand GPU Cloud"))
    
- Vast.ai marketplace + docs. ([Vast AI](https://vast.ai/pricing?utm_source=chatgpt.com "Pricing"), [docs.vast.ai](https://docs.vast.ai/?utm_source=chatgpt.com "Introduction - Guides - Vast AI"))
    
- CoreWeave pricing & docs (K8s-native GPU cloud). ([CoreWeave](https://www.coreweave.com/pricing?utm_source=chatgpt.com "GPU Cloud Pricing"), [CoreWeave Docs](https://docs.coreweave.com/docs/pricing/pricing-instances?utm_source=chatgpt.com "Instance Pricing"))
    
- Oracle Cloud (OCI) GPU shapes/prices incl. MI300X/Blackwell families. ([Oracle](https://www.oracle.com/cloud/compute/gpu/?utm_source=chatgpt.com "GPU, Virtual Machines and Bare Metal"))
    

### Other decentralized markets (related)

- **iExec** (PoCo verifiable off-chain compute; TEEs/SGX options). ([iExec](https://www.iex.ec/academy/poco-documentation?utm_source=chatgpt.com "PoCo - Technical Documentation"), [GitHub](https://github.com/iExecBlockchainComputing/knowledge-base?utm_source=chatgpt.com "iExec Knowledge Base"))
    
- **Render Network (RNDR)** (decentralized GPU rendering). ([Render Network](https://rendernetwork.com/?utm_source=chatgpt.com "Render Network"), [Render Network Knowledge Base](https://know.rendernetwork.com/?utm_source=chatgpt.com "Render Network Knowledge Base"))
    
- **Akash Network** (on-chain bid/ask for containers/GPUs). ([Akash Network](https://akash.network/?utm_source=chatgpt.com "Akash Network - Decentralized Compute Marketplace"))
    

---

# Technical considerations (cross-cut)

**Data & control planes**

- BOINC/F@h: pull-based RPC to schedulers; HTTP for file transfer; validators/assimilators on server; canonical result via quorum. ([boinc.berkeley.edu](https://boinc.berkeley.edu/grid_paper_04.pdf?utm_source=chatgpt.com "A System for Public-Resource Computing and Storage"))
    
- OSG: pilot jobs create “ephemeral slots”; payload jobs match later. ([OSG](https://osg-htc.org/virtual-school-pilot-2020/materials/osg/files/osgvsp20-running-in-osg.pdf?utm_source=chatgpt.com "Running Jobs on the Open Science Grid"))
    
- Golem/iExec/Akash/Render: market negotiation + signed agreements; off-chain execution; on-chain payments; verification/performance left to app/TEEs (iExec PoCo). ([Golem Docs](https://docs.golem.network/docs/golem/overview?utm_source=chatgpt.com "Resource Sharing and Token Payments - Golem Network Guide"), [iExec](https://www.iex.ec/academy/poco-documentation?utm_source=chatgpt.com "PoCo - Technical Documentation"))
    

**Load-balancing, chunking & replication**

- BOINC: split workunits; initial replication >= min_quorum; validators decide canonical; file deleter GC. ([GitHub](https://github.com/BOINC/boinc/wiki/JobReplication?utm_source=chatgpt.com "JobReplication · BOINC/boinc Wiki"), [IN2P3 Events Directory (Indico)](https://indico.in2p3.fr/event/147/contributions/19402/attachments/15866/19469/ACGRID_BOINC_II.pdf?utm_source=chatgpt.com "BOINC II - IN2P3 Events Directory (Indico)"))
    
- OSG: matchmaking + pilot revocation; design for preemption. ([OSG](https://osg-htc.org/virtual-school-pilot-2020/materials/osg/files/osgvsp20-running-in-osg.pdf?utm_source=chatgpt.com "Running Jobs on the Open Science Grid"))
    
- Decentralized markets: you implement chunking; use redundancy/probabilistic verification.
    

**Security, privacy, encryption**

- BOINC/F@h: signed downloads; upload certs; no inherent confidentiality once code/data reach volunteers; avoid sensitive data unless pre-processed. ([boinc.berkeley.edu](https://boinc.berkeley.edu/grid_paper_04.pdf?utm_source=chatgpt.com "A System for Public-Resource Computing and Storage"))
    
- iExec: PoCo + TEEs (SGX) can protect data/code & produce proofs. ([GitHub](https://github.com/iExecBlockchainComputing/knowledge-base?utm_source=chatgpt.com "iExec Knowledge Base"))
    
- Colab/Kaggle/Clouds: rely on cloud isolation; encrypt at rest/in transit; check data residency & org policies.
    

**DBMS and storage**

- BOINC server centered on a relational DB (apps/platforms/versions/workunits/results/accounts/teams). ([boinc.berkeley.edu](https://boinc.berkeley.edu/grid_paper_04.pdf?utm_source=chatgpt.com "A System for Public-Resource Computing and Storage"))
    
- OSG/Clouds: you bring your DB object store; staging/scratch policies apply. ([OSG](https://osg-htc.org/docs/worker-node/using-wn/?utm_source=chatgpt.com "Worker Node Overview - OSG Site Documentation"))
    

**Networking**

- BOINC pull model handles NAT/firewalls; data via HTTP; large downloads/uploads chunked. ([boinc.berkeley.edu](https://boinc.berkeley.edu/grid_paper_04.pdf?utm_source=chatgpt.com "A System for Public-Resource Computing and Storage"))
    
- OSG requires site/network configuration for pilots and worker nodes. ([OSG](https://osg-htc.org/docs/site-planning/?utm_source=chatgpt.com "Site Planning - OSG Site Documentation"))
    

**Quality/performance**

- F@h demonstrated exascale via crowdsourcing during COVID-19; MD GPU kernels historically delivered large speedups. ([foldingathome.org](https://foldingathome.org/2021/01/05/2020-in-review-and-happy-new-year-2021/?utm_source=chatgpt.com "2020 in review, and happy new year 2021!"), [PMC](https://pmc.ncbi.nlm.nih.gov/articles/PMC2934899/?utm_source=chatgpt.com "GPU-Accelerated Molecular Modeling Coming Of Age - PMC"))
    
- Cloud GPUs: choose instance family (A100/H100/B200/MI300X) and interconnect (NVLink/RDMA) for multi-GPU scaling. ([Oracle](https://www.oracle.com/cloud/compute/gpu/?utm_source=chatgpt.com "GPU, Virtual Machines and Bare Metal"))
    

---

# When to use what (decision guide)

- **You want the lowest cost at planetary scale for simple HTC tasks** → BOINC project (you operate servers) or OSG (if you’re an academic VO). ([boinc.berkeley.edu](https://boinc.berkeley.edu/grid_paper_04.pdf?utm_source=chatgpt.com "A System for Public-Resource Computing and Storage"), [OSG](https://osg-htc.org/virtual-school-pilot-2020/materials/osg/files/osgvsp20-running-in-osg.pdf?utm_source=chatgpt.com "Running Jobs on the Open Science Grid"))
    
- **You want general compute without running infra, and can handle variable quotas** → Google Colab/Kaggle for prototyping/teaching; upgrade to Paperspace/RunPod/Lambda/CoreWeave/OCI for production. ([Google Research](https://research.google.com/colaboratory/faq.html?utm_source=chatgpt.com "Google Colab"), [Kaggle](https://www.kaggle.com/docs/notebooks?utm_source=chatgpt.com "Notebooks"))
    
- **You want a permissionless market for cost arbitrage** → Golem/Vast.ai/Akash/Render (fit batch workloads; design your own verification). ([Golem Docs](https://docs.golem.network/docs/golem/overview?utm_source=chatgpt.com "Resource Sharing and Token Payments - Golem Network Guide"), [Vast AI](https://vast.ai/pricing?utm_source=chatgpt.com "Pricing"), [Akash Network](https://akash.network/?utm_source=chatgpt.com "Akash Network - Decentralized Compute Marketplace"))
    
- **You want to contribute to biomedicine** → Folding@home. ([foldingathome.org](https://foldingathome.org/faqs/fah-v7/v7-intermediate/servers/?utm_source=chatgpt.com "Servers"))
    

---

# Best practices

- **Verification**: replicate shards and compare hashes/statistics; embed known-answer tests; or use TEEs (e.g., iExec + SGX) when privacy is required. ([GitHub](https://github.com/iExecBlockchainComputing/knowledge-base?utm_source=chatgpt.com "iExec Knowledge Base"))
    
- **Chunking**: keep workunits 5–60 minutes on commodity hosts; reduce stragglers by adaptive granularity (BOINC ops guidance). ([boinc.berkeley.edu](https://boinc.berkeley.edu/grid_paper_04.pdf?utm_source=chatgpt.com "A System for Public-Resource Computing and Storage"))
    
- **Resilience**: design for preemption (OSG pilots, cloud preemptible); idempotent work; resumable uploads. ([OSG](https://osg-htc.org/virtual-school-pilot-2020/materials/osg/files/osgvsp20-running-in-osg.pdf?utm_source=chatgpt.com "Running Jobs on the Open Science Grid"))
    
- **Data hygiene**: encrypt, anonymize, or synthesize datasets before volunteer/market execution; avoid regulated PII/PHI unless you control the environment.
    
- **Cost**: for training runs, profile on free/cheap tiers but lock-in reservations (Lambda/CoreWeave/OCI) for long jobs; marketplace spot instances (Vast.ai) for experiments with checkpointing. ([Lambda](https://lambda.ai/service/gpu-cloud?utm_source=chatgpt.com "On-Demand GPU Cloud"), [CoreWeave Docs](https://docs.coreweave.com/docs/pricing/pricing-instances?utm_source=chatgpt.com "Instance Pricing"), [Oracle](https://www.oracle.com/cloud/price-list/?utm_source=chatgpt.com "OCI Price List"))
    

---

# Trends & future directions

- **Decentralized GPU markets** (Golem/Render/Akash) expanding GPU supply; verification/attestation (TEEs/ZK) is the main active R&D area. ([Akash Network](https://akash.network/?utm_source=chatgpt.com "Akash Network - Decentralized Compute Marketplace"), [Render Network Knowledge Base](https://know.rendernetwork.com/?utm_source=chatgpt.com "Render Network Knowledge Base"))
    
- **Serverless GPUs** (RunPod et al.) and **K8s-native GPU clouds** (CoreWeave) simplify bursty inference at scale. ([Runpod Documentation](https://docs.runpod.io/serverless/pricing?utm_source=chatgpt.com "Pricing"), [CoreWeave Docs](https://docs.coreweave.com/?utm_source=chatgpt.com "CoreWeave Docs | CoreWeave"))
    
- **Volunteer HTC as exascale burst buffer** (F@h’s COVID response). ([foldingathome.org](https://foldingathome.org/2021/01/05/2020-in-review-and-happy-new-year-2021/?utm_source=chatgpt.com "2020 in review, and happy new year 2021!"))
    

---

# Compliance & governance (quick checklist)

- **Data residency / GDPR**: volunteer/market nodes are global—avoid sensitive data or use TEEs.
    
- **Crypto/KYC/AML**: token payouts/fees (GLM, RNDR, AKT) may trigger compliance. ([Golem Docs](https://docs.golem.network/docs/golem/overview?utm_source=chatgpt.com "Resource Sharing and Token Payments - Golem Network Guide"), [Render Network](https://rendernetwork.com/?utm_source=chatgpt.com "Render Network"), [Akash Network](https://akash.network/?utm_source=chatgpt.com "Akash Network - Decentralized Compute Marketplace"))
    
- **Grant/VO policies**: OSG/academic grids require VO membership and acceptable use. ([OSG](https://osg-htc.org/docs/resource-sharing/overview/?utm_source=chatgpt.com "Compute Resource Sharing Overview - Open Science Grid"))
    

---

## References (selected)

- **BOINC**: Anderson, _A System for Public-Resource Computing and Storage_ (GRID’04); BOINC server/data architecture & replication docs. ([boinc.berkeley.edu](https://boinc.berkeley.edu/grid_paper_04.pdf?utm_source=chatgpt.com "A System for Public-Resource Computing and Storage"), [GitHub](https://github.com/BOINC/boinc/wiki/JobReplication?utm_source=chatgpt.com "JobReplication · BOINC/boinc Wiki"))
    
- **Folding@home**: Server architecture/AS/WS/CS docs; 2023 Biophysical Journal review; 2020 exascale announcements. ([foldingathome.org](https://foldingathome.org/faqs/fah-v7/v7-intermediate/servers/?utm_source=chatgpt.com "Servers"), [docs.foldingathome.org](https://docs.foldingathome.org/ws/?utm_source=chatgpt.com "Work Server documentation"), [ScienceDirect](https://www.sciencedirect.com/science/article/pii/S0006349523002011?utm_source=chatgpt.com "Folding@home: Achievements from over 20 years of ..."))
    
- **Golem**: Network overview, yagna installation, JS Task API. ([Golem Docs](https://docs.golem.network/docs/golem/overview?utm_source=chatgpt.com "Resource Sharing and Token Payments - Golem Network Guide"))
    
- **OSG**: Pilot jobs and CE/worker-node docs. ([OSG](https://osg-htc.org/virtual-school-pilot-2020/materials/osg/files/osgvsp20-running-in-osg.pdf?utm_source=chatgpt.com "Running Jobs on the Open Science Grid"))
    
- **Colab**: FAQ and pricing pages; usage-limit statements. ([Google Research](https://research.google.com/colaboratory/faq.html?utm_source=chatgpt.com "Google Colab"), [Google Colab](https://colab.research.google.com/signup?utm_source=chatgpt.com "Colab Paid Services Pricing"), [Stack Overflow](https://stackoverflow.com/questions/61126851/how-can-i-use-gpu-on-google-colab-after-exceeding-usage-limit?utm_source=chatgpt.com "How can I use GPU on Google Colab after exceeding ..."))
    
- **Kaggle**: Notebooks GPU docs. ([Kaggle](https://www.kaggle.com/docs/notebooks?utm_source=chatgpt.com "Notebooks"))
    
- **Cloud GPU providers**: Paperspace (docs/blog), RunPod (pricing), Lambda (pricing), Vast.ai (pricing/docs), CoreWeave (pricing/docs), Oracle Cloud GPU price/shapes. ([DigitalOcean Docs](https://docs.digitalocean.com/products/paperspace/machines/details/pricing/?utm_source=chatgpt.com "Paperspace Pricing | DigitalOcean Documentation"), [Paperspace by DigitalOcean Blog](https://blog.paperspace.com/paperspace-launches-gradient-community-notebooks/?utm_source=chatgpt.com "Easily Run ML Notebooks on Free GPUs - Paperspace Blog"), [Runpod](https://www.runpod.io/pricing?utm_source=chatgpt.com "Pricing | Runpod GPU cloud computing rates"), [Runpod Documentation](https://docs.runpod.io/serverless/pricing?utm_source=chatgpt.com "Pricing"), [Lambda](https://lambda.ai/service/gpu-cloud?utm_source=chatgpt.com "On-Demand GPU Cloud"), [Vast AI](https://vast.ai/pricing?utm_source=chatgpt.com "Pricing"), [docs.vast.ai](https://docs.vast.ai/?utm_source=chatgpt.com "Introduction - Guides - Vast AI"), [CoreWeave](https://www.coreweave.com/pricing?utm_source=chatgpt.com "GPU Cloud Pricing"), [CoreWeave Docs](https://docs.coreweave.com/docs/pricing/pricing-instances?utm_source=chatgpt.com "Instance Pricing"), [Oracle](https://www.oracle.com/cloud/compute/gpu/?utm_source=chatgpt.com "GPU, Virtual Machines and Bare Metal"))
    

---

#tags  
#VolunteerComputing #DesktopGrid #BOINC #FoldingAtHome #DecentralizedCompute #Golem #iExec #Akash #Render #OpenScienceGrid #HTC #PilotJobs #Colab #Kaggle #Paperspace #RunPod #Lambda #VastAI #CoreWeave #OCI #GPU #TPU #NVLink #RDMA #Quorum #Replication #TEEs #SGX #PoCo #ServerlessGPU #MarketplacePricing #DataResidency #SLA