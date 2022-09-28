# 控制作业执行

使用 LSF 命令来暂停（**bstop**），恢复（**bresume**）和杀死（**bkill**）作业。

## bstop 命令

要暂停正在运行的作业，请使用 **bstop** 命令并指定作业 ID：

```shell
% bstop 1266
Job <1266> is being stopped
```

如果作业在停止时正在运行，则 **bjobs** 命令显示作业 1266 的 USUSP 状态：

```shell
% bjobs
JOBID USER      STAT  QUEUE     FROM_HOST   EXEC_HOST   JOB_NAME    SUBMIT_TIME
1266  user1     USUSP normal    hosta       hostb       sleep 60    Jun 5 17:39:58
```

作业提交者只能暂停自己的工作。 LSF 管理员可以暂停任何作业。

## bresume 命令

要恢复暂停的作业，请使用 **bresume** 命令。

```shell
% bresume 1266
Job <1266> is being resumed
```

如果作业立即恢复，则 **bjobs** 命令显示作业 1266 的运行状态：

```shell
% bjobs
JOBID USER      STAT  QUEUE     FROM_HOST   EXEC_HOST   JOB_NAME    SUBMIT_TIME
1266  user1     RUN   normal    hosta       hostb       sleep 60    Jun 5 17:39:58
```

作业提交者只能恢复自己的工作。 LSF 管理员可以恢复任何作业。.

## bkill 命令

要取消作业，请使用 **bkill** 命令，该命令会向指定的作业发送信号。 例如，如果作业所有者或 LSF 管理员运行以下命令，作业 1266 将被杀死：

```shell
% bkill 1266
Job <1266> is being terminated
```