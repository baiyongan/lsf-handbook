# Control job execution

Use LSF commands to suspend (**bstop**), resume (**bresume**), and kill (**bkill**) jobs.

## bstop command

To suspend a running job, use the **bstop** command and specify the job ID:

```
% bstop 1266
Job <1266> is being stopped
```

If the job was running when it was stopped, the **bjobs** command shows USUSP status for job 1266:

```
% bjobs
JOBID USER      STAT  QUEUE     FROM_HOST   EXEC_HOST   JOB_NAME    SUBMIT_TIME
1266  user1     USUSP normal    hosta       hostb       sleep 60    Jun 5 17:39:58
```

Job owners can suspend only their own jobs. LSF administrators can suspend any job.

## bresume command

To resume a suspended job, use the **bresume** command.

```
% bresume 1266
Job <1266> is being resumed
```

If the job resumes immediately, the **bjobs** command shows RUN status for job 1266:

```
% bjobs
JOBID USER      STAT  QUEUE     FROM_HOST   EXEC_HOST   JOB_NAME    SUBMIT_TIME
1266  user1     RUN   normal    hosta       hostb       sleep 60    Jun 5 17:39:58
```

Job owners can resume only their own jobs. LSF administrators can resume any job.

## bkill command

To kill a job, use the **bkill** command, which sends a signal to the specified jobs. For example, if the job owner or the LSF administrator runs the following command, job 1266 is killed:

```
% bkill 1266
Job <1266> is being terminated
```