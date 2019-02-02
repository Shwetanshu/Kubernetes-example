## Kubernetes Architecture Diagram

![alt text](https://github.com/Shwetanshu/Kubernetes-example/blob/master/Architecture/Architecture_Diagram.png)

Kubernetes Architecture has two nodes : Master Node & Worker Node

Masters - Acts as the primary control plane for Kubernetes. Masters are responsible at a minimum for running the API Server, scheduler, and cluster controller. They commonly also manage storing cluster state, cloud-provider specific components and other cluster essential services. 

Nodes - Are the ‘workers’ of a Kubernetes cluster. They run a minimal agent that manages the node itself, and are tasked with executing workloads as designated by the master. 

# Master Node Components

Master Node is the Control Plane of Kubernetes Cluster. Following are the main components of control plane :

1. kube-apiserver
	Gate keeper for everything in kubernetes
	EVERYTHING interacts with kubernetes through the apiserver
2. etcd
	Distributed storage back end for kubernetes
	The apiserver is the only thing that talks to it
3. kube-controller-manager
	The home of the core controllers
4. kube-scheduler
	handes placement
