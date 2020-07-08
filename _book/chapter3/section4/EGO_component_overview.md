# EGO 组件概览

EGO can be enabled with LSF to provide a system infrastructure to control and manage cluster resources.

Just as an operating system running on a single machine aggregates and virtualizes physical resources and allocates them to applications, EGO performs similar functions, but across a distributed environment.

EGO manages both logical and physical resources and supports all forms of applications. EGO manages the supply of resources, making them available to applications.

Hosts can be divided into two groups: management hosts and compute hosts. Management hosts provide specialized services to the cluster, while compute hosts run user workload.

## Management hosts

Management hosts provide both cluster and workload management services within the cluster, and are not expected to run workload for users. The master host, all master candidate hosts, and session manager hosts must be management hosts. Other management hosts include the host running the data loaders and data purger for the reporting feature.

Management hosts all run on the same operating system: all Windows, all UNIX, or all Linux.

- Master host

  The master host is the first host installed in the cluster. The resource manager (**vemkd**) for the cluster resides on this host. The master host controls the rest of the hosts in the cluster and is the interface to the clients of the cluster.

- Master candidates

  There is only one master host at a time. If the master host should fail, another host automatically takes over the master host role. Hosts that can act as the master are called master candidates.

- Session manager host

  One or more management hosts run session managers. There is one session manager per available slot on a management host. There is one session manager per application.

## Compute hosts

Compute hosts are those hosts in the cluster that provide computing resources to consumers. A cluster may contain any number of compute hosts, but must have at least one compute host.

- CPU slots

  A CPU slot is the unit used to measure compute resources. A single CPU slot can run one service instance on a compute host, or one session manager on a management host.

## Daemons

- vemkd

  The VEM kernel daemon that runs on the master host. It starts other daemons and responds to allocation requests.

- egosc

  The v service controller requests appropriate resources from the **vemkd** daemon and controls service instances.

- pem

  Process execution manager works for the **vemkd** daemon, starting, controlling, and monitoring activities, as well as collecting and sending run time resource usage.