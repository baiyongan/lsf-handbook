# 故障排查

## 技巧

- 运行 **blstat** 以检查当前的许可证使用信息。
- 运行 **blusers** 以检查当前作业和许可证使用情况。 此信息是许可调度程序作业和 FlexNet 信息的已设置交集。
- 运行 **blinfo** 命令以检查当前的许可计划程序配置。
- 运行 **bld -c** 以检查配置是否正确。 带有 **LOG_DEBUG** 的此操作，将详细的配置设置写入调试日志。
- 通过设置 **LSF_LOG_MASK = LOG_DEBUG** 并使用 **bladmin reconfig all** 重新配置守护程序来打开调试。
- 在 lsf.conf 中为 **mbatchd** 调试（**LSB_DEBUG_MBD** ）设置日志类：**LC_LICSCHED**。
- 在 lsf.conf 中使用 **LSB_TIME_SCH = timelevel**（类似于 **LSB_TIME_MBD**）启用日志记录计时信息。
- 运行 **bhosts -s** 以检查资源是否已正确报告给 LSF。



- ##### 文件位置
  
  以下文件对于故障排除很有用。
- ##### 检查 blstat 是否支持 lmstat
  
  有些问题是由于 LSF License Scheduler 收集器不支持许可证管理器所致。
- ##### 除非您定义了 LSF License Scheduler elim，否则不要删除 lsb.tokens
  
  lsb.tokens 文件包含有关分配给集群的功能的分配和使用情况信息。 除非您为 LSF License Scheduler 定义了**elim**，以确保即使 **mbatchd** 和 **bld** 之间的连接断开，LSF 仍可以计划 LSF License Scheduler作业，否则请勿删除或修改此文件。