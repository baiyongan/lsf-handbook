# 查看未完成的作业的摘要信息

## Procedure

Run **bjobs -sum** to view summary information on the status of LSF jobs.

When no other options are specified, **bjobs -sum** displays the count of unfinished tasks for jobs in the following states: running (RUN), system suspended (SSUSP), user suspended (USUSP), pending (PEND), forwarded to remote clusters and pending (FWD_PEND), and UNKNOWN.

Use **bjobs -sum** with other options (such as -m, -P, -q, and -u) to filter the results. For example, bjobs -sum -u user1 displays task counts just for user user1.