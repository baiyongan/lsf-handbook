# 查看在等待作业的原因

When you submit a job, it can be held in the queue before it starts running and it might be suspended while it is running. You can find out why jobs are pending or in suspension with the **bjobs** -**p** option.

## Procedure

1. Run **bjobs -p**.

   Displays information for pending jobs (PEND state) and their reasons. There can be more than one reason why the job is pending.

   The pending reasons also display the number of hosts for each condition.

2. To get specific host names along with pending reasons, run **bjobs -lp**.

3. To view the pending reasons for all users, run **bjobs -p -u all**.

4. Run **bjobs -psum** to display the summarized number of jobs, hosts, and occurrences for each pending reason.

5. Run **busers -w all** to see the maximum pending job threshold for all users.