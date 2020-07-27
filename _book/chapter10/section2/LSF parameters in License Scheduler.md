# LSF parameters in License Scheduler

Parameters in lsf.conf that start with LSF_LIC_SCHED are relevant to both LSF and License Scheduler:

- **LSF_LIC_SCHED_HOSTS**: LIM starts the License Scheduler daemon (**bld**) on candidate License Scheduler hosts.

  CAUTION

  You cannot use LSF_LIC_SCHED_HOSTS if your cluster was installed with UNIFORM_DIRECTORY_PATH or UNIFORM_DIRECTORY_PATH_EGO. Do not set UNIFORM_DIRECTORY_PATH or UNIFORM_DIRECTORY_PATH_EGO for new or upgrade installations. They are for compatibility with earlier versions only.

- **LSF_LIC_SCHED_PREEMPT_REQUEUE**: Requeues a job whose license is preempted by License Scheduler. The job is killed and requeued instead of suspended.

- **LSF_LIC_SCHED_PREEMPT_SLOT_RELEASE**: Releases memory and slot resources of a License Scheduler job that is suspended. These resources are only available to pending License Scheduler jobs that request at least one license that is the same as the suspended job.

  Job slots are released by default, but memory resources are also released if memory preemption is enabled (that is, PREEMPTABLE_RESOURCES = mem is set in lsb.params).

- **LSF_LIC_SCHED_PREEMPT_STOP**: Uses job controls to stop a job that is preempted. When this parameter is set, a UNIX SIGSTOP signal is sent to suspend a job instead of a UNIX SIGTSTP.

- **LSF_LIC_SCHED_STRICT_PROJECT_NAME**: Enforces strict checking of the License Scheduler project name upon job submission. If the project named is misspelled (case sensitivity applies), the job is rejected.

## LSF parameters used by License Scheduler

- **LSB_SHAREDIR**: Directory where the job history and accounting logs are kept for each cluster
- **LSF_LOG_MASK**: Logging level of error messages for LSF daemons
- **LSF_LOGDIR**: LSF system log file directory