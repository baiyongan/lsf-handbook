# 术语与概念

首次使用 LSF 之前，应先阅读 *LSF Foundations Guide*，以基本了解作业负载管理和作业提交，以及 *Administrator Foundations Guide*，以概述集群管理和操作。



## 作业状态

IBM Spectrum LSF 作业有几种状态。

- ##### PEND

  在队列中等待调度和分配。

- ##### RUN

  分派给主机并运行。

- ##### DONE

  正常完成，退出状态码为 0。

- ##### EXIT

  以非 0 退出值结束。

- ##### PSUSP

  作业等待时挂起。

- ##### USUSP

  被用户暂停。

- ##### SSUSP

  被 LSF 系统暂停。

- ##### POST_DONE

  后处理完成，没有错误。

- ##### POST_ERR

  后处理完成，但有错误。

- ##### UNKWN

  **mbatchd** 守护程序，与作业运行所在主机上的 sbatchd 守护程序失去联系。

- ##### WAIT

  对于提交到块作业队列的作业，是等待运行的块作业成员。

- ##### ZOMBI

  如果杀死不可重新运行的作业，或将可重新运行的作业重新排队时，如果执行主机不可访问，则该作业将变为ZOMBI。



## 主机节点

An LSF host is an individual computer in the cluster.

Each host might have more than one processor. Multiprocessor hosts are used to run parallel jobs. A multiprocessor host with a single process queue is considered a single machine. A box full of processors that each have their own process queue is treated as a group of separate machines.

**Tip**

The names of your hosts should be unique. They cannot be the same as the cluster name or any queue that is defined for the cluster.



## 作业

An LSF job is a unit of work that runs in the LSF system.

A job is a command that is submitted to LSF for execution, by using the bsub command. LSF schedules, controls, and tracks the job according to configured policies.

Jobs can be complex problems, simulation scenarios, extensive calculations, anything that needs compute power.

### 作业文件

When a job is submitted to a queue, LSF holds it in a job file until conditions are right for it run. Then, the job file is used to run the job.

On UNIX, the job file is a Bourne shell script that is run at execution time.

On Windows, the job file is a batch file that is processed at execution time.

## 交互式批处理作业

An interactive batch job is a batch job that allows you to interact with the application and still take advantage of LSFscheduling policies and fault tolerance.

All input and output are through the terminal that you used to type the job submission command.

When you submit an interactive job, a message is displayed while the job is awaiting scheduling. A new job cannot be submitted until the interactive job is completed or terminated.

## 交互式任务

An interactive task is a command that is not submitted to a batch queue and scheduled by LSF, but is dispatched immediately.

LSF locates the resources that are needed by the task and chooses the best host among the candidate hosts that has the required resources and is lightly loaded. Each command can be a single process, or it can be a group of cooperating processes.

Tasks are run without using the batch processing features of LSF but still with the advantage of resource requirements and selection of the best host to run the task based on load.

## 本地任务

A local task is an application or command that does not make sense to run remotely.

For example, the **ls** command on UNIX.

## 远程任务

A remote task is an application or command that that can be run on another machine in the cluster.

## 主机类型与主机型号

Hosts in LSF are characterized by host type and host model.

The following example is a host with type X86_64, with host models Opteron240, Opteron840, Intel_EM64T, and so on.

![img](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_admin/hosttypes11.jpg)

### 主机类型

An LSF host type is the combination of operating system and host CPU architecture.

All computers that run the same operating system on the same computer architecture are of the same type. These hosts are binary-compatible with each other.

Each host type usually requires a different set of LSF binary files.

### 主机型号

An LSF host model is the host type of the computer, which determines the CPU speed scaling factor that is applied in load and placement calculations.

The CPU factor is considered when jobs are being dispatched.

## 资源

LSF resources are objects in the LSF system resources that LSF uses track job requirements and schedule jobs according to their availability on individual hosts.

### 资源使用

The LSF system uses built-in and configured resources to track resource availability and usage. Jobs are scheduled according to the resources available on individual hosts.

Jobs that are submitted through the LSF system will have the resources that they use monitored while they are running. This information is used to enforce resource limits and load thresholds as well as fairshare scheduling.

LSF collects the following kinds of information:

- Total CPU time that is consumed by all processes in the job
- Total resident memory usage in KB of all currently running processes in a job
- Total virtual memory usage in KB of all currently running processes in a job
- Currently active process group ID in a job
- Currently active processes in a job

On UNIX and Linux, job-level resource usage is collected through PIM.

### 负载指数

Load indices measure the availability of dynamic, non-shared resources on hosts in the cluster. Load indices that are built into the LIM are updated at fixed time intervals.

### 外部负载指数

Defined and configured by the LSF administrator and collected by an External Load Information Manager (ELIM) program. The ELIM also updates LIM when new values are received.

### 静态资源

Built-in resources that represent host information that does not change over time, such as the maximum RAM available to user processes or the number of processors in a machine. Most static resources are determined by the LIM at start-up time.

Static resources can be used to select appropriate hosts for particular jobs that are based on binary architecture, relative CPU speed, and system configuration.

### 负载阈值

Two types of load thresholds can be configured by your LSF administrator to schedule jobs in queues. Each load threshold specifies a load index value:

- The loadSched load threshold determines the load condition for dispatching pending jobs. If a host’s load is beyond any defined loadSched, a job cannot be started on the host. This threshold is also used as the condition for resuming suspended jobs.
- The loadStop load threshold determines when running jobs can be suspended.

To schedule a job on a host, the load levels on that host must satisfy both the thresholds that are configured for that host and the thresholds for the queue from which the job is being dispatched.

The value of a load index might either increase or decrease with load, depending on the meaning of the specific load index. Therefore, when you compare the host load conditions with the threshold values, you need to use either greater than (>) or less than (<), depending on the load index.

### 运行时资源使用限制

Limit the use of resources while a job is running. Jobs that consume more than the specified amount of a resource are signaled.

### 硬性限制和软性限制

Resource limits that are specified at the queue level are hard limits while limits that are specified with job submission are soft limits. See the setrlimit man page for information about hard and soft limits.

### 资源分配限制

Restrict the amount of a resource that must be available during job scheduling for different classes of jobs to start, and which resource consumers the limits apply to. If all of the resource is consumed, no more jobs can be started until some of the resource is released.

### 资源需求 (bsub -R)

The **bsub -R** option specifies resources requirements for the job. Resource requirements restrict which hosts the job can run on. Hosts that match the resource requirements are the candidate hosts. When LSF schedules a job, it collects the load index values of all the candidate hosts and compares them to the scheduling conditions. Jobs are only dispatched to a host if all load values are within the scheduling thresholds.