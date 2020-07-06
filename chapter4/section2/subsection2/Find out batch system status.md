# Find out batch system status

Use the **bhosts** command to see whether the LSF batch workload system is running properly. The **bqueues** command displays the status of available queues and their configuration parameters.

To use LSF batch commands, the cluster must be up and running. See [Starting your cluster](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_admin_foundations/start_cluster.html?view=kc#start_cluster964) for information about starting LSF daemons.

## bhosts command

The **bhosts** command displays the status of LSF batch server hosts in the cluster, and other details about the batch hosts:

- Maximum number of job slots that are allowed by a single user
- Total number of jobs in the system, running jobs, jobs that are suspended by users, and jobs that are suspended by the system
- Total number of reserved job slots

Normal status 

ok

 for all hosts in your cluster.

```
% bhosts
HOST_NAME          STATUS       JL/U    MAX  NJOBS    RUN  SSUSP  USUSP    RSV 
hosta              ok              -      -      0      0      0      0      0
hostb              ok              -      -      0      0      0      0      0
hostc              ok              -      -      0      0      0      0      0
hostd              ok              -      -      0      0      0      0      0
```

If you see the following message when you start or reconfigure LSF, wait a few seconds and try the **bhosts** command again to give the **mbatchd** daemon time to initialize.

```
batch system daemon not responding ... still trying
```

If the problem persists, see [Solving common LSF problems](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_admin/troubleshooting_common_problems_lsf.html?view=kc#v3534299) for help.

## bqueues command

LSF queues organize jobs with different priorities and different scheduling policies.

The **bqueues** command displays the status of available queues and their configuration parameters. For a queue to accept and dispatch jobs, the status must be Open:Active.

```
% bqueues
QUEUE_NAME      PRIO STATUS          MAX JL/U JL/P JL/H NJOBS  PEND   RUN  SUSP 
owners           43   Open:Active      -    -    -    -     0     0     0     0
priority         43   Open:Active      -    -    -    -     0     0     0     0
night            40    Open:Inact      -    -    -    -     0     0     0     0
chkpnt_rerun_qu  40   Open:Active      -    -    -    -     0     0     0     0
short            35   Open:Active      -    -    -    -     0     0     0     0
license          33   Open:Active      -    -    -    -     0     0     0     0
normal           30   Open:Active      -    -    -    -     0     0     0     0
idle             20   Open:Active      -    -    -    -     0     0     0     0
```

To see more detailed queue information, use the **bqueues -l** command:

```
% bqueues -l normal

QUEUE: normal
  -- For normal low priority jobs, running only if hosts are lightly loaded.  This is the default queue.

PARAMETERS/STATISTICS
PRIO NICE STATUS          MAX JL/U JL/P JL/H NJOBS  PEND   RUN SSUSP USUSP  RSV
 30   20  Open:Active       -    -    -    -     0     0     0     0     0    0
Interval for a host to accept two jobs is 0 seconds

SCHEDULING PARAMETERS
           r15s   r1m  r15m   ut      pg    io   ls    it    tmp    swp    mem
 loadSched   -     -     -     -       -     -    -     -     -      -      -
 loadStop    -     -     -     -       -     -    -     -     -      -      -

SCHEDULING POLICIES:  FAIRSHARE  NO_INTERACTIVE
USER_SHARES:  [default, 1]

USERS: all
HOSTS:  all
```

The bqueues -l command shows the following kinds of information about the queue:

- What kinds of jobs are meant to run on the queue
- Resource usage limits
- Hosts and users able to use the queue
- Scheduling threshold values:
  - loadSched is the threshold for LSF to stop dispatching jobs automatically
  - loadStop is the threshold for LSF to suspend a job automatically

## Other useful commands

- The **bparams** command displays information about the LSF batch system configuration parameters.
- The **bhist** command displays historical information about jobs.