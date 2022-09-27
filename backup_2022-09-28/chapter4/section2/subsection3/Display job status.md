# 显示作业状态

使用 **bjobs** 命令查看作业 ID 和有关您的作业的其他信息。

每个 LSF 作业的状态都会定期更新。

```shell
% bjobs
JOBID USER      STAT  QUEUE     FROM_HOST   EXEC_HOST   JOB_NAME    SUBMIT_TIME
1266  user1     RUN   normal    hosta       hostb       sleep 60    Jun 5 17:39:58
```

名为 sleep 60 的作业将运行60秒。 作业完成时，LSF 发送电子邮件以报告作业完成情况。

您可以使用作业 ID 监视特定作业的状态。

如果所有主机都忙，则不会立即启动作业，并且 STAT 列显示 PEND。