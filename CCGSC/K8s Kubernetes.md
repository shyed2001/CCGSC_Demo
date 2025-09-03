


[How does Kubernetes create a Pod?](https://www.youtube.com/watch?v=BgrQ16r84pM)


Two type of Nodes

3 Control Node
    efcd
    Scheduler
     Controller Manager 
Many Compute Nodes
	kubelet
	 Computer Runtime Engine CRI
	 Kube-proxy	



kubelet does a few things: 
1. register compute nodes
2. report status 
3. start/stop workload

Steps in creating a new pod: 1. A user submits a new configuration with kubectl to kube-API Server 2. Kube-API Server writes the configuration to etcd 3. Scheduler compares the configuration to actual state 4. Scheduler informs kube-API Server of which compute node(s) to schedule the workload 5. Kube-API Server requests corresponding Kubelets to create the new pod 6. Kubelet creates a new pod 7. Kubelets report latest status to kube-API Server 8. Kube-API Server updates the actual state in etcd

1. After Kube-API server returned "created" response to user, the pod's state will be "pending" 
2. After scheduler set the node for that pod, Pod's state will be "creating" 
3. After Kubelet created the pod, state will be "running" 
4. If the pod is failing and restarting, state will be "Crash loop back off"


![[Pasted image 20250705170602.png]]




![[Pasted image 20250705170651.png]]







![[Pasted image 20250705170842.png]]







![[Pasted image 20250705171021.png]]





![[Pasted image 20250705171157.png]]








