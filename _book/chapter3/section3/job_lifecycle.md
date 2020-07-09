# 作业生命周期

An LSF job goes through several states, starting with job submission, through dispatch, execution, and return of job results.

![an LSF job lifecycle](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_foundations/job_cycle_new.jpg)

## 1. Submit a job

You submit a job from an LSF client or server with the **bsub** command.

If you do not specify a queue when you submit a job, the job is submitted to the default queue.

Jobs are held in a queue while they wait to be scheduled. Waiting jobs have the PEND state. The job is held in a job file in the LSF_SHAREDIR/cluster_name/logdir/info/ directory, or in one of its subdirectories if the **MAX_INFO_DIRS** parameter is defined in the configuration file lsb.params.

- Job ID

  LSF assigns each job a unique job ID when you submit the job.

- Job name

  You can also assign an arbitrary name to the job with the **-J** option of **bsub**. Unlike the job ID, the job name is not necessarily unique.

## 2. Schedule the job

1. The master batch daemon (**mbatchd**) looks at jobs in the queue and sends the jobs for scheduling to the master batch scheduler daemon (**mbschd**). Jobs are scheduled at a preset time interval (defined by the parameter **JOB_SCHEDULING_INTERVAL** in the configuration file lsb.params).

2. mbschd

    

   evaluates jobs and makes scheduling decisions based on:

   - Job priority
   - Scheduling policies
   - Available resources

3. mbschd

    

   selects the best hosts where the job can run and sends its decisions back to

    

   mbatchd

   .

   Resource information is collected at preset time intervals by the master load information manager (LIM) from LIMs on server hosts. The master LIM communicates this information to **mbatchd**, which in turn communicates it to **mbschd** to support scheduling decisions.

## 3. Dispatch the job

As soon as **mbatchd** receives scheduling decisions, it immediately dispatches the jobs to hosts.

## 4. Run the job

The slave batch daemon (**sbatchd**) has the following functions:

1. Receives the request from **mbatchd**.

2. Creates a child **sbatchd** for the job.

3. Creates the execution environment.

4. Starts the job by using a remote execution server (

   res

   ).

   LSF copies the execution environment from the submission host to the execution host:

   - Environment variables that are needed by the job

   - Working directory where the job begins running

   - Other system-dependent environment settings

     - On UNIX and Linux, resource limits and umask

     - On Windows, desktop and Windows root directory

       The job runs under the user account that submitted the job and has the status RUN.

## 5. Return output

When a job is completed, it is assigned the DONE status if the job was completed without any problems. The job is assigned the EXIT status if errors prevented the job from completing.

**sbatchd** communicates job information, such as errors and output to **mbatchd**.

## 6. Send email to client

**mbatchd** returns the job output, job error, and job information to the submission host through email. Use the **-o** and **-e** options of **bsub** to send job output and errors to a file.

A job report is sent by email to the LSF client and includes the following information:

- Job information:
  - CPU use
  - Memory use
  - Name of the account that submitted the job
- Job output
- Errors