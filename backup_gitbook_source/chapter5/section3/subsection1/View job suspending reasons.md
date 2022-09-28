# 查看作业暂停原因

When you submit a job, it may be held in the queue before it starts running and it may be suspended while running.

## Procedure

1. Run the **bjobs -s** command.

   Displays information for suspended jobs (SUSP state) and their reasons. There can be more than one reason why the job is suspended.

   The pending reasons also display the number of hosts for each condition.

2. Run **bjobs -ls** to see detailed information about suspended jobs, including specific host names along with the suspend reason.

   The load threshold that caused LSF to suspend a job, together with the scheduling parameters, is displayed.

   **Note**The **STOP_COND** parameter affects the suspending reasons as displayed by the **bjobs** command. If the**STOP_COND** parameter is specified in the queue and the loadStop thresholds are not specified, the suspending reasons for each individual load index are not displayed.

3. To view the suspend reasons for all users, run **bjobs -s -u all**.