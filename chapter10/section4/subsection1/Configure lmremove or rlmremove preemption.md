# Configure lmremove or rlmremove preemption

Enable and configure **lmremove** (for FlexNet) or **rlmremove** (for Reprise License Manager) as a preemption action.

## About this task

Preemption is enabled by configuring license ownership for a project. When a project has ownership of licenses that are occupied by another project, these licenses can be preempted by the project that has ownership when it needs to use the licenses.

```
Begin Feature
NAME = lic1
FAST_DISPATCH= Y
DISTRIBUTION = serviceDomain1(projectA 1/10 projectB 1 )
End Feature
```

The default preemption action is to send a TSTP signal to the job. Some applications will respond well to this action, and will free up their licenses and suspend their processes. If your applications respond well to the TSTP signal, leave this default as the preemption action.

For applications that do not respond well to the TSTP signal, an alternative preemption action for projects in fast dispatch project mode is to suspend the job’s processes, then use **lmremove** or **rlmremove** to remove licenses from the application. **lmremove** or **rlmremove** causes the license manager daemon and vendor daemons to close the TCP connection with the application.

Once the application is resumed, it will try to reacquire the licenses. In general, **lmremove** or **rlmremove** will fail to remove licenses from an application for a period of time after the licenses are checked out. This period depends on the application itself.

When LSF License Scheduler calls **lmremove** or **rlmremove**, it may remove licenses from running jobs when the running jobs share the same user and host as a suspended job. LSF License Scheduler will continue to reserve the licenses (from the rusage) for the running job. Therefore, when the running job tries to reacquire its licenses, there will be licenses available for it.

LSF License Scheduler calls **lmremove** or **rlmremove** in the same directory as it calls the **lmstat** or **rlmstat** command (as defined in the **LMSTAT_PATH** or **RLMSTAT_PATH** parameter).

## Procedure

1. Enable `lmremove` or `rlmremove` as a preemption action by specifying the **LM_REMOVE_SUSP_JOBS** parameter in the `Parameters` or `Feature` section of lsf.licensescheduler.

   LM_REMOVE_SUSP_JOBS = seconds

   Set this parameter for a license feature in its corresponding `Feature` section as long as it is using the fast dispatch project mode. If you set this parameter in the `Parameters` section, this applies to all license features using the fast dispatch project mode. When this parameter is configured for a license feature, LSF License Scheduler will periodically use **lmremove** or **rlmremove** to try to remove the license feature from each recently-suspended job.

   For a given application, set **LM_REMOVE_SUSP_JOBS** to a value greater than the period following a license checkout that **lmremove** or **rlmremove** will fail for that application. In this way, you can be sure that when a job is suspended, its licenses will be released. The length of this period depends on the application.

   LSF License Scheduler will continue to try removing the license feature for the specified number of seconds after the job is first suspended.

   For example, if you define LM_REMOVE_SUSP_JOBS = 10, when a job is suspended due to preemption,LSF License Scheduler will continue to try removing the license feature for up to ten seconds after the job is first suspended.

2. Enable LSF License Scheduler to preempt a job immediately after a license checkout by defining LM_REMOVE_INTERVAL = 0 in the `Parameters` section of lsf.licensescheduler.

   LM_REMOVE_INTERVAL = 0

   Defining this parameter to a larger value prevents LSF License Scheduler from preempting a job for a period of time after LSF License Scheduler first detects a license checkout by the job (the default value is 180 seconds). Defining LM_REMOVE_INTERVAL = 0 ensures that LSF License Scheduler can preempt a job immediately after checkout. After the job is suspended, LSF License Scheduler calls **lmremove** or **rlmremove** to release licenses from the job.

3. To limit the amount of time between subsequent forks of child processes to run **lmremove** or **rlmremove**, define the **LM_REMOVE_SUSP_JOBS_INTERVAL** parameter in the `Parameters` or section of lsf.licensescheduler.

   LM_REMOVE_SUSP_JOBS_INTERVAL = seconds

   By default, LSF License Scheduler forks a child process to run **lmremove** or **rlmremove** every time it receives an update from a license collector daemon (**blcollect**). Defining this parameter controls the minimum amount of time between subsequent forks.