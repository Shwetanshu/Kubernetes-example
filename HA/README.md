# The anatomy of HA cluster setup

There are few common guidelines for HA cluster setup:

- We need a replicated, distributed etcd storage layer.
- We need to replicate the apiserver across several machines and front them with a load-balancer.
- We need to replicate the controllers and schedulers and set them up for leader-election.
- We need to configure the (worker) nodes’ kubelet and kube-proxy to access the apiserver through the loadbalancer.

The replication factor depends on the level of availability one need to achieve. With three sets of master components the cluster can tolerate a failure of one master node since, in that case, etcd requires two live members to be able to form a quorum (a node majority) and continue working. Below table provides the fault-tolerance of different etcd cluster sizes.

CLUSTER SIZE|MAJORITY|FAILURE TOLERANCE
---|---|---
1|1|0
2|2|0
3|2|1
4|3|1
5|3|2
6|4|2
7|4|3
8|5|3
9|5|4

---
HA cluster with a replication factor of three could be realized as illustrated in the following diagram:

![alt text](https://github.com/Shwetanshu/Kubernetes-example/blob/master/img/HA_Cluster.png)

- etcd replicates the cluster state to all master nodes. Therefore, to lose all data, all three nodes must experience simultaneous disk failures. Although unlikely, one may want to make the storage layer even more reliable by using a separate disk that is decoupled from the lifecycle of the machine/VM. You can also use a RAID setup to mirror disks, and finally set up etcd to take periodical backups.
- The etcd replicas can be placed on separate, dedicated machines to isolate them and give them dedicated machine resources for improved performance.
- The load-balancer must monitor the health of its apiservers and only forward traffic to live servers.
- Spread masters across data centers to increase the overall uptime of the cluster. If the masters are placed in different zones, the cluster can tolerate the outage of an entire availability zone.
- (Worker) node kubelets and kube-proxys must access the apiserver via the load-balancer to not tie them to a particular master instance.
- The loadbalancer must not become a single point of failure. Most cloud providers can offer fault-tolerant loadbalancer services. For on-premise setups, one can make use of an active/passive nginx/HAProxy setup with a virtual/floating IP that is re-assigned by keepalived when failover is required.
