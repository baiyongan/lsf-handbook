# 3.3 作业负载管理

Understand the LSF job lifecycle. Use the **bsub** to submit jobs to a queue and specify job submission options to modify the default job behavior. Submitted jobs wait in queues until they are scheduled and dispatched to a host for execution. At job dispatch, LSF checks to see which hosts are eligible to run the job.



**[Job lifecycle](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_foundations/job_life_cycle_lsf.html?view=kc)**
An LSF job goes through several states, starting with job submission, through dispatch, execution, and return of job results.



**[Job submission](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_foundations/job_submission_lsf.html?view=kc)**
Submit jobs on the command line with the **bsub** command. You can specify many options with the **bsub** command to modify the default behavior. Jobs must be submitted to a queue.



**[Job scheduling and dispatch](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_foundations/job_scheduling_dispatch_lsf.html?view=kc)**
Submitted jobs wait in queues until they are scheduled and dispatched to a host for execution.



**[Host selection](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_foundations/host_selection_lsf.html?view=kc)**
Each time LSF attempts to dispatch a job, it checks to see which hosts are eligible to run the job.



**[Job execution environment](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_foundations/job_execution_environ_lsf.html?view=kc)**
When LSF runs your jobs, it copies the environment from the submission host to the execution host.