# 文件位置

以下文件对于故障排除很有用。

- **BLD** 日志位于标准 $LSF_LOGDIR 中。
- **BLCOLLECT** 日志位于守护程序正在运行的主机上的 /tmp 或 $LSF_LOGDIR 中。
- 来自 **BLD**，**BLCOLLECT**，**mbatchd**，**lim** 和 **mbsched** 的核心文件位于守护程序本地主机上的 /tmp 中。