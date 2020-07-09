# 作业调度

Submitted jobs wait in queues until they are scheduled and dispatched to a host for execution.

When a job is submitted to LSF, many factors control when and where the job starts to run:

- Active time window of the queue or hosts
- Resource requirements of the job
- Availability of eligible hosts
- Various job slot limits
- Job dependency conditions
- Fairshare constraints (configured user share policies)
- Load conditions



## Scheduling policies

To solve diverse problems, LSF allows multiple scheduling policies in the same cluster. LSF has several queue scheduling policies such as exclusive, preemptive, fairshare, and hierarchical fairshare.

- First-come, first-served (FCFS) scheduling: By default, jobs in a queue are dispatched in FCFS order. This means that jobs are dispatched according to their order in the queue.
- Service level agreement (SLA) scheduling: An SLA in LSF is a “just-in-time” scheduling policy that schedules the services agreed to between LSF administrators and LSF users. The SLA scheduling policy defines how many jobs should be run from each SLA to meet the configured goals.
- Fairshare scheduling: If you specify a fairshare scheduling policy for the queue or if host partitions have been configured, LSF dispatches jobs between users based on assigned user shares, resource usage, or other factors.
- Preemption: You can specify desired behavior so that when two or more jobs compete for the same resources, one job preempts the other. Preemption can apply to not only job slots, but also to advance reservation (reserving hosts for particular jobs) and licenses (using IBM Platform License Scheduler).
- Backfill: Allows small jobs to run on job slots reserved for other jobs, provided the backfilling job completes before the reservation time expires and resource usage is due.

## Scheduling and dispatch

Jobs are scheduled at regular intervals (5 seconds by default). Once jobs are scheduled, they can be immediately dispatched to hosts.

To prevent overloading any host, by default LSF waits a short time between dispatching jobs to the same host.

### Dispatch order

Jobs are not necessarily dispatched in order of submission.

Each queue has a priority number set by the LSF administrator when the queue is defined. LSF tries to start jobs from the highest priority queue first.

LSF considers jobs for dispatch in the following order:

- For each queue, from highest to lowest priority. If multiple queues have the same priority, LSF schedules all the jobs from these queues in first-come, first-served (FCFS) order.
- For each job in the queue, according to FCFS order.
- If any host is eligible to run this job, start the job on the best eligible host, and mark that host ineligible to start any other job until the period specified byt the **JOB_ACCEPT_INTERVAL** parameter has passed.