# D Run jobs

!!! abstract 
    概述
    

## About IBM Spectrum LSF
- [ ] LSF clusters, jobs, and queues
- [ ] Hosts
- [ ] LSF daemons
- [ ] Batch jobs and tasks
- [ ] Host types and host models
- [ ] Users and administrators
- [ ] Resources
- [ ] Job lifecycle


## Working with jobs
- [ ] Submitting jobs (bsub)
    - [ ] Submit a job
        - [ ] About submitting a job to a specific queue
        - [ ] View available queues
        - [ ] Submit a job to a queue
        - [ ] Submit a job associated with a project (bsub -P)
        - [ ] Submit a job associated with a user group (bsub -G)
        - [ ] Submit a job with a job name (bsub -J)
        - [ ] Submit a job to a service class (bsub -sla)
        - [ ] Submit a job under a job group (bsub -g)
        - [ ] Submit a job with a JSON file (bsub -json)
        - [ ] Submit a job with a YAML file (bsub -yaml)
        - [ ] Submit a job with a JSDL file (bsub -jsdl)
- [ ] Modify pending jobs (bmod)
- [ ] Modify running jobs
- [ ] About controlling jobs
    - [ ] Kill a job (bkill)
        - [ ] Forcing removal of a job from LSF
    - [ ] About suspending and resuming jobs (bstop and bresume)
    - [ ] Move a job to the bottom of a queue (bbot)
    - [ ] Move a job to the top of a queue (btop)
    - [ ] Control jobs in job groups
    - [ ] Submit a job to specific hosts
    - [ ] Submit a job with specific resources
    - [ ] Queues and host preference
    - [ ] Specify different levels of host preference
    - [ ] Submit a job with resource requirements
    - [ ] Submit a job with SSH X11 forwarding
- [ ] Using LSF with non-shared file space
    - [ ] Operator
- [ ] About resource reservation
    - [ ] View resource information
    - [ ] Submit a job with resource requirements
    - [ ] Submit a job with start or termination times
    - [ ] Submit a job with compute unit resource requirements
- [ ] Set pending time limits

## Monitoring jobs
- [ ] View information about jobs
    - [ ] View unfinished jobs
    - [ ] View summary information of unfinished jobs
    - [ ] View all jobs
    - [ ] View running jobs
    - [ ] View pending reasons for jobs
    - [ ] View job suspending reasons
    - [ ] View detailed job information
    - [ ] View job group information
    - [ ] Monitor SLA progress
    - [ ] View job output
    - [ ] View chronological history of jobs
    - [ ] View history of jobs not listed in active event log
    - [ ] View job history
    - [ ] View the job submission environment
    - [ ] Update interval
    - [ ] Job-level information
- [ ] Display resource allocation limits
    - [ ] View information about resource allocation limits
