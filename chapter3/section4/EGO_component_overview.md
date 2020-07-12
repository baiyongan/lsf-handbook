# EGO 组件概览

可以使用 LSF 启用 EGO，以提供系统基础结构来控制和管理群集资源。

就像在一台计算机上运行的操作系统聚合并虚拟化物理资源，并将其分配给应用程序一样，EGO 可以在分布式环境中执行类似的功能。

EGO 管理逻辑和物理资源，并支持所有形式的应用程序。 EGO 管理资源的供应，使资源可供应用程序使用。

主机可以分为两类：管理主机和计算主机。 管理主机为群集提供专门服务，而计算主机运行用户作业负载。

## 管理节点

Management hosts provide both cluster and workload management services within the cluster, and are not expected to run workload for users. The master host, all master candidate hosts, and session manager hosts must be management hosts. Other management hosts include the host running the data loaders and data purger for the reporting feature.

Management hosts all run on the same operating system: all Windows, all UNIX, or all Linux.

- Master host

  The master host is the first host installed in the cluster. The resource manager (**vemkd**) for the cluster resides on this host. The master host controls the rest of the hosts in the cluster and is the interface to the clients of the cluster.

- Master candidates

  There is only one master host at a time. If the master host should fail, another host automatically takes over the master host role. Hosts that can act as the master are called master candidates.

- Session manager host

  One or more management hosts run session managers. There is one session manager per available slot on a management host. There is one session manager per application.

## 计算节点

Compute hosts are those hosts in the cluster that provide computing resources to consumers. A cluster may contain any number of compute hosts, but must have at least one compute host.

- CPU slots

  A CPU slot is the unit used to measure compute resources. A single CPU slot can run one service instance on a compute host, or one session manager on a management host.

## 守护进程

- vemkd

  The VEM kernel daemon that runs on the master host. It starts other daemons and responds to allocation requests.

- egosc

  The v service controller requests appropriate resources from the **vemkd** daemon and controls service instances.

- pem

  Process execution manager works for the **vemkd** daemon, starting, controlling, and monitoring activities, as well as collecting and sending run time resource usage.