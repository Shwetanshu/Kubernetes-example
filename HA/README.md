# The anatomy of HA cluster setup

There are few common guidelines for HA cluster setup:

- We need a replicated, distributed etcd storage layer.
- We need to replicate the apiserver across several machines and front them with a load-balancer.
- We need to replicate the controllers and schedulers and set them up for leader-election.
- We need to configure the (worker) nodes’ kubelet and kube-proxy to access the apiserver through the loadbalancer.

The replication factor depends on the level of availability one need to achieve. With three sets of master components the cluster can tolerate a failure of one master node since, in that case, etcd requires two live members to be able to form a quorum (a node majority) and continue working.

HA cluster with a replication factor of three could be realized as illustrated in the following diagram:

![alt text](https://github.com/Shwetanshu/Kubernetes-example/blob/master/img/"HA Cluster.png")
