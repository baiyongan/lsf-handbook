# 节点选择

Each time LSF attempts to dispatch a job, it checks to see which hosts are eligible to run the job.

A number of conditions determine whether a host is eligible:

- Host dispatch windows
- Resource requirements of the job
- Resource requirements of the queue
- Host list of the queue
- Host load levels
- Job slot limits of the host
- User quota and user limits

A host is only eligible to run a job if all the conditions are met. If a job is queued and an eligible host for that job is available, the job is placed on that host. If more than one host is eligible, the job is started on the best host based on both the job and the queue resource requirements.

## Host load levels

A host is available if the values of the load indexes (such as r1m, pg, mem) of the host are within the configured scheduling thresholds. You can configure two kinds of scheduling thresholds: host and queue. If any load index on the host exceeds the corresponding host threshold or queue threshold, the host is not eligible to run any job.

## Eligible hosts

When LSF tries to place a job, it obtains current load information for all hosts.

The load levels on each host are compared to the scheduling thresholds configured for that host in the Host section of lsb.hosts, and the per-queue scheduling thresholds configured in lsb.queues.

If any load index exceeds either its per-queue or its per-host scheduling threshold, no new job is started on that host.