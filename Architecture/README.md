# Kubernetes Architecture Diagram

![alt text](https://github.com/Shwetanshu/Kubernetes-example/blob/master/img/Architecture_Diagram.png)

Kubernetes Architecture has two nodes : Master Node & Worker Node

- Master Node - Acts as the primary control plane for Kubernetes. Masters are responsible at a minimum for running the API Server, scheduler, and cluster controller. They commonly also manage storing cluster state, cloud-provider specific components and other cluster essential services. 

- Worker Nodes - Are the ‘workers’ of a Kubernetes cluster. They run a minimal agent that manages the node itself, and are tasked with executing workloads as designated by the master. 

## Master Node Components

Master Node is the Control Plane of Kubernetes Cluster. Following are the main components of control plane :

1. kube-apiserver

   Gate keeper for everything in kubernetes.<br/>
   EVERYTHING interacts with kubernetes through the apiserver.

2. etcd

   Distributed storage back end for kubernetes.<br/>
   The apiserver is the only thing that talks to it.

3. kube-controller-manager

   The home of the core controllers.Logically, each controller is a separate process, but to reduce complexity, they are all compiled into a single binary and run in a single process.These controllers include:
      - Node Controller
      - Replication Controller
      - Endpoints Controller
      - Service Account & Token Controllers

4. kube-scheduler

   Handles placement.

5. cloud-controller-manager

   Runs controllers that interact with the underlying cloud providers. The cloud-controller-manager binary is an alpha feature introduced in Kubernetes release 1.6.
   cloud-controller-manager allows cloud vendors code and the Kubernetes code to evolve independent of each other.Following controllers have cloud provider dependencies:
      - Node Controller
      - Route Controller
      - Service Controller
      - Volume Controller

## Worker Node Components

Worker node component runs on every cluster node. These includes:

1. Container Runtime : The container runtime is the software that is responsible for running containers. Kubernetes supports several runtimes: Docker, rkt, runc and any OCI runtime-spec implementation.

2. kubelet : An agent that runs on each node in the cluster. It makes sure that containers are running in a pod. Executes containers (pods) on the node as dictated by the control plane’s scheduling, and ensures the health of those pods (for example, by restarting failed pods)

3. kube-proxy : a network proxy/loadbalancer that implements the Service abstraction. It programs the iptables rules on
the node to redirect service IP requests to one of its registered backend pods.

## Addons

Addons are pods and services that implement cluster features.Namespaced addon objects are created in the kube-system namespace. For list of available addons please refer [Addons](https://kubernetes.io/docs/concepts/cluster-administration/addons/)

### Another HLD for Kubernetes :

![alt text](https://github.com/Shwetanshu/Kubernetes-example/blob/master/img/K8s_HLD.png)
