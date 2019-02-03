# Kubernetes Architecture Diagram

![alt text](https://github.com/Shwetanshu/Kubernetes-example/blob/master/img/Architecture_Diagram.png)

Kubernetes Architecture has two nodes : Master Node & Worker Node

Masters - Acts as the primary control plane for Kubernetes. Masters are responsible at a minimum for running the API Server, scheduler, and cluster controller. They commonly also manage storing cluster state, cloud-provider specific components and other cluster essential services. 

Nodes - Are the ‘workers’ of a Kubernetes cluster. They run a minimal agent that manages the node itself, and are tasked with executing workloads as designated by the master. 

## Master Node Components

Master Node is the Control Plane of Kubernetes Cluster. Following are the main components of control plane :

1. kube-apiserver

   Gate keeper for everything in kubernetes<br/>
   EVERYTHING interacts with kubernetes through the apiserver

2. etcd

	Distributed storage back end for kubernetes<br/>
	The apiserver is the only thing that talks to it

3. kube-controller-manager

	The home of the core controllers

4. kube-scheduler

	handles placement

## Worker Node Components

Worker node component runs on every cluster node. These includes:

1. container runtime : such as Docker, to execute containers on the node

2. kubelet : executes containers (pods) on the node as dictated by the control plane’s scheduling, and ensures the
health of those pods (for example, by restarting failed pods)

3. kube-proxy : a network proxy/loadbalancer that implements the Service abstraction. It programs the iptables rules on
the node to redirect service IP requests to one of its registered backend pods.

### Another HLD for Kubernetes :

![alt text](https://github.com/Shwetanshu/Kubernetes-example/blob/master/img/K8s_HLD.png)
