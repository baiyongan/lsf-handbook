# 运行作业

Use the **bsub** and **lsrun** commands to run jobs through LSF. Use the **bjobs** command to see the status of your jobs. Control job execution with the **bstop**, **bresume**, and **bkill** commands.

## Run LSF jobs with bsub and lsrun

Use two basic commands to run jobs through LSF:

- **bsub** submits jobs to the LSF batch scheduler. LSF schedules and dispatches jobs to the best available host based on the scheduling policies you configure in your LSF queues.
- The **lsrun** command runs an interactive task on the best available host, based on current system load information gathered by the **lim** daemon.

For most jobs, all you need to do is add either the **lsrun** or **bsub** command in front of the job commands you normally use. You usually don't need to modify your executable applications or execution scripts.

**[Submit batch jobs with bsub](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_admin_foundations/submit_jobs.html?view=kc)**
The **bsub** command submits jobs to LSF batch scheduling queues.

**[Display job status with bjobs](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_admin_foundations/display_job_status.html?view=kc)**
Use the **bjobs** command to see the job ID and other information about your jobs.

**[Control job execution with bstop, bresume, and bkill](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_admin_foundations/control_job_exec.html?view=kc)**
Use LSF commands to suspend (**bstop**), resume (**bresume**), and kill (**bkill**) jobs.

**[Run interactive tasks with lsrun and lsgrun](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_admin_foundations/run_tasks.html?view=kc)**
The **lsrun** command runs a task on either the current local host or remotely on the best available host, provided it can find the necessary resources and the appropriate host type. The **lsgrun** command is similar to **lsrun**, but it runs a task on a group of hosts.

**[Integrate your applications with LSF](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_admin_foundations/integrate_apps.html?view=kc)**
By integrating your applications with LSF, you can make sure that your users can submit and run their jobs with correct and complete job submission options without making them learn LSF commands.