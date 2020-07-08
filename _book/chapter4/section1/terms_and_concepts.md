# 术语与概念

Before you use LSF for the first time, you should read the *LSF Foundations Guide* for a basic understanding of workload management and job submission, and the *Administrator Foundations Guide* for an overview of cluster management and operations.



## Job states

IBM Spectrum LSF jobs have several states.

- PEND

  Waiting in a queue for scheduling and dispatch.

- RUN

  Dispatched to a host and running.

- DONE

  Finished normally with zero exit value.

- EXIT

  Finished with nonzero exit value.

- PSUSP

  Suspended while the job is pending.

- USUSP

  Suspended by user.

- SSUSP

  Suspended by the LSF system.

- POST_DONE

  Post-processing completed without errors.

- POST_ERR

  Post-processing completed with errors.

- UNKWN

  The **mbatchd** daemon lost contact with the **sbatchd** daemon on the host where the job runs.

- WAIT

  For jobs submitted to a chunk job queue, members of a chunk job that are waiting to run.

- ZOMBI

  A job becomes ZOMBI if the execution host is unreachable when a non-rerunnable job is killed or a rerunnable job is requeued.

## Host

An LSF host is an individual computer in the cluster.

Each host might have more than one processor. Multiprocessor hosts are used to run parallel jobs. A multiprocessor host with a single process queue is considered a single machine. A box full of processors that each have their own process queue is treated as a group of separate machines.

**Tip**

The names of your hosts should be unique. They cannot be the same as the cluster name or any queue that is defined for the cluster.

## Job

An LSF job is a unit of work that runs in the LSF system.

A job is a command that is submitted to LSF for execution, by using the bsub command. LSF schedules, controls, and tracks the job according to configured policies.

Jobs can be complex problems, simulation scenarios, extensive calculations, anything that needs compute power.

### Job files

When a job is submitted to a queue, LSF holds it in a job file until conditions are right for it run. Then, the job file is used to run the job.

On UNIX, the job file is a Bourne shell script that is run at execution time.

On Windows, the job file is a batch file that is processed at execution time.

## Interactive batch job

An interactive batch job is a batch job that allows you to interact with the application and still take advantage of LSFscheduling policies and fault tolerance.

All input and output are through the terminal that you used to type the job submission command.

When you submit an interactive job, a message is displayed while the job is awaiting scheduling. A new job cannot be submitted until the interactive job is completed or terminated.

## Interactive task

An interactive task is a command that is not submitted to a batch queue and scheduled by LSF, but is dispatched immediately.

LSF locates the resources that are needed by the task and chooses the best host among the candidate hosts that has the required resources and is lightly loaded. Each command can be a single process, or it can be a group of cooperating processes.

Tasks are run without using the batch processing features of LSF but still with the advantage of resource requirements and selection of the best host to run the task based on load.

## Local task

A local task is an application or command that does not make sense to run remotely.

For example, the **ls** command on UNIX.

## Remote task

A remote task is an application or command that that can be run on another machine in the cluster.

## Host types and host models

Hosts in LSF are characterized by host type and host model.

The following example is a host with type X86_64, with host models Opteron240, Opteron840, Intel_EM64T, and so on.

![img](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_admin/hosttypes11.jpg)

### Host type

An LSF host type is the combination of operating system and host CPU architecture.

All computers that run the same operating system on the same computer architecture are of the same type. These hosts are binary-compatible with each other.

Each host type usually requires a different set of LSF binary files.

### Host model

An LSF host model is the host type of the computer, which determines the CPU speed scaling factor that is applied in load and placement calculations.

The CPU factor is considered when jobs are being dispatched.

## Resources

LSF resources are objects in the LSF system resources that LSF uses track job requirements and schedule jobs according to their availability on individual hosts.

### Resource usage

The LSF system uses built-in and configured resources to track resource availability and usage. Jobs are scheduled according to the resources available on individual hosts.

Jobs that are submitted through the LSF system will have the resources that they use monitored while they are running. This information is used to enforce resource limits and load thresholds as well as fairshare scheduling.

LSF collects the following kinds of information:

- Total CPU time that is consumed by all processes in the job
- Total resident memory usage in KB of all currently running processes in a job
- Total virtual memory usage in KB of all currently running processes in a job
- Currently active process group ID in a job
- Currently active processes in a job

On UNIX and Linux, job-level resource usage is collected through PIM.

### Load indices

Load indices measure the availability of dynamic, non-shared resources on hosts in the cluster. Load indices that are built into the LIM are updated at fixed time intervals.

### External load indices

Defined and configured by the LSF administrator and collected by an External Load Information Manager (ELIM) program. The ELIM also updates LIM when new values are received.

### Static resources

Built-in resources that represent host information that does not change over time, such as the maximum RAM available to user processes or the number of processors in a machine. Most static resources are determined by the LIM at start-up time.

Static resources can be used to select appropriate hosts for particular jobs that are based on binary architecture, relative CPU speed, and system configuration.

### Load thresholds

Two types of load thresholds can be configured by your LSF administrator to schedule jobs in queues. Each load threshold specifies a load index value:

- The loadSched load threshold determines the load condition for dispatching pending jobs. If a host’s load is beyond any defined loadSched, a job cannot be started on the host. This threshold is also used as the condition for resuming suspended jobs.
- The loadStop load threshold determines when running jobs can be suspended.

To schedule a job on a host, the load levels on that host must satisfy both the thresholds that are configured for that host and the thresholds for the queue from which the job is being dispatched.

The value of a load index might either increase or decrease with load, depending on the meaning of the specific load index. Therefore, when you compare the host load conditions with the threshold values, you need to use either greater than (>) or less than (<), depending on the load index.

### Runtime resource usage limits

Limit the use of resources while a job is running. Jobs that consume more than the specified amount of a resource are signaled.

### Hard and soft limits

Resource limits that are specified at the queue level are hard limits while limits that are specified with job submission are soft limits. See the setrlimit man page for information about hard and soft limits.

### Resource allocation limits

Restrict the amount of a resource that must be available during job scheduling for different classes of jobs to start, and which resource consumers the limits apply to. If all of the resource is consumed, no more jobs can be started until some of the resource is released.

### Resource requirements (bsub -R)

The **bsub -R** option specifies resources requirements for the job. Resource requirements restrict which hosts the job can run on. Hosts that match the resource requirements are the candidate hosts. When LSF schedules a job, it collects the load index values of all the candidate hosts and compares them to the scheduling conditions. Jobs are only dispatched to a host if all load values are within the scheduling thresholds.