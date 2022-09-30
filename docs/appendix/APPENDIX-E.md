# 附录 E Administer LSF

!!! abstract 
    概述
    

## Cluster management essentials
- [ ] Work with your cluster
- [ ] Viewing cluster information
- [ ] Control daemons
- [ ] Controlling mbatchd
- [ ] LSF daemon startup control
- [ ] Overview
- [ ] Configuration to enable
- [ ] LSF daemon startup control behavior
- [ ] Configuration to modify
- [ ] Commands
- [ ] Commands to reconfigure your cluster
- [ ] Reconfiguring with the lsadmin and badmin commands
- [ ] Reconfiguring by restarting the mbatchd daemon
- [ ] Viewing configuration errors
- [ ] Live reconfiguration
- [ ] bconf command authentication
- [ ] Enabling live reconfiguration
- [ ] Adding a user share to a fairshare queue
- [ ] View bconf records
- [ ] Merge configuration files
- [ ] Adding cluster adminstrators
- [ ] Working with hosts
- [ ] Host status
- [ ] View host information
- [ ] Customize host information output
- [ ] Customize host load information output
- [ ] Control hosts
- [ ] Connect to an execution host or container
- [ ] Host names
- [ ] Hosts with multiple addresses
- [ ] Use IPv6 addresses
- [ ] Specify host names with condensed notation
- [ ] Job directories and data
- [ ] Directory for job output
- [ ] Specify a directory for job output
- [ ] Temporary job directories
- [ ] About flexible job CWD
- [ ] About flexible job output directory
- [ ] Job notification
- [ ] Disable job email
- [ ] Size of job email

## Monitoring cluster operations and health
- [ ] Monitor cluster performance
- [ ] Monitor performance metrics in real time
- [ ] Diagnose query requests
- [ ] Diagnose scheduler buckets
- [ ] Monitor scheduler efficiency and overhead
- [ ] Monitor job information
- [ ] View host-level and queue-level suspending conditions
- [ ] View job-level suspending conditions
- [ ] View resume thresholds
- [ ] View job priority information
- [ ] View job dependencies
- [ ] View information about backfill jobs
- [ ] View information about job start time
- [ ] View the run limits for interruptible backfill jobs (bjobs and bhist)
- [ ] Display available slots for backfill jobs
- [ ] Viewing job array information
- [ ] View information about reserved job slots
- [ ] View configured job slot share
- [ ] View slot allocation of running jobs
- [ ] Monitor applications by using external scripts
- [ ] Create external scripts
- [ ] Configure the application profiles
- [ ] Use the application profiles
- [ ] View resource information
- [ ] View job-level resource requirements
- [ ] View queue-level resource requirements
- [ ] View shared resources for hosts
- [ ] View load on a host
- [ ] View job resource usage
- [ ] View cluster resources (lsinfo)
- [ ] View host resources (lshosts)
- [ ] Viewing host load by resource (lshosts -s)
- [ ] Customize host resource information output
- [ ] View resource reservation information
- [ ] View host-level resource information (bhosts)
- [ ] View queue-level resource information (bqueues)
- [ ] View reserved memory for pending jobs (bjobs)
- [ ] View per-resource reservation (bresources)
- [ ] View information about resource allocation limits
- [ ] View application profile information
- [ ] View available application profiles
- [ ] View fairshare information
- [ ] View queue-level fairshare information
- [ ] View cross-queue fairshare information
- [ ] View hierarchical share information for a group
- [ ] View hierarchical share information for a host partition
- [ ] View host partition information
- [ ] Viewing information about SLAs and service classes
- [ ] Monitoring an SLA
- [ ] Viewing configured guaranteed resource pools
- [ ] Viewing guarantee policy information
- [ ] View user and user group information
- [ ] View user information
- [ ] View user pending job threshold information
- [ ] Customize user information output
- [ ] View user group information
- [ ] View user share information
- [ ] View user group admin information
- [ ] View queue information
- [ ] Queue states
- [ ] View available queues and queue status
- [ ] View detailed queue information
- [ ] Customize queue information output
- [ ] View the state change history of a queue
- [ ] View queue administrators
- [ ] View exception status for queues (bqueues)

## Managing job execution
- [ ] Managing job execution
- [ ] About job states
- [ ] View job information
- [ ] View all jobs for all users
- [ ] View job IDs
- [ ] View jobs for specific users
- [ ] View running jobs
- [ ] View done jobs
- [ ] View pending job information
- [ ] View job suspend reasons
- [ ] View post-execution states
- [ ] View exception status for jobs (bjobs)
- [ ] View unfinished job summary information
- [ ] View the job submission environment
- [ ] Customize job information output
- [ ] Force job execution
- [ ] Force a pending job to run
- [ ] Suspend and resume jobs
- [ ] Suspend a job
- [ ] Resume a job
- [ ] Kill jobs
- [ ] Kill a job
- [ ] Kill multiple jobs
- [ ] Kill jobs by status
- [ ] Kill and record jobs as DONE
- [ ] Force removal of a job from LSF
- [ ] Remove hung jobs from LSF
- [ ] Orphan job termination
- [ ] Send a signal to a job
- [ ] Signals on different platforms
- [ ] Send a signal to a job
- [ ] Data provenance
- [ ] Prerequisites
- [ ] Using data provenance tools
- [ ] Job file spooling
- [ ] File spooling for job input, output, and command files
- [ ] Specify job input file
- [ ] Change job input file
- [ ] Job spooling directory (JOB_SPOOL_DIR)
- [ ] Specify a job command file (bsub -Zs)
- [ ] Remote file access with non-shared file space
- [ ] Copy files from the submission host to execution host
- [ ] Specify input file
- [ ] Copy output files back to the submission host
- [ ] Job submission option files
- [ ] Specify a JSON file
- [ ] Specify a YAML file
- [ ] Specify a JSDL file
- [ ] Job data management
- [ ] Copy a file to a remote host (bsub -f)
- [ ] Use LSF Data Manager for data staging
- [ ] Use direct data staging (bsub -stage)
- [ ] Configuring direct data staging
- [ ] Submitting and running direct data staging jobs
- [ ] Job scheduling and dispatch
- [ ] Use exclusive scheduling
- [ ] Configure an exclusive queue
- [ ] Configure a host to run one job at a time
- [ ] Submit an exclusive job
- [ ] Configure a compute unit exclusive queue
- [ ] Submit a compute unit exclusive job
- [ ] Job dependency and job priority
- [ ] Job dependency scheduling
- [ ] Job dependency terminology
- [ ] Dependency conditions
- [ ] Job priorities
- [ ] User-assigned job priority
- [ ] Configure job priority
- [ ] Specify job priority
- [ ] Automatic job priority escalation
- [ ] Configure job priority escalation
- [ ] Absolute priority scheduling
- [ ] Enable absolute priority scheduling
- [ ] Modify the system APS value (bmod)
- [ ] Configure APS across multiple queues
- [ ] Job priority behavior
- [ ] Job requeue and job rerun
- [ ] About job requeue
- [ ] Automatic job requeue
- [ ] Configure automatic job requeue
- [ ] Job-level automatic requeue
- [ ] Configure reverse requeue
- [ ] Exclusive job requeue
- [ ] Configure exclusive job requeue
- [ ] Requeue a job
- [ ] Automatic job rerun
- [ ] Configure queue-level job rerun
- [ ] Submit a rerunnable job
- [ ] Submit a job as not rerunnable
- [ ] Disable post-execution for rerunnable jobs
- [ ] Job start time prediction
- [ ] Job affinity scheduling with host attributes
- [ ] Configure host attributes
- [ ] Manage host attributes
- [ ] Submit jobs with attribute affinity
- [ ] Control job execution
- [ ] Pre-execution and post-execution processing
- [ ] About pre- and post-execution processing
- [ ] Configuration to enable pre- and post-execution processing
- [ ] Pre- and post-execution processing behavior
- [ ] Check job history for a pre-execution script failure
- [ ] Configuration to modify pre- and post-execution processing
- [ ] Set host exclusion based on job-based pre-execution scripts
- [ ] Pre- and post-execution processing commands
- [ ] Job starters
- [ ] About job starters
- [ ] Command-level job starters
- [ ] Queue-level job starters
- [ ] Configure a queue-level job starter
- [ ] JOB_STARTER parameter (lsb.queues)
- [ ] Control the execution environment with job starters
- [ ] Job control actions
- [ ] Submit jobs as other users
- [ ] External job submission and execution controls
- [ ] Job submission and execution controls
- [ ] Configuration to enable job submission and execution controls
- [ ] Job submission and execution controls behavior
- [ ] Configuration to modify job submission and execution controls
- [ ] Job submission and execution controls commands
- [ ] Command arguments for job submission and execution controls
- [ ] Interactive jobs and remote tasks
- [ ] Interactive jobs with bsub
- [ ] About interactive jobs
- [ ] Submit interactive jobs
- [ ] Submit an interactive job
- [ ] Submit an interactive job by using a pseudo-terminal
- [ ] Submit an interactive job and redirect streams to files
- [ ] Submit an interactive job, redirect streams to files, and display streams
- [ ] Performance tuning for interactive batch jobs
- [ ] Interactive batch job messaging
- [ ] Configure interactive batch job messaging
- [ ] Example messages
- [ ] Run X applications with bsub
- [ ] Configure SSH X11 forwarding for jobs
- [ ] Write job scripts
- [ ] Register utmp file entries for interactive batch jobs
- [ ] Interactive and remote tasks
- [ ] Run remote tasks
- [ ] Run a task on the best available host
- [ ] Run a task on a host with specific resources
- [ ] Resource usage
- [ ] Run a task on a specific host
- [ ] Run a task by using a pseudo-terminal
- [ ] Run the same task on many hosts in sequence
- [ ] Run parallel tasks
- [ ] Run tasks on hosts specified by a file
- [ ] Interactive tasks
- [ ] Redirect streams to files
- [ ] Load sharing interactive sessions
- [ ] Log on to the least loaded host
- [ ] Log on to a host with specific resources
- [ ] Configuring and sharing job resources
- [ ] About LSF resources
- [ ] Resource categories
- [ ] How LSF uses resources
- [ ] Representing job resources in LSF
- [ ] Batch built-in resources
- [ ] Static resources
- [ ] How LIM detects cores, threads, and processors
- [ ] Define ncpus—processors, cores, or threads
- [ ] Define computation of ncpus on dynamic hosts
- [ ] Define computation of ncpus on static hosts
- [ ] Load indices
- [ ] About configured resources
- [ ] Add new resources to your cluster
- [ ] Configure the lsf.shared resource section
- [ ] Configure lsf.cluster.cluster_name Host section
- [ ] Configure lsf.cluster.cluster_name ResourceMap section
- [ ] Reserve a static shared resource
- [ ] External load indices
- [ ] About external load indices
- [ ] Configuration to enable external load indices
- [ ] Define a dynamic external resource
- [ ] Map an external resource
- [ ] Create an elim executable file
- [ ] Overriding built-in load indices
- [ ] Setting up an ELIM to support JSDL
- [ ] Example of an elim executable file
- [ ] External load indices behavior
- [ ] Configuration to modify external load indices
- [ ] External load indices commands
- [ ] External static load indices
- [ ] Configuration to enable external static load indices
- [ ] Create eslim executable files
- [ ] Example of an eslim executable file
- [ ] Modify a built-in load index
- [ ] Configure host resources
- [ ] Adding a host to your cluster
- [ ] Add hosts dynamically
- [ ] Configuring and running batch jobs on dynamic hosts
- [ ] Change a dynamic host to a static host
- [ ] Add a dynamic host in a shared file system environment
- [ ] Add a dynamic host in a non-shared file system environment
- [ ] Add a host to the cluster using bconf
- [ ] Removing a host from your cluster
- [ ] Remove a host from management candidate list
- [ ] Remove dynamic hosts
- [ ] Share resources in queues
- [ ] Controlling queues
- [ ] Closing a queue
- [ ] Opening a queue
- [ ] Deactivating a queue
- [ ] Activating a queue
- [ ] Logging a comment on a queue control command
- [ ] Configuring dispatch windows
- [ ] Configuring run windows
- [ ] Adding a queue
- [ ] Removing a queue
- [ ] Restricting which hosts can use queues
- [ ] Restricting job size requested by parallel jobs in a queue
- [ ] Adding queue administrators
- [ ] Change job order within queues
- [ ] Switch jobs from one queue to another
- [ ] Switch a single job to a different queue
- [ ] Switch all jobs to a different queue
- [ ] Use external job switch controls
- [ ] Configuration to enable job switch controls
- [ ] Configuration to modify job switch controls
- [ ] Command arguments for job switch controls
- [ ] Application profiles
- [ ] Manage application profiles
- [ ] Add an application profile
- [ ] Submit jobs to application profiles
- [ ] How application profiles interact with queue and job parameters
- [ ] Application profile settings that override queue settings
- [ ] Application profile limits and queue limits
- [ ] Define application-specific environment variables
- [ ] Task limits
- [ ] Absolute run limits
- [ ] Pre-execution
- [ ] Post-execution
- [ ] Rerunnable jobs
- [ ] Resource requirements
- [ ] Estimated job run time and runtime limits
- [ ] Plan-based scheduling and reservations
- [ ] Enabling plan-based scheduling
- [ ] Plan-based allocations
- [ ] Plan-based scheduling run time
- [ ] Plan-based scheduling limits and prioritization
- [ ] Configuring extendable run limits
- [ ] Reserving resources for an allocation plan
- [ ] Canceling planned allocations
- [ ] Delaying planning for jobs
- [ ] Limiting the number of planned jobs
- [ ] Adjusting the plan window
