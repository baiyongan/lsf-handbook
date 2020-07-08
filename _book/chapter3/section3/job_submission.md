# 作业提交

Submit jobs on the command line with the **bsub** command. You can specify many options with the **bsub** command to modify the default behavior. Jobs must be submitted to a queue.

You can also use the IBM Platform Application Center to submit jobs.

**Parent topic:**

[Inside workload management](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_foundations/chap_lsf_inside_workload_management.html?view=kc)

## Queues

Queues represent a set of pending jobs, lined up in a defined order and waiting for their opportunity to use resources. Queues implement different job scheduling and control policies.

Queues have the following attributes:

- Priority
- Name
- Queue limits (restrictions on hosts, number of jobs, users, groups, or processors)
- Standard UNIX and Linux limits (memory, swap, process, CPU)
- Scheduling policies
- Administrators
- Run conditions
- Load-sharing threshold conditions
- UNIX **nice** value (sets the UNIX and Linux scheduler priority)

### Queue priority

Defines the order in which queues are searched to determine which job will be processed. Queues are assigned a priority by the LSF administrator, where a higher number has a higher priority. Queues are serviced by LSF in order of priority from the highest to the lowest. If multiple queues have the same priority, LSF schedules all the jobs from these queues in first-come, first-served order.

## Automatic queue selection

When you submit a job, LSF considers the requirements of the job and automatically chooses a suitable queue from a list of candidate default queues.

LSF selects a suitable queue according to the following constraints:

- User access restriction

  Queues that do not allow this user to submit jobs are not considered.

- Host restriction

  If the job explicitly specifies a list of hosts on which the job can be run, then the selected queue must be configured to send jobs to hosts in the list.

- Queue status

  Closed queues are not considered.

- Exclusive execution restriction

  If the job requires exclusive execution, then queues that are not configured to accept exclusive jobs are not considered.

- Job’s requested resources

  Resources that the job requests must be within the resource allocation limits of the selected queue.

If multiple queues satisfy the above requirements, then the first queue that is listed in the candidate queues that satisfies the requirements is selected.