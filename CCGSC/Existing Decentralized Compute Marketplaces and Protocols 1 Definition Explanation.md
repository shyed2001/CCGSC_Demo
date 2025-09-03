

[[Existing Decentralized Compute Marketplaces and Protocols 2 - Comparative Analysis of Top Volunteer and Decentralized Computing Frameworks]]




### CCGSC System Analysis and Research Guidance

Based on the provided document, which outlines your proposed CCGSC (Crowd Cloud Grid Super-Computing System)—a hierarchical, decentralized platform leveraging VMs, containers, sandboxes, and browser-based resources across Dew, Cluster, Grid, and Cloud layers for distributed computing—I'll address your queries concisely. I'll explain key concepts where they add value, then provide research topics as requested.

#### 1. Comparisons: CCGSC vs. Alternatives

- **CCGSC vs. BOINC, Golem, Akash, SONM, iExec, Ankr**: These are volunteer/decentralized computing networks (e.g., BOINC for scientific tasks via idle CPUs; Golem/Akash for blockchain-based resource marketplaces). CCGSC differentiates by integrating hierarchical layers (Dew for offline/low-power devices, Cluster/Grid for dynamic VM orchestration) with full OS VMs, allowing seamless personal/business use alongside computing contributions. Pros: CCGSC offers better offline resilience (via Dew) and resource pooling (CPU/GPU/RAM/storage over P2P). Cons: Higher complexity in VM management vs. BOINC's simplicity. Improvements: Add tokenomics like Golem for incentives, but use lightweight blockchain for security (as you propose, unlike most which rely on heavy chains).
- **CCGSC vs. Proposed CCGSC Platform**: Your proposal emphasizes novelty in hybrid VM/container/browser sandboxes with P2P torrent protocols for data/task sharing and lightweight blockchain for auth/security. It's an evolution: proposed version adds dynamic resource allocation via head nodes, making it more adaptive than static grids.
- **CCGSC vs. Google Colab/Similar (Kaggle, Binder, Azure Notebooks)**: Colab et al. are managed, cloud-hosted Jupyter environments for ML/data science, with free/limited GPUs but no offline support or user-owned VMs. CCGSC enables full OS VMs for any app (not just notebooks), with crowd-sourced resources. Pros: CCGSC reduces costs via P2P; Colab is easier for beginners. Gaps: CCGSC lacks Colab's seamless integration with Google Drive/Github.
- **CCGSC vs. Other Cloud Platforms (AWS, Azure, GCP)**: Clouds offer scalable VMs (e.g., AWS EC2) but are centralized, pay-per-use, with no crowd/volunteer aspect. CCGSC is decentralized, incentive-based (rewards/points), and supports offline Dew layers. Pros: CCGSC optimizes idle resources globally; clouds guarantee uptime/SLAs. Improvements: Integrate CCGSC with clouds for hybrid bursting (e.g., fall back to AWS when crowd resources are low).
- **CCGSC vs. Traditional HPC Systems (Supercomputers like Summit, Fugaku)**: HPC uses dedicated clusters (e.g., MPI for message passing) for massive parallelism but requires huge CapEx/OpEx, no crowd integration. CCGSC crowdsources via VMs, reducing costs (e.g., via P2P for MPI-like tasks). Pros: CCGSC is accessible/affordable; HPC is faster/reliable for exascale. Gaps: CCGSC's network latency vs. HPC's low-latency interconnects (e.g., InfiniBand).

**Why Pursue CCGSC Research?** It fills gaps in democratizing HPC: traditional systems are elite/expensive; alternatives lack full VM flexibility or offline resilience. Novelty: P2P torrent + lightweight blockchain for secure, dynamic resource sharing in a multi-layer hierarchy, enabling probabilistic tasks (e.g., Monte Carlo) on heterogeneous devices.

#### 2. Research Gaps and Improvements

- **CCGSC vs. Similar Systems**: Gaps: BOINC/Golem focus on CPU-only; lack GPU/RAM pooling or full OS VMs. Improvements: CCGSC's Dew layer for intermittent connectivity; add AI-driven resource discovery (e.g., ML for predicting node availability).
- **CCGSC vs. All Other Cloud Systems**: Gaps: Clouds ignore idle global resources; no P2P incentives. Improvements: CCGSC's blockchain for trustless auth; dynamic allocation reduces waste (e.g., 70-80% idle cloud resources per studies).
- **CCGSC vs. Traditional HPC**: Gaps: HPC ignores crowdsourcing; high energy/cost. Improvements: CCGSC lowers barriers (e.g., via browser sandboxes); probabilistic tasks suit CCGSC's variable nodes.

**Resource Pooling/Discovery/Allocation**: CCGSC uses continuous monitoring by cloud/master nodes (e.g., via heartbeats/pings as in your plan). Discovery via P2P broadcasts; allocation delegated to head nodes based on task needs (e.g., FIFO queues). This is novel vs. centralized clouds.

#### 3. Research Framework for Your Thesis

- **Research Aim**: To design and evaluate CCGSC as a decentralized, multi-layer platform that crowdsources computing resources via VMs/containers for affordable, resilient HPC, addressing gaps in accessibility and resource efficiency.
- **Research Purpose**: Bridge the divide between expensive HPC/clouds and volunteer networks by enabling dynamic, secure resource sharing on heterogeneous devices, reducing CapEx/OpEx while supporting offline/parallel tasks.
- **Research Question**: How can a hierarchical CCGSC platform, using P2P protocols and lightweight blockchain, improve resource utilization and task offloading compared to traditional HPC and cloud systems?
- **Problem Statement**: Current HPC/cloud platforms are costly, centralized, and underutilize global idle resources (e.g., 50-70% idle PCs worldwide per IDC reports), while volunteer systems lack VM flexibility and security for complex, probabilistic workloads.
- **Significant Contributions**: (1) Novel multi-layer architecture for resilient computing; (2) Reduced costs (e.g., 80% via crowdsourcing); (3) Enables applications in fields like drug discovery/ML on low-power devices; (4) Probabilistic task optimization (e.g., Monte Carlo via Dew offline).
- **WHY (Thesis Research)**: Democratizes supercomputing amid rising AI/ML demands; fills gaps in sustainable, accessible HPC.
- **WHAT**: Prototype CCGSC with VM orchestration (e.g., using Docker/Podman + WebAssembly for browsers); evaluate via simulations/benchmarks.
- **HOW**: Use MPI/PVM for messaging; P2P torrent for sharing; blockchain for auth. Test on LAN/WAN with metrics like throughput, latency, cost savings.
- **Novelty**: Integration of Dew offline + full OS VMs with P2P/blockchain; solves heterogeneity in crowdsourced HPC (no other platform combines this for probabilistic results).
- **Problems CCGSC Solves & How**:
    - **High Costs**: Crowdsources idle resources (P2P discovery), slashing CapEx 70-90%.
    - **Resource Waste**: Dynamic allocation/pooling recycles idle CPUs/GPUs/RAM.
    - **Intermittency**: Dew layer allows offline processing/sync.
    - **Security**: Lightweight blockchain for auth/consensus.
    - **Scalability**: Hierarchical layers + MPI for parallelism in probabilistic tasks (e.g., simulations via independent subtasks).

#### 4. Platform-Specific Questions

- **Full OS VMs in Other Platforms**: No—BOINC/Golem run lightweight tasks, not full VMs/OS for personal use. Clouds (AWS) offer VMs but not crowd-sourced/incentive-based. CCGSC's novelty: VMs act as personal PCs while contributing (e.g., via Hyper-V/WSL isolation).
- **P2P Torrent + Lightweight Blockchain**: Unique to CCGSC; others use centralized ledgers (Golem) or none (BOINC). This enables secure, decentralized sharing without heavy overhead.

#### 5. Local Cluster Creation

- **Using RDP/CRD for Clusters**: Yes, feasible for local CCGSC-like setups. RDP/CRD allows remote control; combine with MPI/PVM for task distribution over LAN (e.g., head node RDP to workers for orchestration). Pros: Simple; Cons: Latency for HPC. Start with CRD for ease (browser-based).
- **Using WSL/Sandbox/Hyper-V/CRD for Local Clusters**: Absolutely—ideal for prototyping CCGSC. WSL2 for Linux VMs; Sandbox for isolated tasks; Hyper-V for Windows VMs; RDP/CRD for networking. How: Set up head node in Hyper-V, workers in WSL/Sandboxes; use MPI over LAN. This mimics CCGSC layers (e.g., Sandbox as Dew).

#### 6. Research Paper Topics (Based on Your Plan)

Your plan focuses on CCGSC's architecture, layers, resource sharing, and applications. I'll derive topics progressively.

- **1 Single Topic**: "Design and Evaluation of CCGSC: A Hierarchical Crowd-Sourced Supercomputing Platform for Probabilistic Workloads."
- **3 Topics from the Plan** (Expanding on core elements like layers, VMs, and parallelism):
    1. "Multi-Layer Architecture in CCGSC: Integrating Dew, Cluster, and Grid for Resilient Distributed Computing."
    2. "Dynamic Resource Allocation in CCGSC VMs: P2P Protocols for CPU/GPU/RAM Pooling in Heterogeneous Networks."
    3. "Application Fields of CCGSC: Enhancing Probabilistic Simulations in AI/ML and Scientific Computing via Crowdsourcing."
- **5 Topics from the Plan** (Further branching into implementation, security, evaluation, gaps, and novelty):
    1. "VM Orchestration in CCGSC: Using Docker, Podman, and WebAssembly for Browser-Based Dew Layer Nodes."
    2. "Security Mechanisms in CCGSC: Lightweight Blockchain and P2P Torrent for Authentication in Crowd Networks."
    3. "Performance Evaluation of CCGSC vs. Traditional HPC: Benchmarks for Parallel Task Offloading in Probabilistic Scenarios."
    4. "Research Gaps in Decentralized Computing: How CCGSC Addresses Resource Waste in Clouds and Volunteer Systems."
    5. "Novelty and Contributions of CCGSC: Enabling Full OS VMs for Personal and Supercomputing Use in a Multi-Layer Framework."

These topics are structured for journal articles (e.g., IEEE Transactions on Cloud Computing or ACM Computing Surveys), with abstracts focusing on novelty/gaps. If you need outlines or abstracts, let me know!







# Existing Decentralized Compute Marketplaces and Protocols

Several platforms and projects mirror the ambition of building a global, volunteer-powered, reward-based P2P compute grid. They differ in architecture, incentive models, and targeted workloads. Key examples include:

## 1. Golem Network

Definition & Architecture  
Golem is an open-source, peer-to-peer marketplace for compute power. Nodes (“providers”) rent out unused CPU/GPU cycles via a lightweight protocol and are compensated in GLM tokens[1](https://www.golem.network/platform).

Pros

- True P2P marketplace, no central server or operator[2](https://www.binance.com/en/research/projects/Golem).    
- Supports general-purpose compute tasks (e.g., CGI rendering, ML inference).    
- Modular design; integrates easily with existing dApps.
    

Cons

- Currently limited to batch and stateless workloads.    
- Network performance depends on provider availability and heterogeneity.    
- GLM price volatility can disrupt provider incentives.
    

Use Cases

- 3D rendering pipelines.    
- Scientific batch jobs (e.g., protein simulations).    
- Distributed ML inference.
    

When to Use

- When workloads can be parallelized into independent tasks.    
- If you need a turnkey, blockchain-mediated compute marketplace.
    

Best Practices

- Pre-benchmark tasks on small test clusters to estimate costs.    
- Maintain redundant providers to improve reliability.    
- Use off-chain aggregation to minimize on-chain transaction fees.
    

## 2. iExec RLC

Definition & Architecture  
iExec provides a decentralized marketplace for cloud computing resources, with proof-of-contribution consensus. Providers stake RLC tokens and are rewarded for off-chain compute services[3](https://www.coinbase.com/price/rlc).

Pros

- Enterprise-grade SLAs and workflow orchestration.    
- Support for confidential compute via Intel SGX.    
- Integrated marketplace for data, algorithms, and resources.
    

Cons

- Token economics require staking, which may deter small providers.    
- Focused more on cloud-style on-demand VMs than ultra-low-power edge devices.
    

Use Cases

- Secure analytics on private data.    
- On-demand GPU clusters for DL training.    
- Data marketplace for specialized datasets.
    

When to Use

- When workload privacy is critical.    
- For managed, on-demand clusters with formal SLAs.
    

Best Practices

- Stake sufficient RLC to ensure resource access.    
- Leverage SGX enclaves for sensitive tasks.    
- Integrate with Kubernetes for dynamic scaling.
    

## 3. SONM

Definition & Architecture  
SONM is a fog-computing platform that pools idle resources globally. Task distribution uses containerized workloads over a hybrid blockchain/P2P network, and providers earn SNM tokens[4](https://simpleswap.io/blog/what-is-sonm).

Pros

- Real-time fog computing for low-latency tasks.    
- Docker-based containers simplify deployment.    
- Rewards based on actual resource usage.
    

Cons

- Network still maturing; spotty provider coverage in some regions.    
- Container orchestration overhead on low-power devices.
    

Use Cases

- Edge-level IoT analytics.    
- Real-time video transcoding.    
- Microservices for latency-sensitive applications.
    

When to Use

- For tasks requiring sub-second response at the network edge.    
- When deploying heterogeneous container workloads.
    

Best Practices

- Use service meshes (e.g., Istio) for resilience.    
- Monitor edge node capacity to avoid overload.    
- Implement local caching to reduce network I/O.
    

## 4. DeepBrain Chain (DBC)

Definition & Architecture  
DeepBrain Chain offers AI-focused compute via a NEO-based blockchain. Providers supply GPU cycles, and AI firms access cheap neural-network training environments, paying in DBC tokens[5](https://www.deepbrainchain.org/DeepBrainChainWhitepaper_en.pdf).

Pros

- Specialized optimizations for deep-learning frameworks (TensorFlow, Caffe).    
- Smart contracts enforce data privacy between model trainers and data owners.    
- High concurrency and low latency for AI workloads.
    

Cons

- NEO platform limits interoperability with other blockchains.    
- Predominantly focused on ML training, not general compute.
    

Use Cases

- Large-scale DL model training.    
- Federated learning on private datasets.    
- On-chain AI inference microservices.
    

When to Use

- When training complex neural nets with strict data-privacy needs.    
- To lower costs vs. self-hosted GPU clusters.
    

Best Practices

- Prepackage environments in containers for consistency.    
- Leverage smart contracts to audit and verify training runs.    
- Use distributed sharding strategies to parallelize large models.
    

## 5. Ankr Network (ANKR)

Definition & Architecture  
Ankr provides decentralized cloud infrastructure for Web3 via idle data-center resources. It supports node hosting, API endpoints, and staking, with providers rewarded in ANKR tokens[6](https://www.bitget.com/wiki/what-is-ankr).

Pros

- Supports multiple blockchains (Ethereum, BSC, Polygon).    
- One-click node deployment and edge-optimized deployments.    
- Competitive pricing vs. centralized cloud.
    

Cons

- Primarily designed for blockchain nodes rather than arbitrary compute.    
- Staking economics can fluctuate with token price.
    

Use Cases

- Fast node provisioning for dApp backends.    
- Lightweight compute jobs via container registry.    
- On-chain analytics requiring RPC access.
    

When to Use

- When building cross-chain, Web3 applications needing dedicated node endpoints.    
- To monetize underutilized data center capacity.
    

Best Practices

- Combine with caching layers to reduce RPC calls.    
- Pool providers by region for DR and geo-load balancing.    
- Monitor token economics to optimize provider reward levels.
    

# Comparative Overview

|Platform|Compute Focus|Incentive Token|Suitability|Privacy|Ease of Onboarding|
|---|---|---|---|---|---|
|Golem|General GPU/CPU tasks|GLM|Batch jobs, rendering, ML inference|Low|High|
|iExec|Confidential compute|RLC|Secure ML, data analytics|High|Medium|
|SONM|Fog/edge containers|SNM|Low-latency edge compute|Medium|Medium|
|DeepBrain Chain|AI training|DBC|Deep-learning, federated learning|High|Low-Medium|
|Ankr|Web3 node hosting|ANKR|dApp node endpoints, APIs|Medium|Very High|

# Recommendations for Improvement

To realize your vision—a unified Dew→Mist→Edge→Cluster→Grid supercomputing continuum—consider:

1. **Unified Orchestration Layer**  
    Develop an **AI-driven scheduler** that dynamically assigns workloads across device tiers (low-power to server-grade) based on latency, energy, and cost constraints. Borrow concepts from Kubernetes auto-scaling and iExec’s workflow engine.
    
2. **Multi-Token Incentive Model**  
    Use a **dual-token system**:
    
    - A stable-value reward token (to insulate providers from volatility).        
    - A utility token for governance and priority access.
        
3. **Lightweight Blockchain Sharding**  
    Implement a **layer-2 sharded ledger** that records only essential metadata (task proofs, reputation scores) on-chain, minimizing blockchain load and enabling high task throughput akin to Golem’s off-chain aggregation.
    
4. **Hybrid Consensus: Proof-of-Useful-Work + Stake**  
    Combine **Proof-of-Useful-Work** (HEPchain style[7](https://arxiv.org/abs/2304.13507)) for compute validation with a **Proof-of-Stake** layer for ledger security, balancing energy efficiency and trust.
    
5. **Edge-Native Container Runtime**  
    Integrate a **lightweight WASM-based runtime** for low-power devices, reducing the footprint vs. Docker and enabling efficient edge participation, as inspired by SONM’s container model.
    
6. **Data Privacy via Secure Enclaves**  
    Provide optional **TEE/SGX integration** for sensitive workloads, drawing from iExec’s confidential compute offering.
    
7. **Comprehensive Monitoring & SLAs**  
    Offer real-time QoS dashboards and **SLA-backed compute tiers**—from best-effort dew/mist nodes to guaranteed-performance clusters—to meet varying application needs.
    
8. **Best Practices for Providers**
    
    - Maintain **redundant connectivity** and **auto-heal scripts**.
        
    - Use **predictive scaling** driven by historical load patterns.
        
    - Automate token reward claims via **on-node “harvester” agents**.
        

By combining the proven strengths of existing decentralized compute platforms with these enhancements, you can build a scalable, secure, and efficient global supercomputing fabric spanning idle mobile devices through exascale clusters.

1. [https://www.golem.network/platform](https://www.golem.network/platform)
2. [https://www.binance.com/en/research/projects/Golem](https://www.binance.com/en/research/projects/Golem)
3. [https://www.coinbase.com/price/rlc](https://www.coinbase.com/price/rlc)
4. [https://simpleswap.io/blog/what-is-sonm](https://simpleswap.io/blog/what-is-sonm)
5. [https://www.deepbrainchain.org/DeepBrainChainWhitepaper_en.pdf](https://www.deepbrainchain.org/DeepBrainChainWhitepaper_en.pdf)
6. [https://www.bitget.com/wiki/what-is-ankr](https://www.bitget.com/wiki/what-is-ankr)
7. [https://arxiv.org/abs/2304.13507](https://arxiv.org/abs/2304.13507)
8. [https://ppl-ai-file-upload.s3.amazonaws.com/web/direct-files/attachments/58780524/cd929b03-ffe8-4f09-9cbe-843d20fadaa5/Introduction-v1.1-AutoRecovered.docx](https://ppl-ai-file-upload.s3.amazonaws.com/web/direct-files/attachments/58780524/cd929b03-ffe8-4f09-9cbe-843d20fadaa5/Introduction-v1.1-AutoRecovered.docx)
9. [https://ppl-ai-file-upload.s3.amazonaws.com/web/direct-files/attachments/58780524/56b6f187-6481-4516-92dd-d0caf11db38b/paste-2.txt](https://ppl-ai-file-upload.s3.amazonaws.com/web/direct-files/attachments/58780524/56b6f187-6481-4516-92dd-d0caf11db38b/paste-2.txt)
10. [https://ppl-ai-file-upload.s3.amazonaws.com/web/direct-files/attachments/58780524/17a19bc1-f3cc-435e-a398-31f06fe5a13a/paste-3.txt](https://ppl-ai-file-upload.s3.amazonaws.com/web/direct-files/attachments/58780524/17a19bc1-f3cc-435e-a398-31f06fe5a13a/paste-3.txt)
11. [https://www.sec.gov/Archives/edgar/data/1178697/000164117225001720/form10-k.htm](https://www.sec.gov/Archives/edgar/data/1178697/000164117225001720/form10-k.htm)
12. [https://www.sec.gov/Archives/edgar/data/1178697/000149315224011530/form10-k.htm](https://www.sec.gov/Archives/edgar/data/1178697/000149315224011530/form10-k.htm)
13. [https://www.sec.gov/Archives/edgar/data/1178697/000149315224022640/formdef14a.htm](https://www.sec.gov/Archives/edgar/data/1178697/000149315224022640/formdef14a.htm)
14. [https://www.sec.gov/Archives/edgar/data/1178697/000149315223008199/form10-k.htm](https://www.sec.gov/Archives/edgar/data/1178697/000149315223008199/form10-k.htm)
15. [https://www.sec.gov/Archives/edgar/data/1178697/000156459022011226/sonm-10k_20211231.htm](https://www.sec.gov/Archives/edgar/data/1178697/000156459022011226/sonm-10k_20211231.htm)
16. [https://www.sec.gov/Archives/edgar/data/1178697/000156459022019279/sonm-10q_20220331.htm](https://www.sec.gov/Archives/edgar/data/1178697/000156459022019279/sonm-10q_20220331.htm)
17. [https://www.ssrn.com/abstract=3675987](https://www.ssrn.com/abstract=3675987)
18. [https://www.ssrn.com/abstract=3782221](https://www.ssrn.com/abstract=3782221)
19. [https://www.cambridge.org/core/product/identifier/CBO9780511541353A007/type/book_part](https://www.cambridge.org/core/product/identifier/CBO9780511541353A007/type/book_part)
20. [http://ijict.iaescore.com/index.php/IJICT/article/view/19298](http://ijict.iaescore.com/index.php/IJICT/article/view/19298)
21. [https://www.cambridge.org/core/product/identifier/CBO9781107295612A010/type/book_part](https://www.cambridge.org/core/product/identifier/CBO9781107295612A010/type/book_part)
22. [https://www.jstor.org/stable/10.2307/40250841?origin=crossref](https://www.jstor.org/stable/10.2307/40250841?origin=crossref)
23. [https://www.golem.network](https://www.golem.network/)
24. [https://coinmarketcap.com/currencies/golem-network-tokens/](https://coinmarketcap.com/currencies/golem-network-tokens/)
25. [https://ch.linkedin.com/company/golem-network](https://ch.linkedin.com/company/golem-network)
26. [https://kriptomat.io/cryptocurrency-prices/golem-glm-price/what-is/](https://kriptomat.io/cryptocurrency-prices/golem-glm-price/what-is/)
27. [https://iq.wiki/wiki/iexec](https://iq.wiki/wiki/iexec)
28. [https://coinbureau.com/review/sonm-snm/](https://coinbureau.com/review/sonm-snm/)
29. [https://www.thebigwhale.io/tokens/rlc](https://www.thebigwhale.io/tokens/rlc)
30. [https://venturebeat.com/business/sonm-uses-blockchain-to-create-a-decentralized-computing-power-marketplace/](https://venturebeat.com/business/sonm-uses-blockchain-to-create-a-decentralized-computing-power-marketplace/)
31. [https://www.sec.gov/Archives/edgar/data/1871638/000119312525023099/d906819ds1a.htm](https://www.sec.gov/Archives/edgar/data/1871638/000119312525023099/d906819ds1a.htm)
32. [https://www.sec.gov/Archives/edgar/data/2046328/000121390025058113/ea0246813-s1a1_bitwise.htm](https://www.sec.gov/Archives/edgar/data/2046328/000121390025058113/ea0246813-s1a1_bitwise.htm)
33. [https://www.sec.gov/Archives/edgar/data/2068385/000182912625003670/rothchholdings_s4.htm](https://www.sec.gov/Archives/edgar/data/2068385/000182912625003670/rothchholdings_s4.htm)
34. [https://www.sec.gov/Archives/edgar/data/1871638/000119312525008689/d906819ds1.htm](https://www.sec.gov/Archives/edgar/data/1871638/000119312525008689/d906819ds1.htm)
35. [https://www.sec.gov/Archives/edgar/data/896493/000121465925005868/r4925210k.htm](https://www.sec.gov/Archives/edgar/data/896493/000121465925005868/r4925210k.htm)
36. [https://www.sec.gov/Archives/edgar/data/1394056/000095017025041974/oss-20241231.htm](https://www.sec.gov/Archives/edgar/data/1394056/000095017025041974/oss-20241231.htm)
37. [http://www.sersc.org/journals/AJMAHS/vol6_no1_2016/36.pdf](http://www.sersc.org/journals/AJMAHS/vol6_no1_2016/36.pdf)
38. [https://arxiv.org/pdf/2210.05365.pdf](https://arxiv.org/pdf/2210.05365.pdf)
39. [https://arxiv.org/pdf/1806.06575.pdf](https://arxiv.org/pdf/1806.06575.pdf)
40. [http://ejnteti.jteti.ugm.ac.id/index.php/JNTETI/article/download/395/318](http://ejnteti.jteti.ugm.ac.id/index.php/JNTETI/article/download/395/318)
41. [https://arxiv.org/html/2503.23644v1](https://arxiv.org/html/2503.23644v1)
42. [https://arxiv.org/pdf/2401.05345.pdf](https://arxiv.org/pdf/2401.05345.pdf)
43. [https://rendernetwork.com](https://rendernetwork.com/)
44. [https://cointelegraph.com/news/render-network-for-decentralized-gpu-rendering](https://cointelegraph.com/news/render-network-for-decentralized-gpu-rendering)
45. [https://www.coingecko.com/learn/what-is-render-network-rndr-crypto](https://www.coingecko.com/learn/what-is-render-network-rndr-crypto)
46. [https://know.rendernetwork.com](https://know.rendernetwork.com/)
47. [https://www.coinbackyard.com/blockchain/render-network-decentralized-gpu-rendering/](https://www.coinbackyard.com/blockchain/render-network-decentralized-gpu-rendering/)
48. [https://indexcoop.com/blog/render-network-rndr](https://indexcoop.com/blog/render-network-rndr)
49. [https://renderfoundation.com/gpu](https://renderfoundation.com/gpu)
50. [https://www.sec.gov/Archives/edgar/data/2057315/0002057315-25-000001-index.htm](https://www.sec.gov/Archives/edgar/data/2057315/0002057315-25-000001-index.htm)
51. [https://www.sec.gov/Archives/edgar/data/2066824/000206682425000002/vaneckbnbetfs-1.htm](https://www.sec.gov/Archives/edgar/data/2066824/000206682425000002/vaneckbnbetfs-1.htm)
52. [https://www.sec.gov/Archives/edgar/data/1720265/000095017025035469/zcsh-20241231.htm](https://www.sec.gov/Archives/edgar/data/1720265/000095017025035469/zcsh-20241231.htm)
53. [https://www.sec.gov/Archives/edgar/data/1759186/000168316825004762/coeptis_s4.htm](https://www.sec.gov/Archives/edgar/data/1759186/000168316825004762/coeptis_s4.htm)
54. [https://www.sec.gov/Archives/edgar/data/2057388/000113743925000111/s1.htm](https://www.sec.gov/Archives/edgar/data/2057388/000113743925000111/s1.htm)
55. [https://www.sec.gov/Archives/edgar/data/1527762/000164117225007755/form20-f.htm](https://www.sec.gov/Archives/edgar/data/1527762/000164117225007755/form20-f.htm)
56. [https://ieeexplore.ieee.org/document/10174864/](https://ieeexplore.ieee.org/document/10174864/)
57. [https://ieeexplore.ieee.org/document/10528325/](https://ieeexplore.ieee.org/document/10528325/)
58. [https://ieeexplore.ieee.org/document/10049604/](https://ieeexplore.ieee.org/document/10049604/)
59. [https://ieeexplore.ieee.org/document/10701002/](https://ieeexplore.ieee.org/document/10701002/)
60. [https://ieeexplore.ieee.org/document/9684238/](https://ieeexplore.ieee.org/document/9684238/)
61. [https://ieeexplore.ieee.org/document/10839037/](https://ieeexplore.ieee.org/document/10839037/)
62. [https://www.deepbrainchain.org](https://www.deepbrainchain.org/)
63. [https://www.gate.com/learn/articles/what-is-deepbrain-chain-all-you-need-to-know-about-deepbrain-chain/3749](https://www.gate.com/learn/articles/what-is-deepbrain-chain-all-you-need-to-know-about-deepbrain-chain/3749)
64. [https://en.thebigwhale.io/token-summary/deepbrain-chain](https://en.thebigwhale.io/token-summary/deepbrain-chain)
65. [https://www.bitrue.com/blog/deepbrain-chain-dbc-guide](https://www.bitrue.com/blog/deepbrain-chain-dbc-guide)
66. [https://www.diadata.org/web3-ai-map/deepbrain/](https://www.diadata.org/web3-ai-map/deepbrain/)
67. [https://coins.ph/academy/what-is-deepbrain-chain-dbc-everything-you-need-to-know/](https://coins.ph/academy/what-is-deepbrain-chain-dbc-everything-you-need-to-know/)
68. [https://www.accessnewswire.com/newsroom/en/blockchain-and-cryptocurrency/deepbrain-chain-leads-the-charge-in-embracing-the-depin-revolution-wit-848286](https://www.accessnewswire.com/newsroom/en/blockchain-and-cryptocurrency/deepbrain-chain-leads-the-charge-in-embracing-the-depin-revolution-wit-848286)
69. [https://www.sec.gov/Archives/edgar/data/2060021/0002060021-25-000001-index.htm](https://www.sec.gov/Archives/edgar/data/2060021/0002060021-25-000001-index.htm)
70. [https://www.sec.gov/Archives/edgar/data/2049410/0002049410-24-000001-index.htm](https://www.sec.gov/Archives/edgar/data/2049410/0002049410-24-000001-index.htm)
71. [https://www.sec.gov/Archives/edgar/data/2011535/000113743924001040/fets1a05312024.htm](https://www.sec.gov/Archives/edgar/data/2011535/000113743924001040/fets1a05312024.htm)
72. [https://www.sec.gov/Archives/edgar/data/1729997/000095017023045927/gdlc-20230630.htm](https://www.sec.gov/Archives/edgar/data/1729997/000095017023045927/gdlc-20230630.htm)
73. [https://www.sec.gov/Archives/edgar/data/1732409/000095017022018010/bchg-20220630.htm](https://www.sec.gov/Archives/edgar/data/1732409/000095017022018010/bchg-20220630.htm)
74. [https://www.sec.gov/Archives/edgar/data/2011535/000168035924000151/fets1a06212024.htm](https://www.sec.gov/Archives/edgar/data/2011535/000168035924000151/fets1a06212024.htm)
75. [https://ieeexplore.ieee.org/document/8412212/](https://ieeexplore.ieee.org/document/8412212/)
76. [http://research.ijcaonline.org/volume93/number8/pxc3895784.pdf](http://research.ijcaonline.org/volume93/number8/pxc3895784.pdf)
77. [https://ieeexplore.ieee.org/document/9846938/](https://ieeexplore.ieee.org/document/9846938/)
78. [https://ieeexplore.ieee.org/document/10690718/](https://ieeexplore.ieee.org/document/10690718/)
79. [https://ieeexplore.ieee.org/document/10536667/](https://ieeexplore.ieee.org/document/10536667/)
80. [https://ijarsct.co.in/Paper22316.pdf](https://ijarsct.co.in/Paper22316.pdf)
81. [https://atomicwallet.io/academy/articles/what-is-akash-network](https://atomicwallet.io/academy/articles/what-is-akash-network)
82. [https://www.coinspeaker.com/guides/akash-network-akt-a-decentralized-cloud-for-defi/](https://www.coinspeaker.com/guides/akash-network-akt-a-decentralized-cloud-for-defi/)
83. [https://zebpay.com/blog/how-does-the-ankr-network-work](https://zebpay.com/blog/how-does-the-ankr-network-work)
84. [https://www.cryptohopper.com/currencies/detail?currency=ANKR](https://www.cryptohopper.com/currencies/detail?currency=ANKR)
85. [https://www.coingecko.com/en/coins/ankr-network](https://www.coingecko.com/en/coins/ankr-network)
86. [https://www.sec.gov/Archives/edgar/data/2057388/000206159025000090/s1a.htm](https://www.sec.gov/Archives/edgar/data/2057388/000206159025000090/s1a.htm)
87. [https://www.sec.gov/Archives/edgar/data/1725882/000121390025028697/ea0236654-20f_inxltd.htm](https://www.sec.gov/Archives/edgar/data/1725882/000121390025028697/ea0236654-20f_inxltd.htm)
88. [https://www.sec.gov/Archives/edgar/data/2028834/000121390025054351/ea0245677-s1a1_21shares.htm](https://www.sec.gov/Archives/edgar/data/2028834/000121390025054351/ea0245677-s1a1_21shares.htm)
89. [https://www.sec.gov/Archives/edgar/data/1859392/000162828025028001/glxy-20250527.htm](https://www.sec.gov/Archives/edgar/data/1859392/000162828025028001/glxy-20250527.htm)
90. [https://www.sec.gov/Archives/edgar/data/2067111/000121390025040111/ea0240783-s1_bitwise.htm](https://www.sec.gov/Archives/edgar/data/2067111/000121390025040111/ea0240783-s1_bitwise.htm)
91. [https://ieeexplore.ieee.org/document/10239356/](https://ieeexplore.ieee.org/document/10239356/)
92. [https://ieeexplore.ieee.org/document/10338897/](https://ieeexplore.ieee.org/document/10338897/)
93. [https://ieeexplore.ieee.org/document/9944948/](https://ieeexplore.ieee.org/document/9944948/)
94. [https://ieeexplore.ieee.org/document/10098911/](https://ieeexplore.ieee.org/document/10098911/)
95. [https://ieeexplore.ieee.org/document/9783194/](https://ieeexplore.ieee.org/document/9783194/)
96. [https://ieeexplore.ieee.org/document/10124004/](https://ieeexplore.ieee.org/document/10124004/)
97. [https://www.cryptoboostnews.com/brand/golem](https://www.cryptoboostnews.com/brand/golem)
98. [https://learn.bybit.com/en/web3/what-is-golem-crypto-glm/](https://learn.bybit.com/en/web3/what-is-golem-crypto-glm/)
99. [https://www.sec.gov/Archives/edgar/data/1930756/0001930756-22-000001-index.htm](https://www.sec.gov/Archives/edgar/data/1930756/0001930756-22-000001-index.htm)
100. [https://www.sec.gov/Archives/edgar/data/2013744/000199937124007581/bitwise-s1a_061824.htm](https://www.sec.gov/Archives/edgar/data/2013744/000199937124007581/bitwise-s1a_061824.htm)
101. [https://www.sec.gov/Archives/edgar/data/2013744/000199937124008735/bitwise-s1a_071124.htm](https://www.sec.gov/Archives/edgar/data/2013744/000199937124008735/bitwise-s1a_071124.htm)
102. [https://www.sec.gov/Archives/edgar/data/2013744/000199937124008247/bitwise-s1a_070324.htm](https://www.sec.gov/Archives/edgar/data/2013744/000199937124008247/bitwise-s1a_070324.htm)
103. [https://www.sec.gov/Archives/edgar/data/1725882/000121390024034149/ea0204059-20f_inxltd.htm](https://www.sec.gov/Archives/edgar/data/1725882/000121390024034149/ea0204059-20f_inxltd.htm)
104. [https://www.sec.gov/Archives/edgar/data/1761325/000095017023065631/gxlm-20230930.htm](https://www.sec.gov/Archives/edgar/data/1761325/000095017023065631/gxlm-20230930.htm)
105. [https://zenodo.org/records/11504157/files/GENIAL_ICC_Workshp_2024.pdf](https://zenodo.org/records/11504157/files/GENIAL_ICC_Workshp_2024.pdf)
106. [https://arxiv.org/abs/2109.10642v1](https://arxiv.org/abs/2109.10642v1)
107. [http://jultika.oulu.fi/files/nbnfi-fe2022020717882.pdf](http://jultika.oulu.fi/files/nbnfi-fe2022020717882.pdf)
108. [https://arxiv.org/html/2404.00034v1](https://arxiv.org/html/2404.00034v1)
109. [https://pmc.ncbi.nlm.nih.gov/articles/PMC7787356/](https://pmc.ncbi.nlm.nih.gov/articles/PMC7787356/)
110. [https://pmc.ncbi.nlm.nih.gov/articles/PMC8597856/](https://pmc.ncbi.nlm.nih.gov/articles/PMC8597856/)
111. [http://arxiv.org/pdf/2205.15614.pdf](http://arxiv.org/pdf/2205.15614.pdf)
112. [http://arxiv.org/pdf/2203.02865.pdf](http://arxiv.org/pdf/2203.02865.pdf)
113. [https://www.bitrue.com/blog/golem-glm-coin](https://www.bitrue.com/blog/golem-glm-coin)
114. [https://www.sec.gov/Archives/edgar/data/1889123/000121390025026537/ea0235889-s1_foldhold.htm](https://www.sec.gov/Archives/edgar/data/1889123/000121390025026537/ea0235889-s1_foldhold.htm)
115. [https://www.sec.gov/Archives/edgar/data/1889123/000101376225004107/ea0232841-10k_fold.htm](https://www.sec.gov/Archives/edgar/data/1889123/000101376225004107/ea0232841-10k_fold.htm)
116. [https://www.sec.gov/Archives/edgar/data/1787441/000121390024085654/ea0212543-01.htm](https://www.sec.gov/Archives/edgar/data/1787441/000121390024085654/ea0212543-01.htm)
117. [https://www.sec.gov/Archives/edgar/data/1889123/000095017025072818/ck0001889123-20250331.htm](https://www.sec.gov/Archives/edgar/data/1889123/000095017025072818/ck0001889123-20250331.htm)
118. [https://www.sec.gov/Archives/edgar/data/1889123/000095017025087072/fld-20250616.htm](https://www.sec.gov/Archives/edgar/data/1889123/000095017025087072/fld-20250616.htm)
119. [https://www.sec.gov/Archives/edgar/data/1679788/000167978825000022/coin-20241231.htm](https://www.sec.gov/Archives/edgar/data/1679788/000167978825000022/coin-20241231.htm)
120. [https://ieeexplore.ieee.org/document/10689736/](https://ieeexplore.ieee.org/document/10689736/)
121. [https://www.semanticscholar.org/paper/52c8861d9328225cf21d9d1df763b60f8c225e56](https://www.semanticscholar.org/paper/52c8861d9328225cf21d9d1df763b60f8c225e56)
122. [https://www.emerald.com/insight/content/doi/10.1108/JICES-02-2020-0018/full/html](https://www.emerald.com/insight/content/doi/10.1108/JICES-02-2020-0018/full/html)
123. [http://arxiv.org/pdf/1306.0846.pdf](http://arxiv.org/pdf/1306.0846.pdf)
124. [https://www.matec-conferences.org/articles/matecconf/pdf/2018/16/matecconf_mms2018_05009.pdf](https://www.matec-conferences.org/articles/matecconf/pdf/2018/16/matecconf_mms2018_05009.pdf)
125. [https://gridcoin.us](https://gridcoin.us/)
126. [https://en.wikipedia.org/wiki/Gridcoin](https://en.wikipedia.org/wiki/Gridcoin)
127. [http://bitcoinwiki.org/wiki/gridcoin](http://bitcoinwiki.org/wiki/gridcoin)
128. [https://gridcoin.us/guides/boinc-install.htm](https://gridcoin.us/guides/boinc-install.htm)
129. [https://www.coinbase.com/en-de/price/gridcoin](https://www.coinbase.com/en-de/price/gridcoin)
130. [https://www.centralcharts.com/en/559171-folding-coin/informations](https://www.centralcharts.com/en/559171-folding-coin/informations)
131. [https://www.nasdaq.com/articles/fold-launches-bitcoin-rewards-credit-card](https://www.nasdaq.com/articles/fold-launches-bitcoin-rewards-credit-card)
132. [https://foldapp.com/rewards](https://foldapp.com/rewards)
133. [https://www.sec.gov/Archives/edgar/data/1859392/000110465922008454/tm2127871-8_s4.htm](https://www.sec.gov/Archives/edgar/data/1859392/000110465922008454/tm2127871-8_s4.htm)
134. [https://www.sec.gov/Archives/edgar/data/1405064/000110465922008454/tm2127871-8_s4.htm](https://www.sec.gov/Archives/edgar/data/1405064/000110465922008454/tm2127871-8_s4.htm)
135. [https://arxiv.org/abs/2405.14767](https://arxiv.org/abs/2405.14767)
136. [https://ieeexplore.ieee.org/document/10835647/](https://ieeexplore.ieee.org/document/10835647/)
137. [https://crrjournals.com/crrj/node/63](https://crrjournals.com/crrj/node/63)
138. [https://www.emerald.com/insight/content/doi/10.1108/K-04-2024-0977/full/html](https://www.emerald.com/insight/content/doi/10.1108/K-04-2024-0977/full/html)
139. [https://www.mdpi.com/2078-2489/14/1/31](https://www.mdpi.com/2078-2489/14/1/31)
140. [https://www.mdpi.com/1999-4907/15/12/2180](https://www.mdpi.com/1999-4907/15/12/2180)
141. [https://iq.wiki/wiki/deepbrain-chain](https://iq.wiki/wiki/deepbrain-chain)
142. [https://kriptomat.io/cryptocurrency-prices/ankr-price/what-is/](https://kriptomat.io/cryptocurrency-prices/ankr-price/what-is/)
143. [https://x4t.com/market/ankr-network/](https://x4t.com/market/ankr-network/)
144. [https://link.springer.com/10.1007/s10894-024-00458-z](https://link.springer.com/10.1007/s10894-024-00458-z)
145. [https://www.semanticscholar.org/paper/9d4d5a92bd5a10e05e3f5769d672c4537a069a10](https://www.semanticscholar.org/paper/9d4d5a92bd5a10e05e3f5769d672c4537a069a10)
146. [https://agupubs.onlinelibrary.wiley.com/doi/10.1029/97WR00409](https://agupubs.onlinelibrary.wiley.com/doi/10.1029/97WR00409)
147. [https://www.semanticscholar.org/paper/ea491283dc3bcbb6c2b40bb56ddfab4aa98c93f0](https://www.semanticscholar.org/paper/ea491283dc3bcbb6c2b40bb56ddfab4aa98c93f0)
148. [https://x.com/golemproject?lang=bn](https://x.com/golemproject?lang=bn)
149. [https://github.com/golemfactory/golem](https://github.com/golemfactory/golem)
150. [https://www.sec.gov/Archives/edgar/data/896493/000121465925008887/i62250s1a1.htm](https://www.sec.gov/Archives/edgar/data/896493/000121465925008887/i62250s1a1.htm)
151. [http://arxiv.org/pdf/1401.0608.pdf](http://arxiv.org/pdf/1401.0608.pdf)
152. [https://arxiv.org/html/2412.15050v4](https://arxiv.org/html/2412.15050v4)
153. [https://arxiv.org/pdf/2402.00028.pdf](https://arxiv.org/pdf/2402.00028.pdf)
154. [https://arxiv.org/pdf/1611.10210.pdf](https://arxiv.org/pdf/1611.10210.pdf)
155. [https://x.com/rendernetwork?lang=bn](https://x.com/rendernetwork?lang=bn)
156. [https://coinmarketcap.com/currencies/render/](https://coinmarketcap.com/currencies/render/)
157. [https://ieeexplore.ieee.org/document/9783023/](https://ieeexplore.ieee.org/document/9783023/)
158. [https://www.mdpi.com/1996-1073/15/15/5313](https://www.mdpi.com/1996-1073/15/15/5313)
159. [https://www.semanticscholar.org/paper/ad103e6b600c9ab81671c90436ddb128d2b574da](https://www.semanticscholar.org/paper/ad103e6b600c9ab81671c90436ddb128d2b574da)
160. [https://www.mdpi.com/1424-8220/22/19/7387](https://www.mdpi.com/1424-8220/22/19/7387)
161. [https://x.com/deepbrainchain?lang=bn](https://x.com/deepbrainchain?lang=bn)
162. [https://dropstab.com/coins/deepbrain-chain](https://dropstab.com/coins/deepbrain-chain)
163. [https://www.sec.gov/Archives/edgar/data/1436229/000164117225010401/form10-q.htm](https://www.sec.gov/Archives/edgar/data/1436229/000164117225010401/form10-q.htm)
164. [https://www.sec.gov/Archives/edgar/data/1588489/000119312523054302/d453116d10k.htm](https://www.sec.gov/Archives/edgar/data/1588489/000119312523054302/d453116d10k.htm)
165. [https://www.hippocampus.si/ISBN/978-961-293-253-4/scores23.10.pdf](https://www.hippocampus.si/ISBN/978-961-293-253-4/scores23.10.pdf)
166. [https://www.semanticscholar.org/paper/940077fc7d7d5b8f182e66acae7dd1cf5ed1ca30](https://www.semanticscholar.org/paper/940077fc7d7d5b8f182e66acae7dd1cf5ed1ca30)
167. [https://www.semanticscholar.org/paper/a8071294abaaaed7a849c8ea5987f39ca885851e](https://www.semanticscholar.org/paper/a8071294abaaaed7a849c8ea5987f39ca885851e)
168. [https://ieeexplore.ieee.org/document/9396921/](https://ieeexplore.ieee.org/document/9396921/)
169. [https://akash.network](https://akash.network/)
170. [https://akash.network/docs/getting-started/intro-to-akash/akash-network/](https://akash.network/docs/getting-started/intro-to-akash/akash-network/)
171. [https://www.okx.com/learn/akash-network](https://www.okx.com/learn/akash-network)
172. [https://www.alchemy.com/dapps/akash-network](https://www.alchemy.com/dapps/akash-network)
173. [https://iq.wiki/wiki/akash-network](https://iq.wiki/wiki/akash-network)
174. [https://link.springer.com/10.1007/s00779-024-01821-9](https://link.springer.com/10.1007/s00779-024-01821-9)
175. [https://link.springer.com/10.1007/s10723-023-09729-z](https://link.springer.com/10.1007/s10723-023-09729-z)
176. [https://arxiv.org/pdf/2303.14162.pdf](https://arxiv.org/pdf/2303.14162.pdf)
177. [https://arxiv.org/pdf/2202.03836.pdf](https://arxiv.org/pdf/2202.03836.pdf)
178. [https://glm.golem.network](https://glm.golem.network/)
179. [https://www.semanticscholar.org/paper/cc465b104163529d55d18b5e16759567eb75c14c](https://www.semanticscholar.org/paper/cc465b104163529d55d18b5e16759567eb75c14c)
180. [https://link.springer.com/10.1007/978-981-15-4218-3_13](https://link.springer.com/10.1007/978-981-15-4218-3_13)
181. [https://peerj.com/articles/2248](https://peerj.com/articles/2248)
182. [https://www.geosci-model-dev.net/10/811/2017/gmd-10-811-2017.pdf](https://www.geosci-model-dev.net/10/811/2017/gmd-10-811-2017.pdf)
183. [https://news.ycombinator.com/item?id=26236325](https://news.ycombinator.com/item?id=26236325)
184. [https://www.coingecko.com/en/coins/gridcoin-research](https://www.coingecko.com/en/coins/gridcoin-research)
185. [https://www.reddit.com/r/gridcoin/](https://www.reddit.com/r/gridcoin/)
186. [https://linkinghub.elsevier.com/retrieve/pii/S0360835224006818](https://linkinghub.elsevier.com/retrieve/pii/S0360835224006818)
187. [https://ieeexplore.ieee.org/document/10499081/](https://ieeexplore.ieee.org/document/10499081/)
188. [https://dl.acm.org/doi/10.1145/3701716.3715484](https://dl.acm.org/doi/10.1145/3701716.3715484)
189. [https://arxiv.org/abs/2410.13407](https://arxiv.org/abs/2410.13407)
190. [https://www.coinbase.com/price/deepbrain-chain](https://www.coinbase.com/price/deepbrain-chain)




# Hybrid Dew–Fog–Grid Supercomputing Platforms

Existing high-performance computing (HPC) deployments traditionally centralize workloads in large data centers. However, the emerging paradigm of the **computing continuum** spans:

- **Dew** (device-level compute on endpoints)
    
- **Fog** (local, edge servers and micro-data centers)
    
- **Grid** (mid-tier clusters)
    
- **Cloud/Supercomputers** (high-power servers and exascale systems)
    

While few turnkey platforms fully integrate all tiers for scientific HPC, several commercial and research projects exemplify aspects of this continuum:

- **Galaxy Digital’s Helios Campus** co-locates GPU and CPU clusters on a 600 MW power substation, converting legacy Bitcoin-mining sites into AI/HPC facilities to de-bottleneck local grids[1](https://www.sec.gov/Archives/edgar/data/1859392/000162828025028001/glxy-20250527.htm).
    
- **Soluna Cloud’s Projects Kati/Rosa** in Texas pair behind-the-meter wind farms with modular data centers, offering scalable HPC and AI hosting alongside demand-response services[2](https://www.sec.gov/Archives/edgar/data/64463/000164117225015179/forms-1a.htm).
    
- **Hut 8 HPC** leverages custom liquid-cooled racks at renewable-energy sites for GPU-as-a-Service, integrating edge-like onsite orchestration via MaestroOS with exascale-class GPU clusters[3](https://www.sec.gov/Archives/edgar/data/1964789/000155837025001996/hut-20241231x10k.htm)[4](https://www.globenewswire.com/news-release/2024/09/26/2953641/0/en/Hut-8-GPU-as-a-Service-Vertical-Goes-Live-with-Inaugural-Deployment.html).
    
- **Applied Digital** deploys modular HPC camps at “stranded” power sources (wind/solar), using direct grid interconnect to run AI and batch HPC at low-cost energy sites[5](https://marketscale.com/industries/software-and-technology/applied-digital-is-revolutionizing-high-performance-computing-by-locating-facilities-at-unique-power-sources/).
    
- **Recursion’s BioHive SuperPODs** combine on-premises NVIDIA DGX-based exaFLOP-scale supercomputers with cloud bursting on Google Cloud for large-scale biological simulations[6](https://www.sec.gov/Archives/edgar/data/1601830/000160183025000035/rxrx-20241231.htm).
    

In academia, hybrid architectures remain experimental. For deep learning, Song et al. classify deployment across dew, fog, and cloud, anticipating **hybrid cloud–fog–dew HPC** for IoT AI workloads[7](http://repqj.com/index.php/repqj/article/view/3119). Zhang et al. outline scalable dew nodes as a precursor to integrated continuum platforms[8](https://www.mdpi.com/2076-3417/12/19/9510/pdf?version=1663841514).

# Scalability and Energy Efficiency Trade-offs

Comparison of representative distributed HPC models:

|Platform|Peak Throughput|Scalability|Energy Footprint|
|---|---|---|---|
|Volunteer computing (BOINC)|~10 PFLOPS¹|Virtually unlimited volunteers[9](https://boinc.berkeley.edu/boinc_papers/crossroads.pdf)|Consumer PCs: 30–40% less datacenter energy but higher per-device inefficiency[9](https://boinc.berkeley.edu/boinc_papers/crossroads.pdf)|
|Traditional supercomputers|1–2 EFLOPS (Frontier)|Fixed rack count, modular expansion[10](https://dl.acm.org/doi/10.1145/3339186.3339212)|~15–25 MW per site, PUE ~1.1[10](https://dl.acm.org/doi/10.1145/3339186.3339212)|
|Edge/Fog clusters|0.1–10 TFLOPS/per node|Limited by edge node count|Extremely low latency; each node ~20–30% energy of cloud CPU[11](https://www.scpe.org/index.php/scpe/article/view/1558)|
|HPC-as-a-Service (Nimbix, HPE)|Elastic up to 1 EFLOPS|On-demand scaling|Cloud provider PUE ~1.2; hardware-optimized nodes[12](https://eviden.com/solutions/high-performance-computing/hpc-as-a-service/)[13](https://buy.hpe.com/nz/en/use-cases/hpe-high-performance-computing-\(hpc\)-solutions/c/h001023)|

₁ “About 700,000 consumer devices… collectively provide ~93 PFLOPS”[9](https://boinc.berkeley.edu/boinc_papers/crossroads.pdf).

Volunteer projects excel in aggregate scale but lack energy efficiency of purpose-built HPC. Commercial HPC data centers optimize PUE and liquid cooling to minimize energy per FLOP[10](https://dl.acm.org/doi/10.1145/3339186.3339212).

# BOINC & Folding@Home: Characteristics, Pros / Cons

Volunteer computing platforms (BOINC, Folding@Home) share these attributes:

- Heterogeneity & churn: Devices vary in CPU/GPU, join/leave unpredictably[14](http://link.springer.com/10.1007/s10723-019-09497-9).    
- High‐throughput focus: Best for _embarrassingly parallel_ tasks with minimal inter-task communication[9](https://boinc.berkeley.edu/boinc_papers/crossroads.pdf).    
- Security/untrusted nodes: Require result replication and validation; homogeneous redundancy reduces but not eliminates overhead[14](http://link.springer.com/10.1007/s10723-019-09497-9).    
- Low operational cost: Volunteer energy offset by heat reuse, zero direct capital expense for compute[9](https://boinc.berkeley.edu/boinc_papers/crossroads.pdf).
    
Pros:
- Massive aggregate FLOPS at minimal capital cost[9](https://boinc.berkeley.edu/boinc_papers/crossroads.pdf).    
- Extensible to millions of endpoints globally.    
- Ideal for large parameter sweeps, Monte Carlo, batch simulations.
    
Cons:
- Unsuitable for tightly-coupled MPI workloads due to high latency.    
- Throughput wasted on validation and replication overhead (up to 50% slower)[14](http://link.springer.com/10.1007/s10723-019-09497-9).    
- Unreliable devices cause deadline uncertainty; limited QoS control[15](https://boinc.berkeley.edu/boinc_papers/pcgrid_11/p2.pdf).    
- Security vulnerabilities from malicious volunteers remain a risk[9](https://boinc.berkeley.edu/boinc_papers/crossroads.pdf).
    

**When to use:** independent work units, volunteer-friendly scientific workloads.  
**When not to use:** real‐time HPC tasks, applications requiring deterministic low latency or secure enclave.

# Best Practices & Enhancements for Volunteer HPC

To evolve BOINC-style grids toward a dew–fog–grid continuum suitable for HPC:

1. **Fog-proximal scheduling:** deploy _fog nodes_ (local servers) to pre-aggregate and pre-validate results, reducing latency and churn dependency[16](https://arxiv.org/pdf/1903.01699.pdf).
    
2. **Dew-node pipeline:** offload trivial pre-processing to dew devices (IoT/edge) to reserve fog and grid compute for core HPC tasks[8](https://www.mdpi.com/2076-3417/12/19/9510/pdf?version=1663841514).
    
3. **Intelligent replication:** use _adaptive redundancy_ to replicate only on untrusted or new devices, trusting historically reliable nodes[14](http://link.springer.com/10.1007/s10723-019-09497-9).
    
4. **Secure enclaves:** integrate lightweight virtualization or TEEs (e.g., SGX) in fog nodes to improve data integrity and privacy.
    
5. **ML‐driven scheduling:** apply AI-based schedulers (e.g., ATMapper[17](https://ieeexplore.ieee.org/document/10821099/)) to optimize node assignment, minimizing network hops and energy per task.
    
6. **Blockchain‐based incentives:** employ tokenized rewards and immutable task ledgers to enhance trust and participation consistency.
    

By merging **dew** (device-level), **fog** (edge servers), and **grid/cloud** (clustered HPC), such hybrid frameworks can support a broader class of workloads, improve energy efficiency, and extend volunteer computing into latency-sensitive domains.

1. [https://www.sec.gov/Archives/edgar/data/1859392/000162828025028001/glxy-20250527.htm](https://www.sec.gov/Archives/edgar/data/1859392/000162828025028001/glxy-20250527.htm)
2. [https://www.sec.gov/Archives/edgar/data/64463/000164117225015179/forms-1a.htm](https://www.sec.gov/Archives/edgar/data/64463/000164117225015179/forms-1a.htm)
3. [https://www.sec.gov/Archives/edgar/data/1964789/000155837025001996/hut-20241231x10k.htm](https://www.sec.gov/Archives/edgar/data/1964789/000155837025001996/hut-20241231x10k.htm)
4. [https://www.globenewswire.com/news-release/2024/09/26/2953641/0/en/Hut-8-GPU-as-a-Service-Vertical-Goes-Live-with-Inaugural-Deployment.html](https://www.globenewswire.com/news-release/2024/09/26/2953641/0/en/Hut-8-GPU-as-a-Service-Vertical-Goes-Live-with-Inaugural-Deployment.html)
5. [https://marketscale.com/industries/software-and-technology/applied-digital-is-revolutionizing-high-performance-computing-by-locating-facilities-at-unique-power-sources/](https://marketscale.com/industries/software-and-technology/applied-digital-is-revolutionizing-high-performance-computing-by-locating-facilities-at-unique-power-sources/)
6. [https://www.sec.gov/Archives/edgar/data/1601830/000160183025000035/rxrx-20241231.htm](https://www.sec.gov/Archives/edgar/data/1601830/000160183025000035/rxrx-20241231.htm)
7. [http://repqj.com/index.php/repqj/article/view/3119](http://repqj.com/index.php/repqj/article/view/3119)
8. [https://www.mdpi.com/2076-3417/12/19/9510/pdf?version=1663841514](https://www.mdpi.com/2076-3417/12/19/9510/pdf?version=1663841514)
9. [https://boinc.berkeley.edu/boinc_papers/crossroads.pdf](https://boinc.berkeley.edu/boinc_papers/crossroads.pdf)
10. [https://dl.acm.org/doi/10.1145/3339186.3339212](https://dl.acm.org/doi/10.1145/3339186.3339212)
11. [https://www.scpe.org/index.php/scpe/article/view/1558](https://www.scpe.org/index.php/scpe/article/view/1558)
12. [https://eviden.com/solutions/high-performance-computing/hpc-as-a-service/](https://eviden.com/solutions/high-performance-computing/hpc-as-a-service/)
13. [https://buy.hpe.com/nz/en/use-cases/hpe-high-performance-computing-(hpc)-solutions/c/h001023](https://buy.hpe.com/nz/en/use-cases/hpe-high-performance-computing-\(hpc\)-solutions/c/h001023)
14. [http://link.springer.com/10.1007/s10723-019-09497-9](http://link.springer.com/10.1007/s10723-019-09497-9)
15. [https://boinc.berkeley.edu/boinc_papers/pcgrid_11/p2.pdf](https://boinc.berkeley.edu/boinc_papers/pcgrid_11/p2.pdf)
16. [https://arxiv.org/pdf/1903.01699.pdf](https://arxiv.org/pdf/1903.01699.pdf)
17. [https://ieeexplore.ieee.org/document/10821099/](https://ieeexplore.ieee.org/document/10821099/)
18. [https://ppl-ai-file-upload.s3.amazonaws.com/web/direct-files/attachments/58780524/cd929b03-ffe8-4f09-9cbe-843d20fadaa5/Introduction-v1.1-AutoRecovered.docx](https://ppl-ai-file-upload.s3.amazonaws.com/web/direct-files/attachments/58780524/cd929b03-ffe8-4f09-9cbe-843d20fadaa5/Introduction-v1.1-AutoRecovered.docx)
19. [https://ppl-ai-file-upload.s3.amazonaws.com/web/direct-files/attachments/58780524/56b6f187-6481-4516-92dd-d0caf11db38b/paste-2.txt](https://ppl-ai-file-upload.s3.amazonaws.com/web/direct-files/attachments/58780524/56b6f187-6481-4516-92dd-d0caf11db38b/paste-2.txt)
20. [https://ppl-ai-file-upload.s3.amazonaws.com/web/direct-files/attachments/58780524/17a19bc1-f3cc-435e-a398-31f06fe5a13a/paste-3.txt](https://ppl-ai-file-upload.s3.amazonaws.com/web/direct-files/attachments/58780524/17a19bc1-f3cc-435e-a398-31f06fe5a13a/paste-3.txt)
21. [https://www.sec.gov/Archives/edgar/data/1513845/000155837025005991/nbis-20241231x20f.htm](https://www.sec.gov/Archives/edgar/data/1513845/000155837025005991/nbis-20241231x20f.htm)
22. [https://www.sec.gov/Archives/edgar/data/1394056/000095017025041974/oss-20241231.htm](https://www.sec.gov/Archives/edgar/data/1394056/000095017025041974/oss-20241231.htm)
23. [https://www.sec.gov/Archives/edgar/data/1769628/000119312525067651/d899798d424b4.htm](https://www.sec.gov/Archives/edgar/data/1769628/000119312525067651/d899798d424b4.htm)
24. [https://www.sec.gov/Archives/edgar/data/1769628/000119312525058309/d899798ds1a.htm](https://www.sec.gov/Archives/edgar/data/1769628/000119312525058309/d899798ds1a.htm)
25. [https://www.sec.gov/Archives/edgar/data/916793/000117891325001515/zk2533068.htm](https://www.sec.gov/Archives/edgar/data/916793/000117891325001515/zk2533068.htm)
26. [https://www.sec.gov/Archives/edgar/data/1847075/000121390025035765/ea0238503-20f_saiheat.htm](https://www.sec.gov/Archives/edgar/data/1847075/000121390025035765/ea0238503-20f_saiheat.htm)
27. [https://ieeexplore.ieee.org/document/10973671/](https://ieeexplore.ieee.org/document/10973671/)
28. [https://www.mdpi.com/2227-7390/12/1/116](https://www.mdpi.com/2227-7390/12/1/116)
29. [https://www.mdpi.com/2079-9292/13/15/2919](https://www.mdpi.com/2079-9292/13/15/2919)
30. [https://ieeexplore.ieee.org/document/9987329/](https://ieeexplore.ieee.org/document/9987329/)
31. [https://www.mdpi.com/2071-1050/10/4/1258](https://www.mdpi.com/2071-1050/10/4/1258)
32. [https://ieeexplore.ieee.org/document/9091027/](https://ieeexplore.ieee.org/document/9091027/)
33. [https://www.mdpi.com/2076-3417/12/19/9510](https://www.mdpi.com/2076-3417/12/19/9510)
34. [https://www.zte.com.cn/global/about/magazine/zte-communications/2017/4/en_222/466307.html](https://www.zte.com.cn/global/about/magazine/zte-communications/2017/4/en_222/466307.html)
35. [https://www.academia.edu/93978947/Scalable_Distributed_Computing_Hierarchy_Cloud_Fog_and_Dew_Computing](https://www.academia.edu/93978947/Scalable_Distributed_Computing_Hierarchy_Cloud_Fog_and_Dew_Computing)
36. [https://www.mdpi.com/2313-7673/10/3/143](https://www.mdpi.com/2313-7673/10/3/143)
37. [https://dl.acm.org/doi/fullHtml/10.1145/3486221](https://dl.acm.org/doi/fullHtml/10.1145/3486221)
38. [https://durham-repository.worktribe.com/preview/1249307/34978.pdf](https://durham-repository.worktribe.com/preview/1249307/34978.pdf)
39. [https://pubs.acs.org/doi/abs/10.1021/acsami.1c16609](https://pubs.acs.org/doi/abs/10.1021/acsami.1c16609)
40. [https://www.academia.edu/65802614/Cloud_Fog_Dew_and_Smart_Dust_Platform_for_Environmental_Analysis](https://www.academia.edu/65802614/Cloud_Fog_Dew_and_Smart_Dust_Platform_for_Environmental_Analysis)
41. [https://www.sec.gov/Archives/edgar/data/1872302/000121390025031065/ea0235323-20f_nanolabs.htm](https://www.sec.gov/Archives/edgar/data/1872302/000121390025031065/ea0235323-20f_nanolabs.htm)
42. [https://www.sec.gov/Archives/edgar/data/2066116/0002066116-25-000002-index.htm](https://www.sec.gov/Archives/edgar/data/2066116/0002066116-25-000002-index.htm)
43. [https://www.sec.gov/Archives/edgar/data/2066440/0002066440-25-000001-index.htm](https://www.sec.gov/Archives/edgar/data/2066440/0002066440-25-000001-index.htm)
44. [https://www.sec.gov/Archives/edgar/data/2065541/0002065541-25-000001-index.htm](https://www.sec.gov/Archives/edgar/data/2065541/0002065541-25-000001-index.htm)
45. [https://www.sec.gov/Archives/edgar/data/2061845/0002061845-25-000001-index.htm](https://www.sec.gov/Archives/edgar/data/2061845/0002061845-25-000001-index.htm)
46. [https://www.sec.gov/Archives/edgar/data/1652958/000168316825003051/edgemode_i10k-123124.htm](https://www.sec.gov/Archives/edgar/data/1652958/000168316825003051/edgemode_i10k-123124.htm)
47. [https://library.matanauniversity.ac.id/ojs/index.php/marka/article/view/249](https://library.matanauniversity.ac.id/ojs/index.php/marka/article/view/249)
48. [http://library.matanauniversity.ac.id/ojs/index.php/marka/article/view/192](http://library.matanauniversity.ac.id/ojs/index.php/marka/article/view/192)
49. [https://services.igi-global.com/resolvedoi/resolve.aspx?doi=10.4018/IJACI.2021100108](https://services.igi-global.com/resolvedoi/resolve.aspx?doi=10.4018/IJACI.2021100108)
50. [https://journal.hmjournals.com/index.php/JAIMLNN/article/view/4036](https://journal.hmjournals.com/index.php/JAIMLNN/article/view/4036)
51. [https://ejurnal.itenas.ac.id/index.php/terracotta/article/view/8544](https://ejurnal.itenas.ac.id/index.php/terracotta/article/view/8544)
52. [https://ieeexplore.ieee.org/document/9717894/](https://ieeexplore.ieee.org/document/9717894/)
53. [https://dl.acm.org/doi/abs/10.1007/s42979-021-00521-y](https://dl.acm.org/doi/abs/10.1007/s42979-021-00521-y)
54. [https://www.supermicro.com/en/glossary/fog-computing](https://www.supermicro.com/en/glossary/fog-computing)
55. [https://irep.ntu.ac.uk/id/eprint/41818/1/1393289_Frincu.pdf](https://irep.ntu.ac.uk/id/eprint/41818/1/1393289_Frincu.pdf)
56. [https://www.mdpi.com/2078-2489/11/6/303](https://www.mdpi.com/2078-2489/11/6/303)
57. [https://www.scribd.com/document/416053340/fog](https://www.scribd.com/document/416053340/fog)
58. [https://www.sec.gov/Archives/edgar/data/1710350/000101376225000307/ea0233723-10k_bitdigit.htm](https://www.sec.gov/Archives/edgar/data/1710350/000101376225000307/ea0233723-10k_bitdigit.htm)
59. [https://www.sec.gov/Archives/edgar/data/1046179/000119312525083423/d896993d20f.htm](https://www.sec.gov/Archives/edgar/data/1046179/000119312525083423/d896993d20f.htm)
60. [https://www.sec.gov/Archives/edgar/data/1964789/000155837024011968/hut-20240630x10q.htm](https://www.sec.gov/Archives/edgar/data/1964789/000155837024011968/hut-20240630x10q.htm)
61. [https://www.sec.gov/Archives/edgar/data/1144879/000114487924000216/apld-20240531.htm](https://www.sec.gov/Archives/edgar/data/1144879/000114487924000216/apld-20240531.htm)
62. [https://www.sec.gov/Archives/edgar/data/1964789/000155837024008203/hut-20240331x10q.htm](https://www.sec.gov/Archives/edgar/data/1964789/000155837024008203/hut-20240331x10q.htm)
63. [https://www.sec.gov/Archives/edgar/data/50863/000005086324000010/intc-20231230.htm](https://www.sec.gov/Archives/edgar/data/50863/000005086324000010/intc-20231230.htm)
64. [https://www.scpe.org/index.php/scpe/article/view/2224](https://www.scpe.org/index.php/scpe/article/view/2224)
65. [https://ieeexplore.ieee.org/document/10707220/](https://ieeexplore.ieee.org/document/10707220/)
66. [https://digitaltwin1.org/articles/4-7/v1](https://digitaltwin1.org/articles/4-7/v1)
67. [https://www.scitepress.org/DigitalLibrary/Link.aspx?doi=10.5220/0012977500003825](https://www.scitepress.org/DigitalLibrary/Link.aspx?doi=10.5220/0012977500003825)
68. [https://ieeexplore.ieee.org/document/10815810/](https://ieeexplore.ieee.org/document/10815810/)
69. [https://ieeexplore.ieee.org/document/10900838/](https://ieeexplore.ieee.org/document/10900838/)
70. [https://en.wikipedia.org/wiki/Edge_computing](https://en.wikipedia.org/wiki/Edge_computing)
71. [https://utimaco.com/news/blog-posts/edge-fog-cloud](https://utimaco.com/news/blog-posts/edge-fog-cloud)
72. [https://www.mdpi.com/1999-5903/17/1/22](https://www.mdpi.com/1999-5903/17/1/22)
73. [https://ijcaonline.org/archives/volume186/number29/development-of-edge-fog-and-cloud-computing-for-health-monitoring-using-raspberry-pi-as-fog-device-and-iot-sensors-as-edge-devices/](https://ijcaonline.org/archives/volume186/number29/development-of-edge-fog-and-cloud-computing-for-health-monitoring-using-raspberry-pi-as-fog-device-and-iot-sensors-as-edge-devices/)
74. [https://www.linkedin.com/pulse/cloud-computing-fog-now-mist-martin-ma-mba-med-gdm-scpm-pmp](https://www.linkedin.com/pulse/cloud-computing-fog-now-mist-martin-ma-mba-med-gdm-scpm-pmp)
75. [https://www.linkedin.com/pulse/unveiling-synergy-how-cloud-edge-fog-computing-data-bansal--mj39c](https://www.linkedin.com/pulse/unveiling-synergy-how-cloud-edge-fog-computing-data-bansal--mj39c)
76. [https://www.sec.gov/Archives/edgar/data/2066824/000206682425000002/vaneckbnbetfs-1.htm](https://www.sec.gov/Archives/edgar/data/2066824/000206682425000002/vaneckbnbetfs-1.htm)
77. [https://www.sec.gov/Archives/edgar/data/1829311/000168316825004278/bitmine_424b4.htm](https://www.sec.gov/Archives/edgar/data/1829311/000168316825004278/bitmine_424b4.htm)
78. [https://www.sec.gov/Archives/edgar/data/1829311/000168316825004030/bitmine_s1a3.htm](https://www.sec.gov/Archives/edgar/data/1829311/000168316825004030/bitmine_s1a3.htm)
79. [https://www.sec.gov/Archives/edgar/data/2041869/000199937125007760/solana-s1a_061325.htm](https://www.sec.gov/Archives/edgar/data/2041869/000199937125007760/solana-s1a_061325.htm)
80. [https://www.sec.gov/Archives/edgar/data/1296774/000141057825000945/ncty-20241231x20f.htm](https://www.sec.gov/Archives/edgar/data/1296774/000141057825000945/ncty-20241231x20f.htm)
81. [https://www.sec.gov/Archives/edgar/data/1829311/000168316825002385/bitmine_s1a2.htm](https://www.sec.gov/Archives/edgar/data/1829311/000168316825002385/bitmine_s1a2.htm)
82. [https://www.medra.org/servlet/aliasResolver?alias=iospressISSNISBN&issn=0927-5452&volume=19&spage=212](https://www.medra.org/servlet/aliasResolver?alias=iospressISSNISBN&issn=0927-5452&volume=19&spage=212)
83. [https://link.springer.com/10.1007/s10723-020-09518-y](https://link.springer.com/10.1007/s10723-020-09518-y)
84. [https://www.epj-conferences.org/10.1051/epjconf/202429503005](https://www.epj-conferences.org/10.1051/epjconf/202429503005)
85. [https://ieeexplore.ieee.org/document/8671629/](https://ieeexplore.ieee.org/document/8671629/)
86. [https://www.degruyter.com/document/doi/10.1515/eng-2017-0042/html](https://www.degruyter.com/document/doi/10.1515/eng-2017-0042/html)
87. [https://scienceunited.org/doc/pearc_20.pdf](https://scienceunited.org/doc/pearc_20.pdf)
88. [https://glennsqlperformance.com/2020/03/30/foldinghome-tips-and-tricks/](https://glennsqlperformance.com/2020/03/30/foldinghome-tips-and-tricks/)
89. [https://www.scitepress.org/Papers/2019/77333/77333.pdf](https://www.scitepress.org/Papers/2019/77333/77333.pdf)
90. [https://en.wikipedia.org/wiki/Folding@home](https://en.wikipedia.org/wiki/Folding@home)
91. [https://indico.cern.ch/event/1379525/contributions/5979694/attachments/2867842/5020151/BOINC-toPublish.pdf](https://indico.cern.ch/event/1379525/contributions/5979694/attachments/2867842/5020151/BOINC-toPublish.pdf)
92. [https://www.sec.gov/Archives/edgar/data/64463/000164117225001756/form10-k.htm](https://www.sec.gov/Archives/edgar/data/64463/000164117225001756/form10-k.htm)
93. [https://www.sec.gov/Archives/edgar/data/1964789/000155837025006845/hut-20250331x10q.htm](https://www.sec.gov/Archives/edgar/data/1964789/000155837025006845/hut-20250331x10q.htm)
94. [https://hut8.com/high-performance-computing/](https://hut8.com/high-performance-computing/)
95. [https://hut8.com](https://hut8.com/)
96. [https://hut8.io](https://hut8.io/)
97. [https://hut8.io/sample-page/](https://hut8.io/sample-page/)
98. [https://ca.linkedin.com/showcase/hut-8-hpc/](https://ca.linkedin.com/showcase/hut-8-hpc/)
99. [https://www.jsa.net/applied-digital-targets-major-growth-with-5-billion-funding-for-hpc-business-segment/](https://www.jsa.net/applied-digital-targets-major-growth-with-5-billion-funding-for-hpc-business-segment/)
100. [https://cointelegraph.com/news/hut8-relocates-6-400-rigs-sees-growth-in-ai-high-performance-computing](https://cointelegraph.com/news/hut8-relocates-6-400-rigs-sees-growth-in-ai-high-performance-computing)
101. [https://new.abb.com/news/detail/126792/abb-and-applied-digital-accelerate-ai-ready-data-centers](https://new.abb.com/news/detail/126792/abb-and-applied-digital-accelerate-ai-ready-data-centers)
102. [https://www.sec.gov/Archives/edgar/data/1907982/000190798225000060/qbts-20241231.htm](https://www.sec.gov/Archives/edgar/data/1907982/000190798225000060/qbts-20241231.htm)
103. [https://www.sec.gov/Archives/edgar/data/1861974/000186197425000004/exc-20241231.htm](https://www.sec.gov/Archives/edgar/data/1861974/000186197425000004/exc-20241231.htm)
104. [https://www.sec.gov/Archives/edgar/data/1907982/000190798225000101/qbts-20250520.htm](https://www.sec.gov/Archives/edgar/data/1907982/000190798225000101/qbts-20250520.htm)
105. [https://www.sec.gov/Archives/edgar/data/1819974/000181997425000010/skyt-20241229.htm](https://www.sec.gov/Archives/edgar/data/1819974/000181997425000010/skyt-20241229.htm)
106. [https://ojs.studiespublicacoes.com.br/ojs/index.php/sees/article/view/6976](https://ojs.studiespublicacoes.com.br/ojs/index.php/sees/article/view/6976)
107. [https://www.frontiersin.org/article/10.3389/fchem.2020.575786/full](https://www.frontiersin.org/article/10.3389/fchem.2020.575786/full)
108. [http://www.dbpia.co.kr/Journal/ArticleDetail/NODE01754504](http://www.dbpia.co.kr/Journal/ArticleDetail/NODE01754504)
109. [https://ieeexplore.ieee.org/document/8587006/](https://ieeexplore.ieee.org/document/8587006/)
110. [http://openurl.ingenta.com/content/xref?genre=article&issn=1533-4880&volume=14&issue=2&spage=1859](http://openurl.ingenta.com/content/xref?genre=article&issn=1533-4880&volume=14&issue=2&spage=1859)
111. [https://www.mist.com/resources/mist-platform-solution-brief/](https://www.mist.com/resources/mist-platform-solution-brief/)
112. [https://scpe.org/index.php/scpe/CFP_SI_SDC](https://scpe.org/index.php/scpe/CFP_SI_SDC)
113. [https://www.techtarget.com/searchnetworking/news/450401110/Mist-introduces-new-analytics-capabilities-for-wireless](https://www.techtarget.com/searchnetworking/news/450401110/Mist-introduces-new-analytics-capabilities-for-wireless)
114. [https://www.sec.gov/Archives/edgar/data/1859392/000162828025028640/galaxydigitalinc-capitalra.htm](https://www.sec.gov/Archives/edgar/data/1859392/000162828025028640/galaxydigitalinc-capitalra.htm)
115. [https://www.sec.gov/Archives/edgar/data/64463/000164117225012098/forms-1.htm](https://www.sec.gov/Archives/edgar/data/64463/000164117225012098/forms-1.htm)
116. [https://www.mdpi.com/2073-431X/11/7/114/pdf?version=1657714751](https://www.mdpi.com/2073-431X/11/7/114/pdf?version=1657714751)
117. [https://arxiv.org/pdf/2203.07425.pdf](https://arxiv.org/pdf/2203.07425.pdf)
118. [https://arxiv.org/pdf/2203.02544.pdf](https://arxiv.org/pdf/2203.02544.pdf)
119. [https://pmc.ncbi.nlm.nih.gov/articles/PMC10168006/](https://pmc.ncbi.nlm.nih.gov/articles/PMC10168006/)
120. [https://pmc.ncbi.nlm.nih.gov/articles/PMC8464028/](https://pmc.ncbi.nlm.nih.gov/articles/PMC8464028/)
121. [https://www.deic.dk/EuroCC2/Access-to-supercomputing](https://www.deic.dk/EuroCC2/Access-to-supercomputing)
122. [https://byjus.com/biology/difference-between-fog-and-mist/](https://byjus.com/biology/difference-between-fog-and-mist/)
123. [https://www.youtube.com/watch?v=WX4Delxf7RA](https://www.youtube.com/watch?v=WX4Delxf7RA)
124. [https://www.britannica.com/science/mist-weather](https://www.britannica.com/science/mist-weather)
125. [https://www.sec.gov/Archives/edgar/data/1645590/000164559024000139/hpe-20241031.htm](https://www.sec.gov/Archives/edgar/data/1645590/000164559024000139/hpe-20241031.htm)
126. [https://link.springer.com/10.1007/s10586-022-03606-2](https://link.springer.com/10.1007/s10586-022-03606-2)
127. [https://link.springer.com/10.1007/s10586-024-04794-9](https://link.springer.com/10.1007/s10586-024-04794-9)
128. [https://ieeexplore.ieee.org/document/10394272/](https://ieeexplore.ieee.org/document/10394272/)
129. [https://ieeexplore.ieee.org/document/10250784/](https://ieeexplore.ieee.org/document/10250784/)
130. [https://www.springerprofessional.de/dew-computing/25999570](https://www.springerprofessional.de/dew-computing/25999570)
131. [https://www.sciencedirect.com/science/article/abs/pii/S2542660519302616](https://www.sciencedirect.com/science/article/abs/pii/S2542660519302616)
132. [https://link.springer.com/10.1007/s42979-021-00521-y](https://link.springer.com/10.1007/s42979-021-00521-y)
133. [https://ieeexplore.ieee.org/document/8409103/](https://ieeexplore.ieee.org/document/8409103/)
134. [http://ieeexplore.ieee.org/document/8251002/](http://ieeexplore.ieee.org/document/8251002/)
135. [https://pmc.ncbi.nlm.nih.gov/articles/PMC11041998/](https://pmc.ncbi.nlm.nih.gov/articles/PMC11041998/)
136. [http://www.ronpub.com/OJCC_2015v2i1n03_Skala.pdf](http://www.ronpub.com/OJCC_2015v2i1n03_Skala.pdf)
137. [https://www.bohrium.com/paper-details/applied-sciences-vol-12-pages-9510-scalable-dew-computing/817351059335806976-96529](https://www.bohrium.com/paper-details/applied-sciences-vol-12-pages-9510-scalable-dew-computing/817351059335806976-96529)
138. [https://dl.acm.org/doi/10.1145/3486221](https://dl.acm.org/doi/10.1145/3486221)
139. [https://www.sciencedirect.com/science/article/abs/pii/S0167739X17329722](https://www.sciencedirect.com/science/article/abs/pii/S0167739X17329722)
140. [https://ietresearch.onlinelibrary.wiley.com/doi/10.1049/gtd2.13286](https://ietresearch.onlinelibrary.wiley.com/doi/10.1049/gtd2.13286)
141. [https://www.e3s-conferences.org/10.1051/e3sconf/202458306012](https://www.e3s-conferences.org/10.1051/e3sconf/202458306012)
142. [https://link.springer.com/10.1007/s11334-022-00458-2](https://link.springer.com/10.1007/s11334-022-00458-2)
143. [https://ieeexplore.ieee.org/document/10558844/](https://ieeexplore.ieee.org/document/10558844/)
144. [https://www.sec.gov/Archives/edgar/data/1826397/000164117225002955/form10-k.htm](https://www.sec.gov/Archives/edgar/data/1826397/000164117225002955/form10-k.htm)
145. [https://www.semanticscholar.org/paper/39e7d4da0ea70b6c822302fb183806140fcdf4b6](https://www.semanticscholar.org/paper/39e7d4da0ea70b6c822302fb183806140fcdf4b6)
146. [http://ieeexplore.ieee.org/document/6009056/](http://ieeexplore.ieee.org/document/6009056/)
147. [https://www.semanticscholar.org/paper/31ff8eeaa86040b00b8b7fc954185becc9562be5](https://www.semanticscholar.org/paper/31ff8eeaa86040b00b8b7fc954185becc9562be5)
148. [http://crm.ics.org.ru/journal/article/2330/](http://crm.ics.org.ru/journal/article/2330/)
149. [https://en.wikipedia.org/wiki/Volunteer_computing](https://en.wikipedia.org/wiki/Volunteer_computing)
150. [https://indico.cern.ch/event/1338689/contributions/6011881/attachments/2951444/5188199/CHEP2024_CMS_at_home-final.pdf](https://indico.cern.ch/event/1338689/contributions/6011881/attachments/2951444/5188199/CHEP2024_CMS_at_home-final.pdf)
151. [https://www.semanticscholar.org/paper/7d5102eb37fca25996cb1f98017aaf14bda013c9](https://www.semanticscholar.org/paper/7d5102eb37fca25996cb1f98017aaf14bda013c9)
152. [http://link.springer.com/10.1007/978-3-030-43222-5_15](http://link.springer.com/10.1007/978-3-030-43222-5_15)
153. [http://ieeexplore.ieee.org/document/7967185/](http://ieeexplore.ieee.org/document/7967185/)
154. [https://dl.acm.org/doi/10.1145/3149412.3149418](https://dl.acm.org/doi/10.1145/3149412.3149418)
155. [https://www.semanticscholar.org/paper/22f65f99bf53ef3e5552b180768576c98e1796f6](https://www.semanticscholar.org/paper/22f65f99bf53ef3e5552b180768576c98e1796f6)
156. [https://link.springer.com/10.1007/s12652-020-02255-w](https://link.springer.com/10.1007/s12652-020-02255-w)
157. [http://link.springer.com/10.1007/978-3-319-25876-8_18](http://link.springer.com/10.1007/978-3-319-25876-8_18)
158. [http://ieeexplore.ieee.org/document/7973456/](http://ieeexplore.ieee.org/document/7973456/)
159. [https://link.springer.com/10.1007/978-1-0716-3449-3_8](https://link.springer.com/10.1007/978-1-0716-3449-3_8)
160. [http://journals.sagepub.com/doi/10.1177/1550147719868669](http://journals.sagepub.com/doi/10.1177/1550147719868669)
161. [https://onlinelibrary.wiley.com/doi/10.1002/admi.201400480](https://onlinelibrary.wiley.com/doi/10.1002/admi.201400480)
162. [https://scispace.com/pdf/application-of-user-dew-agent-in-hybrid-computing-5am7t70dzl.pdf](https://scispace.com/pdf/application-of-user-dew-agent-in-hybrid-computing-5am7t70dzl.pdf)
163. [https://www.sciencedirect.com/science/article/abs/pii/S0021979719313682](https://www.sciencedirect.com/science/article/abs/pii/S0021979719313682)
164. [http://arxiv.org/pdf/1907.10890.pdf](http://arxiv.org/pdf/1907.10890.pdf)
165. [http://arxiv.org/pdf/2405.00016.pdf](http://arxiv.org/pdf/2405.00016.pdf)
166. [https://academic.oup.com/nsr/article-pdf/3/1/36/7434200/nww001.pdf](https://academic.oup.com/nsr/article-pdf/3/1/36/7434200/nww001.pdf)
167. [https://arxiv.org/pdf/1702.06335.pdf](https://arxiv.org/pdf/1702.06335.pdf)
168. [https://www.iotworldtoday.com/quantum/hybrid-quantum-hpc-supercomputing-platform-goes-online](https://www.iotworldtoday.com/quantum/hybrid-quantum-hpc-supercomputing-platform-goes-online)
169. [https://dug.com/supercomputing-puts-toxic-forever-chemicals-to-the-sword/](https://dug.com/supercomputing-puts-toxic-forever-chemicals-to-the-sword/)
170. [https://ec.europa.eu/newsroom/document.cfm?doc_id=42306](https://ec.europa.eu/newsroom/document.cfm?doc_id=42306)
171. [https://www.igi-global.com/pdf.aspx?tid=273413&ptid=261119&ctid=17&t=Appendix%3A+Birds+of+a+Feather&isxn=9781799871569](https://www.igi-global.com/pdf.aspx?tid=273413&ptid=261119&ctid=17&t=Appendix%3A+Birds+of+a+Feather&isxn=9781799871569)
172. https://www.perplexity.ai/search/research-question-s-problem-st-GZmN3spNQdqU4bGTqBvETw

[[Existing Decentralized Compute Marketplaces and Protocols 2 - Comparative Analysis of Top Volunteer and Decentralized Computing Frameworks]]


