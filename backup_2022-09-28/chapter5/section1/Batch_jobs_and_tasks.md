# Batch jobs and tasks

You can either run jobs through the batch system where jobs are held in queues, or you can interactively run tasks without going through the batch system, such as tests.

**Parent topic:**

[About IBM Spectrum LSF](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_users_guide/chap_lsf_about.html?view=kc)

## Job

A unit of work that is run in the LSF system. A job is a command that is submitted to LSF for execution, using the bsub command. LSF schedules, controls, and tracks the job according to configured policies.

Jobs can be complex problems, simulation scenarios, extensive calculations, anything that needs compute power.

### Commands

- **bjobs** — View jobs in the system
- **bsub** — Submit jobs

## Interactive batch job

A batch job that allows you to interact with the application and still take advantage of LSF scheduling policies and fault tolerance. All input and output are through the terminal that you used to type the job submission command.

When you submit an interactive job, a message is displayed while the job is awaiting scheduling. A new job cannot be submitted until the interactive job is completed or terminated.

The **bsub** command stops display of output from the shell until the job completes, and no mail is sent to you by default. Use Ctrl-C at any time to terminate the job.

### Commands

- **bsub -I** — Submit an interactive job

## Interactive task

A command that is not submitted to a batch queue and scheduled by LSF, but is dispatched immediately. LSF locates the resources that are needed by the task and chooses the best host among the candidate hosts that has the required resources and is lightly loaded. Each command can be a single process, or it can be a group of cooperating processes.

Tasks are run without using the batch processing features of LSF but still with the advantage of resource requirements and selection of the best host to run the task based on load.

### Commands

- **lsrun** — Submit an interactive task
- **lsgrun** — Submit an interactive task to a group of hosts

See also LSF utilities such as **ch**, **lsacct**, **lsacctmrg**, **lslogin**, **lsplace**, **lsload**, **lsloadadj**, **lseligible**, **lsmon**, **lstcsh**.

## Local task

An application or command that does not make sense to run remotely. For example, the **ls** command on UNIX.

### Commands

- **lsltasks** — View and add tasks

### Configuration

- lsf.task— Configure system-wide resource requirements for tasks
- lsf.task.cluster — Configure cluster-wide resource requirements for tasks
- .lsftasks — Configure user-specific tasks

## Remote task

An application or command that can be run on another machine in the cluster.

### Commands

- **lsrtasks** — View and add tasks

### Configuration

- lsf.task — Configure system-wide resource requirements for tasks
- lsf.task.cluster — Configure cluster-wide resource requirements for tasks
- .lsftasks — Configure user-specific tasks