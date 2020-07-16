# Display job status

Use the **bjobs** command to see the job ID and other information about your jobs.

The status of each LSF job is updated periodically.

```
% bjobs
JOBID USER      STAT  QUEUE     FROM_HOST   EXEC_HOST   JOB_NAME    SUBMIT_TIME
1266  user1     RUN   normal    hosta       hostb       sleep 60    Jun 5 17:39:58
```

The job that is named sleep 60 runs for 60 seconds. When the job completes, LSF sends email to report the job completion.

You can use the job ID to monitor the status of a specific job.

If all hosts are busy, the job is not started immediately and the STAT column says PEND.