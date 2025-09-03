

# Dynamic Resource Allocation for Virtual Machines

**Main Takeaway:** Modern hypervisors and cloud platforms support truly dynamic, on-the-fly adjustment of VM CPU, RAM, storage—and increasingly GPU—resources without downtime. This “vertical scaling” is realized via hot-add/hot-plug, paravirtualized device drivers, and memory ballooning, complemented by live migration over LAN/WAN to rebalance loads across hosts.

## 1. CPU & RAM Vertical Scaling

## 1.1 Hot-Add / Hot-Plug

- **CPU Hot-Plug:** Add vCPUs to a running VM via hypervisor APIs.
    
    - VMware vSphere: Enable “CPU Hot-Add” (disabled by default) before power-on; works in Windows Server 2019/2022 and modern RHEL kernels[1](https://www.starwindsoftware.com/blog/hot-add-ram-hot-plug-vcpus-vsphere-vms-different-environments/).
        
    - Hyper-V: Enable “Virtual CPU hot plug” in VM settings; supported by guest OSes certified for hot-add[2](https://www.techtarget.com/searchvmware/definition/VMware-DRS).
        
- **Memory Hot-Add:** Similarly, add RAM without reboot.
    
    - VMware: “Memory Hot-Add” feature with guest OS support; typical overhead <3%[1](https://www.starwindsoftware.com/blog/hot-add-ram-hot-plug-vcpus-vsphere-vms-different-environments/).
        
    - Hyper-V: “Memory hot add” in VM settings; supported on Gen2 VMs[3](https://techdocs.broadcom.com/us/en/vmware-cis/vsphere/vsphere/7-0/vsphere-single-host-management-vmware-host-client-7-0/virtual-machine-management-with-the-vsphere-host-client-vSphereSingleHostManagementVMwareHostClient/configuring-virtual-machines-in-the-vsphere-host-client-vSphereSingleHostManagementVMwareHostClient/virtual-memory-configuration-vSphereSingleHostManagementVMwareHostClient/change-memory-hot-add-settings-vSphereSingleHostManagementVMwareHostClient.html).
        
- **Limitations:**
    
    - Hot-remove unsupported; vNUMA disabled when CPU hot-add enabled[1](https://www.starwindsoftware.com/blog/hot-add-ram-hot-plug-vcpus-vsphere-vms-different-environments/).
        
    - Guest OS must have drivers and licensing that permit dynamic plugging.
        

## 1.2 Paravirtualized Memory & Ballooning

- **Balloon Drivers (virtio-balloon):** Guest driver “inflates” to release unused pages to hypervisor.
    
- **Paravirtual Mem (virtio-mem):** Direct, DMA-safe memory de/inflation (e.g., HyperAlloc) with 10–360× faster shrinking than ballooning, enabling sub-second memory scale-down[4](https://dl.acm.org/doi/10.1145/3689031.3717484).
    

## 2. GPU Virtualization & Dynamic Allocation

## 2.1 GPU Passthrough vs vGPU

- **DirectDevice Passthrough:** Exclusive GPU assignment via IOMMU; no sharing, but native performance.
    
- **vGPU / Mediated-Pass-Through:** Hypervisor driver multiplexes GPU among VMs (NVIDIA vGPU, AMD MxGPU), offering near-native throughput and live-migration compatibility[5](https://www.semanticscholar.org/paper/9448b2ffd88e36dadc3a4bb3cb64e2594689fdb7)[6](https://dl.acm.org/doi/10.5555/2663510.2663512).
    

## 2.2 GPU Paravirtualization (PV-GPU)

- **PV-GPU in Windows WDDM 2.4+:** Guest UMD hooks to host GPU KMD over VMBus, no guest KMD; shares one GPU across many VMs[7](https://learn.microsoft.com/en-us/windows-hardware/drivers/display/gpu-paravirtualization).
    
- **PV-GPU in Linux/KVM:** Custom host driver (e.g., GPUvm) marshals CUDA/OpenGL calls to host GPU while allowing live migration[8](http://ieeexplore.ieee.org/document/7349172/).
    

## 2.3 Hot-Plugging GPUs

- **Hyper-V GPU Partitioning:** Use `Add-VMGpuPartitionAdapter` to expose a fraction of GPU to VM; supports dynamic reconfiguration pre- and post-boot[7](https://learn.microsoft.com/en-us/windows-hardware/drivers/display/gpu-paravirtualization).
    
- **Limitations:** Not all GPUs/drivers support dynamic reallocation; typically requires VM reboot or live-migration to rebalance GPU share.
    

## 3. Storage Vertical Scaling

## 3.1 Online Disk Resize

- **Hyper-V 2012 R2+:** Extend or shrink VHDX on a running VM if attached via SCSI; edit virtual disk wizard in Hyper-V Manager[9](https://us.informatiweb-pro.net/virtualization/vmware/vmware-vsphere-6-7-hot-add-resources-vcpu-ram-to-vms.html)[10](https://www.diskpart.com/server-2012/resize-online-vm-hard-disk-hyper-v-2012-r2-1004.html).
    
- **VMware vSphere:** `vmkfstools -X` or vSphere GUI Edit Settings → Increase Disk; then expand partition inside guest OS[11](https://www.vinchin.com/vm-tips/vmware-increase-disk-size.html).
    

## 3.2 Shared & Distributed Storage

- **Scale-Out Filesystems (GlusterFS):** Automatic data replication, linear I/O scaling by adding nodes; supports live VM migration on shared storage[12](http://www.atlantis-press.com/php/paper-details.php?id=21708).
    
- **Software-Defined Storage:** CSI volumes hot-attached to VMs/containers; Kubernetes supports hotplug volumes with reconcilers[13](https://kubevirt.io/user-guide/storage/hotplug_volumes/).
    

## 4. Dynamic Load Balancing & Live Migration

- **Live Migration (LAN/WAN):**
    
    - VMware vMotion and Hyper-V Live Migration move running VMs transparently within LAN, and over WAN with overlay tunnels (VXLAN/GRE) preserving IP connectivity[14](https://www.diva-portal.org/smash/get/diva2:828770/FULLTEXT01.pdf)[15](https://www.sciencedirect.com/science/article/abs/pii/S0045790622005249).
        
- **Distributed Resource Scheduler (DRS):** Automatically places and migrates VMs across hosts based on CPU/memory load and affinity rules[2](https://www.techtarget.com/searchvmware/definition/VMware-DRS)[16](https://www.nakivo.com/blog/what-is-vmware-drs-cluster/).
    

## 5. Orchestration & Automation

- **Cloud APIs & Tools:**
    
    - vSphere API, Hyper-V WMI/PowerShell, AWS/GCP/AKS instance types allow on-demand scaling via REST/CLI.
        
- **Autoscaling Policies:**
    
    - Trigger VM scale-up on utilization thresholds (e.g., CPU > 80% add vCPU), via CloudWatch/Azure Monitor and Infrastructure as Code (Terraform/ARM).
        

## 6. Use Cases & Considerations

|Resource|Use Case|Mechanism|Notes|
|---|---|---|---|
|CPU|Bursty compute jobs|Hot-Add vCPU; live migration|Ensure vNUMA compatibility[1](https://www.starwindsoftware.com/blog/hot-add-ram-hot-plug-vcpus-vsphere-vms-different-environments/)|
|RAM|In-memory caches, analytics|Hot-Add RAM; ballooning; HyperAlloc batching|Paravirtual > balloon for speed[4](https://dl.acm.org/doi/10.1145/3689031.3717484)|
|GPU|AI training/inference|vGPU, PV-GPU, passthrough|Licensing and driver support|
|Storage|Growing datasets|Online disk resize; hotplug volumes|Requires guest FS resize tools|
|Network|Off-load and redirection|DPU/SmartNIC paravirtualization|NVMe-over-Fabric hotplug support|

**Performance Overhead:**

- CPU hot-add: ~1–6% throughput loss[1](https://www.starwindsoftware.com/blog/hot-add-ram-hot-plug-vcpus-vsphere-vms-different-environments/).
    
- Memory hot-add: negligible when OS manages new pages efficiently[1](https://www.starwindsoftware.com/blog/hot-add-ram-hot-plug-vcpus-vsphere-vms-different-environments/).
    
- vGPU: typically <10% loss vs native[6](https://dl.acm.org/doi/10.5555/2663510.2663512).
    

**Security & Isolation:**

- Shared-kernel vs hypervisor boundary: GPU/vGPU drivers increasing attack surface; enforce isolation via SR-IOV and IOMMU.
    

## Citations

[12](http://www.atlantis-press.com/php/paper-details.php?id=21708) The Performance Analysis of GlusterFS In Virtual Storage [12](http://www.atlantis-press.com/php/paper-details.php?id=21708).  
[14](https://www.diva-portal.org/smash/get/diva2:828770/FULLTEXT01.pdf) A Performance Study of VM Live Migration over the WAN [14](https://www.diva-portal.org/smash/get/diva2:828770/FULLTEXT01.pdf).  
[1](https://www.starwindsoftware.com/blog/hot-add-ram-hot-plug-vcpus-vsphere-vms-different-environments/) Hot-Add RAM and CPU in vSphere: Guest OS Compatibility[1](https://www.starwindsoftware.com/blog/hot-add-ram-hot-plug-vcpus-vsphere-vms-different-environments/).  
[2](https://www.techtarget.com/searchvmware/definition/VMware-DRS) What is VMware DRS (Distributed Resource Scheduler)?[2](https://www.techtarget.com/searchvmware/definition/VMware-DRS).  
[16](https://www.nakivo.com/blog/what-is-vmware-drs-cluster/) VMware DRS (Distributed Resource Scheduler) Explained [16](https://www.nakivo.com/blog/what-is-vmware-drs-cluster/).  
[15](https://www.sciencedirect.com/science/article/abs/pii/S0045790622005249) Live virtual machine migration: A survey… [15](https://www.sciencedirect.com/science/article/abs/pii/S0045790622005249).  
[9](https://us.informatiweb-pro.net/virtualization/vmware/vmware-vsphere-6-7-hot-add-resources-vcpu-ram-to-vms.html) Hot add resources (vCPU/RAM) to VMs on VMware vSphere 6.7 [9](https://us.informatiweb-pro.net/virtualization/vmware/vmware-vsphere-6-7-hot-add-resources-vcpu-ram-to-vms.html).  
[3](https://techdocs.broadcom.com/us/en/vmware-cis/vsphere/vsphere/7-0/vsphere-single-host-management-vmware-host-client-7-0/virtual-machine-management-with-the-vsphere-host-client-vSphereSingleHostManagementVMwareHostClient/configuring-virtual-machines-in-the-vsphere-host-client-vSphereSingleHostManagementVMwareHostClient/virtual-memory-configuration-vSphereSingleHostManagementVMwareHostClient/change-memory-hot-add-settings-vSphereSingleHostManagementVMwareHostClient.html) Change Memory Hot Add Settings [3](https://techdocs.broadcom.com/us/en/vmware-cis/vsphere/vsphere/7-0/vsphere-single-host-management-vmware-host-client-7-0/virtual-machine-management-with-the-vsphere-host-client-vSphereSingleHostManagementVMwareHostClient/configuring-virtual-machines-in-the-vsphere-host-client-vSphereSingleHostManagementVMwareHostClient/virtual-memory-configuration-vSphereSingleHostManagementVMwareHostClient/change-memory-hot-add-settings-vSphereSingleHostManagementVMwareHostClient.html).  
[13](https://kubevirt.io/user-guide/storage/hotplug_volumes/) Hotplug Volumes [13](https://kubevirt.io/user-guide/storage/hotplug_volumes/).  
[8](http://ieeexplore.ieee.org/document/7349172/) GPUvm: GPU Virtualization at the Hypervisor [8](http://ieeexplore.ieee.org/document/7349172/).  
[4](https://dl.acm.org/doi/10.1145/3689031.3717484) HyperAlloc: Efficient VM Memory De/Inflation via Hypervisor-Shared… [4](https://dl.acm.org/doi/10.1145/3689031.3717484).  
[5](https://www.semanticscholar.org/paper/9448b2ffd88e36dadc3a4bb3cb64e2594689fdb7) A Full GPU Virtualization Solution with Mediated Pass-Through [5](https://www.semanticscholar.org/paper/9448b2ffd88e36dadc3a4bb3cb64e2594689fdb7).  
[6](https://dl.acm.org/doi/10.5555/2663510.2663512) GPU virtualization for high performance general purpose computing… [6](https://dl.acm.org/doi/10.5555/2663510.2663512).  
[7](https://learn.microsoft.com/en-us/windows-hardware/drivers/display/gpu-paravirtualization) GPU paravirtualization – Windows drivers [7](https://learn.microsoft.com/en-us/windows-hardware/drivers/display/gpu-paravirtualization).

1. [https://www.starwindsoftware.com/blog/hot-add-ram-hot-plug-vcpus-vsphere-vms-different-environments/](https://www.starwindsoftware.com/blog/hot-add-ram-hot-plug-vcpus-vsphere-vms-different-environments/)
2. [https://www.techtarget.com/searchvmware/definition/VMware-DRS](https://www.techtarget.com/searchvmware/definition/VMware-DRS)
3. [https://techdocs.broadcom.com/us/en/vmware-cis/vsphere/vsphere/7-0/vsphere-single-host-management-vmware-host-client-7-0/virtual-machine-management-with-the-vsphere-host-client-vSphereSingleHostManagementVMwareHostClient/configuring-virtual-machines-in-the-vsphere-host-client-vSphereSingleHostManagementVMwareHostClient/virtual-memory-configuration-vSphereSingleHostManagementVMwareHostClient/change-memory-hot-add-settings-vSphereSingleHostManagementVMwareHostClient.html](https://techdocs.broadcom.com/us/en/vmware-cis/vsphere/vsphere/7-0/vsphere-single-host-management-vmware-host-client-7-0/virtual-machine-management-with-the-vsphere-host-client-vSphereSingleHostManagementVMwareHostClient/configuring-virtual-machines-in-the-vsphere-host-client-vSphereSingleHostManagementVMwareHostClient/virtual-memory-configuration-vSphereSingleHostManagementVMwareHostClient/change-memory-hot-add-settings-vSphereSingleHostManagementVMwareHostClient.html)
4. [https://dl.acm.org/doi/10.1145/3689031.3717484](https://dl.acm.org/doi/10.1145/3689031.3717484)
5. [https://www.semanticscholar.org/paper/9448b2ffd88e36dadc3a4bb3cb64e2594689fdb7](https://www.semanticscholar.org/paper/9448b2ffd88e36dadc3a4bb3cb64e2594689fdb7)
6. [https://dl.acm.org/doi/10.5555/2663510.2663512](https://dl.acm.org/doi/10.5555/2663510.2663512)
7. [https://learn.microsoft.com/en-us/windows-hardware/drivers/display/gpu-paravirtualization](https://learn.microsoft.com/en-us/windows-hardware/drivers/display/gpu-paravirtualization)
8. [http://ieeexplore.ieee.org/document/7349172/](http://ieeexplore.ieee.org/document/7349172/)
9. [https://us.informatiweb-pro.net/virtualization/vmware/vmware-vsphere-6-7-hot-add-resources-vcpu-ram-to-vms.html](https://us.informatiweb-pro.net/virtualization/vmware/vmware-vsphere-6-7-hot-add-resources-vcpu-ram-to-vms.html)
10. [https://www.diskpart.com/server-2012/resize-online-vm-hard-disk-hyper-v-2012-r2-1004.html](https://www.diskpart.com/server-2012/resize-online-vm-hard-disk-hyper-v-2012-r2-1004.html)
11. [https://www.vinchin.com/vm-tips/vmware-increase-disk-size.html](https://www.vinchin.com/vm-tips/vmware-increase-disk-size.html)
12. [http://www.atlantis-press.com/php/paper-details.php?id=21708](http://www.atlantis-press.com/php/paper-details.php?id=21708)
13. [https://kubevirt.io/user-guide/storage/hotplug_volumes/](https://kubevirt.io/user-guide/storage/hotplug_volumes/)
14. [https://www.diva-portal.org/smash/get/diva2:828770/FULLTEXT01.pdf](https://www.diva-portal.org/smash/get/diva2:828770/FULLTEXT01.pdf)
15. [https://www.sciencedirect.com/science/article/abs/pii/S0045790622005249](https://www.sciencedirect.com/science/article/abs/pii/S0045790622005249)
16. [https://www.nakivo.com/blog/what-is-vmware-drs-cluster/](https://www.nakivo.com/blog/what-is-vmware-drs-cluster/)
17. [https://www.sec.gov/Archives/edgar/data/1993400/000164117225017162/form10-k.htm](https://www.sec.gov/Archives/edgar/data/1993400/000164117225017162/form10-k.htm)
18. [https://www.sec.gov/Archives/edgar/data/1471781/000173112225000487/e6454_10k.htm](https://www.sec.gov/Archives/edgar/data/1471781/000173112225000487/e6454_10k.htm)
19. [https://www.sec.gov/Archives/edgar/data/1993400/000164117225003009/form424b4.htm](https://www.sec.gov/Archives/edgar/data/1993400/000164117225003009/form424b4.htm)
20. [https://www.sec.gov/Archives/edgar/data/2073520/0002073520-25-000001-index.htm](https://www.sec.gov/Archives/edgar/data/2073520/0002073520-25-000001-index.htm)
21. [https://www.sec.gov/Archives/edgar/data/2058562/0002058562-25-000001-index.htm](https://www.sec.gov/Archives/edgar/data/2058562/0002058562-25-000001-index.htm)
22. [https://www.sec.gov/Archives/edgar/data/1078271/000095017024098129/extr-20240630.htm](https://www.sec.gov/Archives/edgar/data/1078271/000095017024098129/extr-20240630.htm)
23. [https://www.sec.gov/Archives/edgar/data/1066119/000162828025008767/viv-20241231.htm](https://www.sec.gov/Archives/edgar/data/1066119/000162828025008767/viv-20241231.htm)
24. [https://arxiv.org/abs/2504.20937](https://arxiv.org/abs/2504.20937)
25. [https://www.semanticscholar.org/paper/2934a0505bd2d17de8de9d768a491ce2808dc676](https://www.semanticscholar.org/paper/2934a0505bd2d17de8de9d768a491ce2808dc676)
26. [https://www.semanticscholar.org/paper/1ac96374ef9736e309ba4764aa6535f8070fd181](https://www.semanticscholar.org/paper/1ac96374ef9736e309ba4764aa6535f8070fd181)
27. [http://link.springer.com/10.1007/s10619-014-7168-4](http://link.springer.com/10.1007/s10619-014-7168-4)
28. [https://www.semanticscholar.org/paper/8b493f492162403472c2022534279c13bc876ac7](https://www.semanticscholar.org/paper/8b493f492162403472c2022534279c13bc876ac7)
29. [https://www.semanticscholar.org/paper/c45cb287df8bde799b1b3ba9705b3f6cc9be2773](https://www.semanticscholar.org/paper/c45cb287df8bde799b1b3ba9705b3f6cc9be2773)
30. [https://www.semanticscholar.org/paper/b59464043f8bde925346a9197534dc85ab9044f6](https://www.semanticscholar.org/paper/b59464043f8bde925346a9197534dc85ab9044f6)
31. [https://docs.plusserver.com/en/compute/pluscloudvmware/reference/compute/hot_add/](https://docs.plusserver.com/en/compute/pluscloudvmware/reference/compute/hot_add/)
32. [https://techdocs.broadcom.com/us/en/vmware-cis/vsphere/vsphere/8-0/vsphere-networking-8-0/network-io-control/bandwidth-allocation-for-virtual-machine-traffic/bandwidth-allocation-for-virtual-machine-traffi-3.html](https://techdocs.broadcom.com/us/en/vmware-cis/vsphere/vsphere/8-0/vsphere-networking-8-0/network-io-control/bandwidth-allocation-for-virtual-machine-traffic/bandwidth-allocation-for-virtual-machine-traffi-3.html)
33. [https://www.redhat.com/en/topics/virtualization/what-is-live-migration](https://www.redhat.com/en/topics/virtualization/what-is-live-migration)
34. [https://www.nakivo.com/blog/vmware-vsphere-resources-hotadd-hotplug-explained/](https://www.nakivo.com/blog/vmware-vsphere-resources-hotadd-hotplug-explained/)
35. [https://www.altaro.com/vmware/vsphere-distributed-switch-guide/](https://www.altaro.com/vmware/vsphere-distributed-switch-guide/)
36. [https://dl.acm.org/doi/10.1145/1188455.1188758](https://dl.acm.org/doi/10.1145/1188455.1188758)
37. [https://www.altaro.com/vmware/vmware-hot-add/](https://www.altaro.com/vmware/vmware-hot-add/)
38. [https://frankdenneman.nl/2013/02/28/distribution-of-resources-based-on-shares-in-a-resource-pool-environment/](https://frankdenneman.nl/2013/02/28/distribution-of-resources-based-on-shares-in-a-resource-pool-environment/)
39. [https://people.computing.clemson.edu/~jmarty/papers/vtdc07.pdf](https://people.computing.clemson.edu/~jmarty/papers/vtdc07.pdf)
40. [https://www.sec.gov/Archives/edgar/data/2009175/0001104659-25-024949-index.htm](https://www.sec.gov/Archives/edgar/data/2009175/0001104659-25-024949-index.htm)
41. [https://www.sec.gov/Archives/edgar/data/2000112/0002039266-24-000004-index.htm](https://www.sec.gov/Archives/edgar/data/2000112/0002039266-24-000004-index.htm)
42. [https://www.sec.gov/Archives/edgar/data/1682745/000095017025065808/vrrm-20250331.htm](https://www.sec.gov/Archives/edgar/data/1682745/000095017025065808/vrrm-20250331.htm)
43. [https://www.sec.gov/Archives/edgar/data/1169561/000116956125000034/cvlt-20250331.htm](https://www.sec.gov/Archives/edgar/data/1169561/000116956125000034/cvlt-20250331.htm)
44. [https://www.sec.gov/Archives/edgar/data/1570585/000157058525000114/lbtya-20250331.htm](https://www.sec.gov/Archives/edgar/data/1570585/000157058525000114/lbtya-20250331.htm)
45. [https://www.sec.gov/Archives/edgar/data/1570585/000157058525000021/lbtya-20241231.htm](https://www.sec.gov/Archives/edgar/data/1570585/000157058525000021/lbtya-20241231.htm)
46. [https://arxiv.org/abs/2411.12893](https://arxiv.org/abs/2411.12893)
47. [https://ieeexplore.ieee.org/document/8509436/](https://ieeexplore.ieee.org/document/8509436/)
48. [https://dl.acm.org/doi/10.1145/3429357.3430523](https://dl.acm.org/doi/10.1145/3429357.3430523)
49. [https://ieeexplore.ieee.org/document/7164911/](https://ieeexplore.ieee.org/document/7164911/)
50. [https://www.semanticscholar.org/paper/b69382e95bbf9bd9f141bbb7e0d9ab2bd8353e2b](https://www.semanticscholar.org/paper/b69382e95bbf9bd9f141bbb7e0d9ab2bd8353e2b)
51. [https://www.semanticscholar.org/paper/83379736ff1fd0025f0c61530598be36d769c4a4](https://www.semanticscholar.org/paper/83379736ff1fd0025f0c61530598be36d769c4a4)
52. [https://www.semanticscholar.org/paper/be4a3d9945a80dc079eb60db51b213c988a25059](https://www.semanticscholar.org/paper/be4a3d9945a80dc079eb60db51b213c988a25059)
53. [http://www.hindawi.com/journals/bmri/2013/939460/](http://www.hindawi.com/journals/bmri/2013/939460/)
54. [https://www.spiceworks.com/tech/cloud/articles/horizontal-vs-vertical-cloud-scaling/](https://www.spiceworks.com/tech/cloud/articles/horizontal-vs-vertical-cloud-scaling/)
55. [https://www.altaro.com/hyper-v/how-to-resize-online-virtual-machine-hard-disks-in-hyper-v-2012-r2/](https://www.altaro.com/hyper-v/how-to-resize-online-virtual-machine-hard-disks-in-hyper-v-2012-r2/)
56. [https://www.site24x7.com/learn/vertical-vs-horizontal-scaling-in-the-cloud.html](https://www.site24x7.com/learn/vertical-vs-horizontal-scaling-in-the-cloud.html)
57. [https://www.bdrsuite.com/blog/what-is-vmware-hot-add-hot-plug-how-will-it-impact-numa/](https://www.bdrsuite.com/blog/what-is-vmware-hot-add-hot-plug-how-will-it-impact-numa/)
58. [https://help.communicationsquare.com/article/113-how-to-increase-disk-space-of-vm-in-hyperv](https://help.communicationsquare.com/article/113-how-to-increase-disk-space-of-vm-in-hyperv)
59. [https://openmetal.io/docs/edu/openstack/horizontal-scaling-vs-vertical-scaling/](https://openmetal.io/docs/edu/openstack/horizontal-scaling-vs-vertical-scaling/)
60. [https://www.nakivo.com/blog/increase-disk-size-hyper-v-complete-guide/](https://www.nakivo.com/blog/increase-disk-size-hyper-v-complete-guide/)
61. [https://www.digitalocean.com/resources/articles/horizontal-scaling-vs-vertical-scaling](https://www.digitalocean.com/resources/articles/horizontal-scaling-vs-vertical-scaling)
62. [https://docs.redhat.com/en/documentation/red_hat_virtualization/4.0/html/virtual_machine_management_guide/cpu_hot_plug](https://docs.redhat.com/en/documentation/red_hat_virtualization/4.0/html/virtual_machine_management_guide/cpu_hot_plug)
63. [https://www.redhat.com/en/blog/resizing-storage-within-virtual-machines-in-red-hat-openshift-virtualization-version-4](https://www.redhat.com/en/blog/resizing-storage-within-virtual-machines-in-red-hat-openshift-virtualization-version-4)
64. [https://www.macrometa.com/distributed-data/vertical-scaling-vs-horizontal-scaling](https://www.macrometa.com/distributed-data/vertical-scaling-vs-horizontal-scaling)
65. [https://askubuntu.com/questions/764620/how-do-you-hotplug-enable-new-cpu-and-ram-in-a-virtual-machine](https://askubuntu.com/questions/764620/how-do-you-hotplug-enable-new-cpu-and-ram-in-a-virtual-machine)
66. [https://cloud.google.com/dataflow/docs/vertical-autoscaling](https://cloud.google.com/dataflow/docs/vertical-autoscaling)
67. [https://www.sec.gov/Archives/edgar/data/1769628/000119312525058309/d899798ds1a.htm](https://www.sec.gov/Archives/edgar/data/1769628/000119312525058309/d899798ds1a.htm)
68. [https://www.sec.gov/Archives/edgar/data/1769628/000119312525067651/d899798d424b4.htm](https://www.sec.gov/Archives/edgar/data/1769628/000119312525067651/d899798d424b4.htm)
69. [https://www.sec.gov/Archives/edgar/data/896493/000121465925005868/r4925210k.htm](https://www.sec.gov/Archives/edgar/data/896493/000121465925005868/r4925210k.htm)
70. [https://www.sec.gov/Archives/edgar/data/1769628/000119312525044231/d899798ds1.htm](https://www.sec.gov/Archives/edgar/data/1769628/000119312525044231/d899798ds1.htm)
71. [https://www.sec.gov/Archives/edgar/data/1769628/000119312525052207/d899798ds1a.htm](https://www.sec.gov/Archives/edgar/data/1769628/000119312525052207/d899798ds1a.htm)
72. [https://www.sec.gov/Archives/edgar/data/1394056/000095017025041974/oss-20241231.htm](https://www.sec.gov/Archives/edgar/data/1394056/000095017025041974/oss-20241231.htm)
73. [https://www.sec.gov/Archives/edgar/data/1861974/000186197425000004/exc-20241231.htm](https://www.sec.gov/Archives/edgar/data/1861974/000186197425000004/exc-20241231.htm)
74. [https://www.semanticscholar.org/paper/16e21e5c888a9cedb74ff89ef04d6fb1a911da25](https://www.semanticscholar.org/paper/16e21e5c888a9cedb74ff89ef04d6fb1a911da25)
75. [http://ieeexplore.ieee.org/document/7876385/](http://ieeexplore.ieee.org/document/7876385/)
76. [https://www.semanticscholar.org/paper/ec97e16a9ee20c90e7c65fc6dd4ddcd0098c6b3e](https://www.semanticscholar.org/paper/ec97e16a9ee20c90e7c65fc6dd4ddcd0098c6b3e)
77. [https://www.semanticscholar.org/paper/242958f4f63b96bfe0d9ee3bf4170404f07c247b](https://www.semanticscholar.org/paper/242958f4f63b96bfe0d9ee3bf4170404f07c247b)
78. [https://link.springer.com/10.1007/978-3-642-35473-1_20](https://link.springer.com/10.1007/978-3-642-35473-1_20)
79. [https://www.virtualizor.com/docs/professional-features/vertical-scaling](https://www.virtualizor.com/docs/professional-features/vertical-scaling)
80. [https://www.scribd.com/presentation/468074812/Dynamic-Resource-Allocation-Using-Virtual-Machines-for-Cloud-Computing-Environment](https://www.scribd.com/presentation/468074812/Dynamic-Resource-Allocation-Using-Virtual-Machines-for-Cloud-Computing-Environment)
81. [https://cwiki.apache.org/confluence/display/CLOUDSTACK/Dynamic+scaling+of+CPU+and+RAM](https://cwiki.apache.org/confluence/display/CLOUDSTACK/Dynamic+scaling+of+CPU+and+RAM)
82. [https://www.ijeat.org/wp-content/uploads/papers/v3i6/F3393083614.pdf](https://www.ijeat.org/wp-content/uploads/papers/v3i6/F3393083614.pdf)
83. [https://www.atlantic.net/gpu-server-hosting/gpu-virtualization-techniques-solutions-and-best-practices/](https://www.atlantic.net/gpu-server-hosting/gpu-virtualization-techniques-solutions-and-best-practices/)
84. [https://www.youtube.com/watch?v=PcU_qbMxR-I](https://www.youtube.com/watch?v=PcU_qbMxR-I)
85. [https://cloud.google.com/compute/docs/dynamic-resource-management](https://cloud.google.com/compute/docs/dynamic-resource-management)
86. [https://superuser.com/questions/1632822/how-do-i-enable-gpu-acceleration-on-new-hyper-v-virtual-machines-cant-use-rem](https://superuser.com/questions/1632822/how-do-i-enable-gpu-acceleration-on-new-hyper-v-virtual-machines-cant-use-rem)
87. [https://www.reddit.com/r/vmware/comments/1bn70fl/autoscale_vm_vmware/](https://www.reddit.com/r/vmware/comments/1bn70fl/autoscale_vm_vmware/)
88. [https://www.cs.cornell.edu/~weijia/papers/Skewness.pdf](https://www.cs.cornell.edu/~weijia/papers/Skewness.pdf)
89. [https://www.reddit.com/r/VFIO/comments/oinf4x/virtual_hardware_switches_hotplug_gpus_between_vms/](https://www.reddit.com/r/VFIO/comments/oinf4x/virtual_hardware_switches_hotplug_gpus_between_vms/)
90. [https://manage.togglebox.com/index.php?%2Fknowledgebase%2Farticle%2F79%2Fscaling-vm-cpu-ram%2F](https://manage.togglebox.com/index.php?%2Fknowledgebase%2Farticle%2F79%2Fscaling-vm-cpu-ram%2F)
91. [https://www.sciencedirect.com/science/article/pii/S1877050915004482](https://www.sciencedirect.com/science/article/pii/S1877050915004482)
92. [https://docs.nvidia.com/vgpu/18.0/index.html](https://docs.nvidia.com/vgpu/18.0/index.html)
93. [http://link.springer.com/10.1007/BF03289291](http://link.springer.com/10.1007/BF03289291)
94. [https://www.semanticscholar.org/paper/95340b6530e748c3428664d9d43ea3ccd6fc3d9c](https://www.semanticscholar.org/paper/95340b6530e748c3428664d9d43ea3ccd6fc3d9c)
95. [https://www.frontiersin.org/journals/high-performance-computing/articles/10.3389/fhpcp.2024.1417040/pdf](https://www.frontiersin.org/journals/high-performance-computing/articles/10.3389/fhpcp.2024.1417040/pdf)
96. [http://downloads.hindawi.com/journals/bmri/2013/939460.pdf](http://downloads.hindawi.com/journals/bmri/2013/939460.pdf)
97. [https://pmc.ncbi.nlm.nih.gov/articles/PMC3654629/](https://pmc.ncbi.nlm.nih.gov/articles/PMC3654629/)
98. [https://arxiv.org/html/2502.15738v1](https://arxiv.org/html/2502.15738v1)
99. [http://arxiv.org/pdf/1511.07658.pdf](http://arxiv.org/pdf/1511.07658.pdf)
100. [http://arxiv.org/pdf/2405.16283.pdf](http://arxiv.org/pdf/2405.16283.pdf)
101. [https://dl.acm.org/doi/pdf/10.1145/3639478.3640034](https://dl.acm.org/doi/pdf/10.1145/3639478.3640034)
102. [https://publications.eai.eu/index.php/sis/article/download/3254/2445](https://publications.eai.eu/index.php/sis/article/download/3254/2445)
103. [https://www.techscience.com/jiot/v3n4/46091/pdf](https://www.techscience.com/jiot/v3n4/46091/pdf)
104. [https://arxiv.org/pdf/2411.05309.pdf](https://arxiv.org/pdf/2411.05309.pdf)
105. [https://www.geeksforgeeks.org/operating-systems/virtualization-in-distributed-system/](https://www.geeksforgeeks.org/operating-systems/virtualization-in-distributed-system/)
106. [https://www.jstage.jst.go.jp/article/transinf/E96.D/12/E96.D_2663/_article](https://www.jstage.jst.go.jp/article/transinf/E96.D/12/E96.D_2663/_article)
107. [https://www.reddit.com/r/vmware/comments/1f5442k/cpu_hot_add_question/](https://www.reddit.com/r/vmware/comments/1f5442k/cpu_hot_add_question/)
108. [https://www.vmware.com/docs/vsphere6-drs-perf](https://www.vmware.com/docs/vsphere6-drs-perf)
109. [http://link.springer.com/10.1007/11942634](http://link.springer.com/10.1007/11942634)
110. [https://www.semanticscholar.org/paper/36f37e80809cb9b8327aadf2b61303eb3e7d6e69](https://www.semanticscholar.org/paper/36f37e80809cb9b8327aadf2b61303eb3e7d6e69)
111. [https://vfast.org/journals/index.php/VTCS/article/view/521](https://vfast.org/journals/index.php/VTCS/article/view/521)
112. [https://www.mdpi.com/2073-8994/13/3/508/pdf](https://www.mdpi.com/2073-8994/13/3/508/pdf)
113. [https://scholarworks.iu.edu/dspace/bitstream/2022/24567/1/Virtualized_GPU_Benchmarks_for_Deep_Learning.pdf](https://scholarworks.iu.edu/dspace/bitstream/2022/24567/1/Virtualized_GPU_Benchmarks_for_Deep_Learning.pdf)
114. [https://arxiv.org/pdf/2502.01909.pdf](https://arxiv.org/pdf/2502.01909.pdf)
115. [https://pureadmin.qub.ac.uk/ws/files/158833978/reano_ccpe2015_author.pdf](https://pureadmin.qub.ac.uk/ws/files/158833978/reano_ccpe2015_author.pdf)
116. [https://arxiv.org/pdf/2303.13803.pdf](https://arxiv.org/pdf/2303.13803.pdf)
117. [https://docs.oracle.com/en/virtualization/oracle-linux-virtualization-manager/admin/admin-hot-plug-devices.html](https://docs.oracle.com/en/virtualization/oracle-linux-virtualization-manager/admin/admin-hot-plug-devices.html)
118. [https://learn.microsoft.com/en-us/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/dn282284(v=ws.11)](https://learn.microsoft.com/en-us/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/dn282284\(v=ws.11\))
119. [http://ieeexplore.ieee.org/document/6427531/](http://ieeexplore.ieee.org/document/6427531/)
120. [http://link.springer.com/10.1007/s11227-013-1034-4](http://link.springer.com/10.1007/s11227-013-1034-4)
121. [https://arxiv.org/pdf/2005.07598.pdf](https://arxiv.org/pdf/2005.07598.pdf)
122. [https://www.mdpi.com/2076-3417/9/1/137/pdf](https://www.mdpi.com/2076-3417/9/1/137/pdf)
123. [https://arxiv.org/pdf/2201.09652.pdf](https://arxiv.org/pdf/2201.09652.pdf)
124. [https://www.mdpi.com/1424-8220/24/14/4649](https://www.mdpi.com/1424-8220/24/14/4649)
125. [https://fly.io/docs/launch/scale-machine/](https://fly.io/docs/launch/scale-machine/)
126. [https://arxiv.org/abs/2403.13619](https://arxiv.org/abs/2403.13619)
127. [https://documentation.ubuntu.com/server/how-to/graphics/gpu-virtualization-with-qemu-kvm/](https://documentation.ubuntu.com/server/how-to/graphics/gpu-virtualization-with-qemu-kvm/)
128. [https://learn.microsoft.com/en-us/azure/virtual-machine-scale-sets/virtual-machine-scale-sets-autoscale-overview](https://learn.microsoft.com/en-us/azure/virtual-machine-scale-sets/virtual-machine-scale-sets-autoscale-overview)
129. https://www.perplexity.ai/search/4s-vm-virtualization-hyper-v-v-503jnliYTnWQGHjBS4JFyg#2