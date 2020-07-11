# Resources

## Resource usage

The LSF system uses built-in and configured resources to track resource availability and usage. Jobs are scheduled according to the resources available on individual hosts.

Jobs that are submitted through the LSF system will have the resources that they use monitored while they are running. This information is used to enforce resource limits and load thresholds as well as fairshare scheduling.

LSF collects information such as:

- Total CPU time consumed by all processes in the job

- Total resident memory usage in KB of all currently running processes in a job

- Total virtual memory usage in KB of all currently running processes in a job

- Currently active process group ID in a job

- Currently active processes in a job

  On UNIX, job-level resource usage is collected through PIM.

### Commands

- **lsinfo** — View the resources available in your cluster
- **bjobs -l** — View current resource usage of a job

### Configuration

- SBD_SLEEP_TIME in lsb.params — Configures how often resource usage information is sampled by PIM, collected by **sbatchd**, and sent to **mbatchd**

## Load indices

Load indices measure the availability of dynamic, non-shared resources on hosts in the cluster. Load indices that are built into the LIM are updated at fixed time intervals.

### Commands

- **lsload -l** — View all load indices
- **bhosts -l** — View load levels on a host

## External load indices

Defined and configured by the LSF administrator and collected by an External Load Information Manager (ELIM) program. The ELIM also updates LIM when new values are received.

### Commands

- **lsinfo** — View external load indices

## Static resources

Built-in resources that represent host information that does not change over time, such as the maximum RAM available to user processes or the number of processors in a machine. Most static resources are determined by the LIM at startup.

Static resources can be used to select appropriate hosts for particular jobs based on binary architecture, relative CPU speed, and system configuration.

## Load thresholds

Two types of load thresholds can be configured by your LSF administrator to schedule jobs in queues. Each load threshold specifies a load index value:

- loadSched determines the load condition for dispatching pending jobs. If a host’s load is beyond any defined loadSched, a job will not be started on the host. This threshold is also used as the condition for resuming suspended jobs.

- loadStop determines when running jobs should be suspended.

  To schedule a job on a host, the load levels on that host must satisfy both the thresholds that are configured for that host and the thresholds for the queue from which the job is being dispatched.

  The value of a load index may either increase or decrease with load, depending on the meaning of the specific load index. Therefore, when comparing the host load conditions with the threshold values, you need to use either greater than (>) or less than (<), depending on the load index.

### Commands

- **bhosts -l** — View suspending conditions for hosts
- **bqueues -l** — View suspending conditions for queues
- **bjobs -l** — View suspending conditions for a particular job and the scheduling thresholds that control when a job is resumed

### Configuration

- lsb.hosts — Configure thresholds for hosts
- lsb.queues — Configure thresholds for queues

## Runtime resource usage limits

Limit the use of resources while a job is running. Jobs that consume more than the specified amount of a resource are signaled or have their priority lowered.

### Configuration

- lsb.queues — Configure resource usage limits for queues

## Hard and soft limits

Resource limits that are specified at the queue level are hard limits while those specified with job submission are soft limits. See setrlimit(2) man page for concepts of hard and soft limits.

## Resource allocation limits

Restrict the amount of a given resource that must be available during job scheduling for different classes of jobs to start, and which resource consumers the limits apply to. If all of the resource has been consumed, no more jobs can be started until some of the resource is released.

### Configuration

- lsb.resources — Configure queue-level resource allocation limits for hosts, users, queues, and projects

## Resource requirements (bsub -R)

Restrict which hosts the job can run on. Hosts that match the resource requirements are the candidate hosts. When LSF schedules a job, it collects the load index values of all the candidate hosts and compares them to the scheduling conditions. Jobs are only dispatched to a host if all load values are within the scheduling thresholds.

### Commands

- **bsub -R** — Specify resource requirement string for a job

### Configuration

- lsb.queues — Configure resource requirements for queues