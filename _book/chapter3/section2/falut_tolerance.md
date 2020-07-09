# 容错

LSF 的强大体系结构在设计时考虑了容错能力。 系统中的每个组件都具有恢复操作，因此，重要组件可以由另一个组件监视，并可以自动从故障中恢复。

即使集群中的某些主机不可用，LSF 也可以继续运行。 集群中的一个主机充当主节点，但是如果该主节点不可用，则由另一台主机候选节点接管。当集群中有一个主节点候选时，LSF 可用。

LSF 可以容许集群中，任何主机或主机组的故障。当某主机不可用时，在该主机上运行的所有作业，将会重新排队运行或丢失，具体取决于该作业是否被标记为可重新运行。其他挂起或正在运行的作业，则不会受到影响。

## 故障转移的工作原理

容错能力取决于事件日志文件 lsb.events，该文件保存在主文件服务器上。系统中的每个事件都记录在该文件中，包括所有作业提交以及作业和主机状态更改。如果主节点不可用，则从主节点候选列表中选择一个新的主节点，新的主节点上的 **sbatchd** 守护程序，将启动一个新的 **mbatchd** 守护程序。 新的 **mbatchd** 守护程序，会读取lsb.events 文件以恢复系统状态。

## 重复事件记录

For sites not wanting to rely solely on a central file server for recovery information, LSF can be configured to maintain a duplicate event log by keeping a replica of the lsb.events file. The replica is stored on the file server, and used if the primary copy is unavailable. When duplicate event logging is enabled, the primary event log is stored locally on the first master host, and resynchronized with the replicated copy when the host recovers.

## 主机故障转移

The LSF master host is chosen dynamically. If the current master host becomes unavailable, another host takes over automatically. The failover master host is selected from the list that is defined in the **LSF_MASTER_LIST** parameter in the lsf.conf file (specified in the install.config file at installation). The first available host in the list acts as the master.

Running jobs are managed by the **sbatchd** daemon on each server host. When the new **mbatchd** daemon starts, it polls the **sbatchd** daemon on each host and finds the status of its jobs. If the **sbatchd** daemon fails but the host is still running, jobsthat are running on the host are not lost. When the **sbatchd** daemon is restarted, it regains control of all jobs that are running on the host.

## 作业故障转移

Jobs can be submitted as rerunnable, so that they automatically run again from the beginning or as checkpointable, so that they start again from a checkpoint on another host if they are lost because of a host failure.

If all of the hosts in a cluster go down, all running jobs are lost. When a master candidate host comes back up and takes over as master, it reads the lsb.events file to get the state of all batch jobs. Jobs that were running when the systems went down are assumed to be exited unless they were marked as rerunnable, and email is sent to the submitting user. Pending jobs remain in their queues, and are scheduled as hosts become available.

## 分区集群

If the cluster is partitioned by a network failure, a master LIM takes over on each side of the partition while a master host candidate is available on each side of the partition. Interactive load-sharing remains available while each host still has access to the LSF executable files.

## 分区网络

If the network is partitioned, only one of the partitions can access the lsb.events file, so LSF services are only available on one side of the partition. A lock file is used to make sure that only one **mbatchd** daemon runs in the cluster.

## 作业异常处理

You can configure hosts and queues so that LSF detects exceptional conditions while jobs are running, and takes appropriate action automatically. You can customize what exceptions are detected and the corresponding actions. For example, you can set LSF to restart a job automatically if it exits with a specific error code.