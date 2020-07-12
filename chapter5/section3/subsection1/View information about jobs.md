# 查看有关作业的信息

## Procedure

Use the **bjobs** and **bhist** commands to view information about jobs:

- **bjobs** reports the status of jobs and the various options allow you to display specific information.

- **bhist** reports the history of one or more jobs in the system.

  You can also find jobs on specific queues or hosts, find jobs that are submitted by specific projects, and check the status of specific jobs by using their job IDs or names.



- **View unfinished jobs**
- **View summary information of unfinished jobs**
- **View all jobs**
- **View running jobs**
- **View pending reasons for jobs**
  When you submit a job, it can be held in the queue before it starts running and it might be suspended while it is running. You can find out why jobs are pending or in suspension with the **bjobs** -**p** option.
- **View job suspending reasons**
  When you submit a job, it may be held in the queue before it starts running and it may be suspended while running.
- **View detailed job information**
- **View job group information**
  You can view information about jobs in job groups or view jobs by job group.
- **Monitor SLA progress**
- **View job output**
- **View chronological history of jobs**
- **View history of jobs not listed in active event log**
- **View job history**
- **View the job submission environment**
  Use the **bjobs -env** command option to view a job's environment variables or the **bjobs -script** command option to view the job script file.
- **Update interval**
- **Job-level information**