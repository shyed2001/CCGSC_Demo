
[[#Read Related Cluster Computing and VMs-]]

# Creating VM Clusters for Cluster Computing over LAN, WAN, MAN and Internet

To build a virtual‐machine (VM) cluster across multiple PCs—whether on a LAN, across a WAN or MAN, or even over the Internet—you can use one of three leading approaches:

1. **Proxmox VE Cluster** (KVM + corosync)
    
2. **OpenStack Multi-Region** (Nova/Neutron federation)
    
3. **vSAN Stretched Cluster** (VMware vSphere/vSAN)
    

Each solution has different network, storage, and high-availability requirements. Below is a comparison and step-by-step guide for each.

## 1. Proxmox VE Cluster

## 1.1 Overview

- Built-in clustering via corosync and a shared filesystem (`/etc/pve`).
    
- KVM-based VMs; supports live migration, HA, fencing.
    

## 1.2 Prerequisites

- **Nodes**: ≥2 PCs with Proxmox VE installed (Debian-based).
    
- **Network**:
    
    - **Corosync network** (low-latency interface): ideally <5 ms RTT.
        
    - **VM/data network** (bridged).
        
    - **Management** (optional separate VLAN).
        
- **Storage**: local, NFS, CEPH, or iSCSI—but identical on all nodes for live migration.
    

## 1.3 Configure Separate Corosync Network

1. In Proxmox GUI, go to **Datacenter → Cluster → Edit → Network** and add your corosync CIDR.
    
2. Physically connect each node’s dedicated NIC to a switch (even a dumb switch) on that subnet.
    
3. On each node, ensure `/etc/pve/corosync.conf` lists only that interface under the totem `bindnetaddr`.
    
4. Restart cluster services:
    
    bash
    
    `systemctl restart corosync pve-cluster`
    
5. Verify latency:
    
    bash
    
    `ping -c 10 <other-node-corosync-IP>`
    

## 1.4 Create and Join Cluster

On Node A:

bash

`pvecm create my-cluster`

On Node B, C, …:

bash

`pvecm add <NodeA-corosync-IP> \   --password <root-pwd>`

Verify quorum:

bash

`pvecm status`

## 1.5 Live Migration & HA

- Define VM HA policies under **Datacenter → HA**.
    
- Migrate VMs via GUI or:
    
    bash
    
    `qm migrate <vmid> <target-node>`
    

## 2. OpenStack Multi-Region

## 2.1 Overview

- Separate OpenStack deployments (“regions”) share a common Keystone and Horizon.
    
- Nebula of Nova/Neutron services across regions.
    
- VM placement and networking via VPN or L3 federation (e.g., Tricircle).
    

## 2.2 Prerequisites

- Three physical servers per region at minimum:
    
    1. **Controller(s)**
        
    2. **Compute**
        
    3. **Network services**
        
- **Networking**:
    
    - **Underlying WAN** between regions (IPsec/VPN, QoS).
        
    - **FlatDHCP** or VLANs for tenant networks.
        
- **Storage**: Ceph or NFS shared in each region.
    

## 2.3 Configure Regions in DevStack/Kolla-Ansible

- In `globals.yml`:
    
    text
    
    `openstack_region_name: "RegionOne" multiple_regions_names:   - "RegionOne"  - "RegionTwo"`
    
- Ensure Keystone endpoint definitions include region tags.
    
- Deploy each region independently, pointing to the shared Keystone.
    

## 2.4 Networking Between Regions

- Use **Neutron L3 Agent routing** or **VPNaaS** to connect tenant networks.
    
- For true L2 between regions (e.g., VM migration), use **Tricircle** or overlay (VXLAN/MPLS).
    

## 3. VMware vSAN Stretched Cluster

## 3.1 Overview

- Two active data sites + one witness host.
    
- Synchronous replication of VM data between data sites.
    
- Witness sits in a third site (can use lower-bandwidth link).
    

## 3.2 Prerequisites

- ≥3 ESXi hosts:
    
    - **Site A**: ≥1 host + vSAN datastore devices
        
    - **Site B**: ≥1 host + vSAN devices
        
    - **Witness**: 1 host (only metadata)
        
- **Networking**:
    
    - **vSAN network**: Layer 2 or 3 between data sites. Latency ≤5 ms RTT.
        
    - **Witness connectivity**: can be higher latency over L3.
        
    - **Management**: L2 or L3 across all three sites.
        
- **Storage**: local SSD/HDD on each data site.
    

## 3.3 Configuration (vSphere Client)

1. **Cluster Setup**: Create a new cluster.
    
2. **Fault Domains**:
    
    - Site A → Preferred domain
        
    - Site B → Secondary domain
        
    - Witness → Witness domain
        
3. **Disks**: Claim cache/capacity devices on data hosts.
    
4. **Witness**: Assign one VMkernel adapter for vSAN.
    
5. **Review & Complete**.
    

## 3.4 Validation

- Check **vSAN Health**.
    
- Run vSAN performance service with synthetic tests.
    
- Ensure no resynchronizations.
    

## Comparison and When to Use

|Aspect|Proxmox VE|OpenStack Multi-Region|vSAN Stretched Cluster|
|---|---|---|---|
|Scale|Small–medium clusters (≤50 nodes)|Large clouds (100s regions)|Enterprise SAN across ≤2 sites|
|Network latency|<5 ms corosync RTT|WAN latency (tuned)|≤5 ms vSAN; witness can be higher latency|
|Storage|Local, NFS, Ceph|Ceph, Swift, NFS|vSAN storage on host disks|
|HA & Quorum|Yes (with qdevice or 3 nodes)|Yes with regional failover|Yes across data sites|
|Deployment effort|Minutes–hours|Days–weeks|Hours–days|
|Use case|Lab, SMB, HPC|Service provider, telco|Mission-critical enterprise VM storage|

## Best Practices

- **Separate networks**: Dedicate NICs/VLANs for cluster control, VM traffic, storage, and management.
    
- **Monitor latency**: Use `ping`, `corosync-cmapctl`, `vsanPerfQuery`.
    
- **Use qdevice** for 2-node Proxmox clusters to maintain quorum.
    
- **Test failover**: Migrate a VM and simulate site loss.
    
- **Validate storage health**: ceph health, vSAN health checks.
    

This comprehensive overview enables you to choose and deploy the right VM-clustering approach across any network topology—from your LAN to geographically distributed sites—ensuring high availability, performance, and manageability.

1. [https://www.sec.gov/Archives/edgar/data/1346287/000168316825002575/cluster_i10k-123124.htm](https://www.sec.gov/Archives/edgar/data/1346287/000168316825002575/cluster_i10k-123124.htm)
2. [https://www.sec.gov/Archives/edgar/data/1346287/000168316825004933/cluster_i10q-033125.htm](https://www.sec.gov/Archives/edgar/data/1346287/000168316825004933/cluster_i10q-033125.htm)
3. [https://www.sec.gov/Archives/edgar/data/1052354/000095017025043325/ck0001052354-20241231.htm](https://www.sec.gov/Archives/edgar/data/1052354/000095017025043325/ck0001052354-20241231.htm)
4. [https://www.sec.gov/Archives/edgar/data/1862935/000164117225004557/form10-k.htm](https://www.sec.gov/Archives/edgar/data/1862935/000164117225004557/form10-k.htm)
5. [https://www.sec.gov/Archives/edgar/data/2001794/000121390025033795/ea0238904-424b4_concorde.htm](https://www.sec.gov/Archives/edgar/data/2001794/000121390025033795/ea0238904-424b4_concorde.htm)
6. [https://www.sec.gov/Archives/edgar/data/2074782/0002074782-25-000001-index.htm](https://www.sec.gov/Archives/edgar/data/2074782/0002074782-25-000001-index.htm)
7. [https://www.sec.gov/Archives/edgar/data/1862935/000164117225017215/forms-1a.htm](https://www.sec.gov/Archives/edgar/data/1862935/000164117225017215/forms-1a.htm)
8. [https://www.tandfonline.com/doi/full/10.1080/03772063.2022.2060872](https://www.tandfonline.com/doi/full/10.1080/03772063.2022.2060872)
9. [http://link.springer.com/10.1007/3-540-47840-X_19](http://link.springer.com/10.1007/3-540-47840-X_19)
10. [http://ieeexplore.ieee.org/document/5280678/](http://ieeexplore.ieee.org/document/5280678/)
11. [https://link.springer.com/10.1007/s11277-023-10564-4](https://link.springer.com/10.1007/s11277-023-10564-4)
12. [https://link.springer.com/10.1007/s11227-021-04235-z](https://link.springer.com/10.1007/s11227-021-04235-z)
13. [https://www.tandfonline.com/doi/full/10.1080/0954898X.2024.2369137](https://www.tandfonline.com/doi/full/10.1080/0954898X.2024.2369137)
14. [https://pos.sissa.it/434/002](https://pos.sissa.it/434/002)
15. [http://link.springer.com/10.1007/s10586-019-02966-6](http://link.springer.com/10.1007/s10586-019-02966-6)
16. [https://onlinelibrary.wiley.com/doi/10.1155/2021/5586521](https://onlinelibrary.wiley.com/doi/10.1155/2021/5586521)
17. [https://www.youtube.com/watch?v=at4J2bVPdwc](https://www.youtube.com/watch?v=at4J2bVPdwc)
18. [https://docs.it4i.cz/software/tools/virtualization/](https://docs.it4i.cz/software/tools/virtualization/)
19. [https://www.brainkart.com/article/Virtual-Clusters-and-Resource-Management_11343/](https://www.brainkart.com/article/Virtual-Clusters-and-Resource-Management_11343/)
20. [https://www.youtube.com/watch?v=SAP8IxFI7uE](https://www.youtube.com/watch?v=SAP8IxFI7uE)
21. [https://nordvpn.com/cybersecurity/glossary/virtual-machine-cluster/](https://nordvpn.com/cybersecurity/glossary/virtual-machine-cluster/)
22. [https://www.usenix.org/legacyurl/multi-site-virtual-cluster-system-wide-area-networks](https://www.usenix.org/legacyurl/multi-site-virtual-cluster-system-wide-area-networks)
23. [https://www.reddit.com/r/Proxmox/comments/wkrf44/can_i_use_2_computers_to_run_the_same_vm/](https://www.reddit.com/r/Proxmox/comments/wkrf44/can_i_use_2_computers_to_run_the_same_vm/)
24. [https://www.vcluster.com](https://www.vcluster.com/)
25. [https://www.ibm.com/think/topics/cluster-computing](https://www.ibm.com/think/topics/cluster-computing)
26. [https://stackoverflow.com/questions/26660560/how-to-run-vmware-over-cluster-of-pcs](https://stackoverflow.com/questions/26660560/how-to-run-vmware-over-cluster-of-pcs)
27. [https://www.nutanix.com/info/virtualization/server-virtualization](https://www.nutanix.com/info/virtualization/server-virtualization)
28. [https://www.gigabyte.com/jp/Article/cluster-computing-an-advanced-form-of-distributed-computing-a-tech-guide-by-gigabyte](https://www.gigabyte.com/jp/Article/cluster-computing-an-advanced-form-of-distributed-computing-a-tech-guide-by-gigabyte)
29. [https://superuser.com/questions/956895/using-multiple-computers-as-a-processing-and-data-storage-cluster](https://superuser.com/questions/956895/using-multiple-computers-as-a-processing-and-data-storage-cluster)
30. [https://www.studocu.com/in/document/bharati-vidyapeeth-university/cloud-computing/system-modeling-clustering-and-virtualization/43114558](https://www.studocu.com/in/document/bharati-vidyapeeth-university/cloud-computing/system-modeling-clustering-and-virtualization/43114558)
31. [https://www.geeksforgeeks.org/computer-networks/an-overview-of-cluster-computing/](https://www.geeksforgeeks.org/computer-networks/an-overview-of-cluster-computing/)
32. [https://www.sec.gov/Archives/edgar/data/1582961/000158296122000010/docn-20211231.htm](https://www.sec.gov/Archives/edgar/data/1582961/000158296122000010/docn-20211231.htm)
33. [https://www.sec.gov/Archives/edgar/data/1582961/000158296124000031/docn-20231231.htm](https://www.sec.gov/Archives/edgar/data/1582961/000158296124000031/docn-20231231.htm)
34. [https://www.sec.gov/Archives/edgar/data/1462056/000119312521327209/d62601d424b4.htm](https://www.sec.gov/Archives/edgar/data/1462056/000119312521327209/d62601d424b4.htm)
35. [https://www.sec.gov/Archives/edgar/data/1462056/000119312521301141/d62601ds1.htm](https://www.sec.gov/Archives/edgar/data/1462056/000119312521301141/d62601ds1.htm)
36. [https://www.sec.gov/Archives/edgar/data/1769628/000119312525067651/d899798d424b4.htm](https://www.sec.gov/Archives/edgar/data/1769628/000119312525067651/d899798d424b4.htm)
37. [https://www.sec.gov/Archives/edgar/data/1462056/000119312521322225/d62601ds1a.htm](https://www.sec.gov/Archives/edgar/data/1462056/000119312521322225/d62601ds1a.htm)



## Read Related Cluster Computing and VMs-
[[Cluster Computing]]
[[ClusterComputingQA]]
[[CVM Clustered Virtual Machines]]
[[Cluster Computing Page 2]]
[[Cluster Computing Software]]
[[VM Containers]]
[[Virtual Machines]]
[[Parallel Virtual Machine PVM]]
[[Sandbox VMs]]

