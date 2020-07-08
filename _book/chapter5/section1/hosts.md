# 节点

A host is an individual computer in the cluster.

Each host may have more than one processor. Multiprocessor hosts are used to run parallel jobs. A multiprocessor host with a single process queue is considered a single machine, while a box full of processors that each have their own process queue is treated as a group of separate machines.

## Commands

- **lsload** — View load on hosts

- **lshosts** — View configuration information about hosts in the cluster including number of CPUS, model, type, and whether the host is a client or server

- **bhosts** — View batch server hosts in the cluster

  **Tip**The names of your hosts should be unique. They should not be the same as the cluster name or any queue defined for the cluster.