# 容错

The robust architecture of LSF is designed with fault tolerance in mind. Every component in the system has a recovery operationso that vital components are monitored by another component and can automatically recover from a failure.

LSF is designed to continue operating even if some of the hosts in the cluster are unavailable. One host in the cluster acts as the master, but if the master host becomes unavailable another master host candidate takes over. LSF is available when one master host candidate is available in the cluster.

LSF can tolerate the failure of any host or group of hosts in the cluster. When a host becomes unavailable, all jobs that are running on that host are either requeued or lost, depending on whether the job was marked as rerunnable. No other pending or running jobs are affected.

## How failover works

Fault tolerance depends on the event log file, lsb.events, which is kept on the primary file server. Every event in the system is logged in this file, including all job submissions and job and host status changes. If the master host becomes unavailable, a new master is chosen from the master candidate list, and the **sbatchd** daemon on the new master starts a new **mbatchd** daemon. The new **mbatchd** daemon reads the lsb.events file to recover the state of the system.

## Duplicate event logging

For sites not wanting to rely solely on a central file server for recovery information, LSF can be configured to maintain a duplicate event log by keeping a replica of the lsb.events file. The replica is stored on the file server, and used if the primary copy is unavailable. When duplicate event logging is enabled, the primary event log is stored locally on the first master host, and resynchronized with the replicated copy when the host recovers.

## Host failover

The LSF master host is chosen dynamically. If the current master host becomes unavailable, another host takes over automatically. The failover master host is selected from the list that is defined in the **LSF_MASTER_LIST** parameter in the lsf.conf file (specified in the install.config file at installation). The first available host in the list acts as the master.

Running jobs are managed by the **sbatchd** daemon on each server host. When the new **mbatchd** daemon starts, it polls the **sbatchd** daemon on each host and finds the status of its jobs. If the **sbatchd** daemon fails but the host is still running, jobsthat are running on the host are not lost. When the **sbatchd** daemon is restarted, it regains control of all jobs that are running on the host.

## Job failover

Jobs can be submitted as rerunnable, so that they automatically run again from the beginning or as checkpointable, so that they start again from a checkpoint on another host if they are lost because of a host failure.

If all of the hosts in a cluster go down, all running jobs are lost. When a master candidate host comes back up and takes over as master, it reads the lsb.events file to get the state of all batch jobs. Jobs that were running when the systems went down are assumed to be exited unless they were marked as rerunnable, and email is sent to the submitting user. Pending jobs remain in their queues, and are scheduled as hosts become available.

## Partitioned cluster

If the cluster is partitioned by a network failure, a master LIM takes over on each side of the partition while a master host candidate is available on each side of the partition. Interactive load-sharing remains available while each host still has access to the LSF executable files.

## Partitioned network

If the network is partitioned, only one of the partitions can access the lsb.events file, so LSF services are only available on one side of the partition. A lock file is used to make sure that only one **mbatchd** daemon runs in the cluster.

## Job exception handling

You can configure hosts and queues so that LSF detects exceptional conditions while jobs are running, and takes appropriate action automatically. You can customize what exceptions are detected and the corresponding actions. For example, you can set LSF to restart a job automatically if it exits with a specific error code.