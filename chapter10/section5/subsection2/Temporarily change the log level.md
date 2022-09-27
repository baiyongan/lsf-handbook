# 临时更改日志级别

## 开始之前

您必须从运行守护程序的主机提交命令（仅适用于 **bld**）。

## 任务说明

您可以临时更改 **bld** 和 **blcollect** 守护程序的类或消息日志级别，而无需更改 lsf.licensescheduler。

所设置的消息日志级别自设置之时起一直有效，直到您将其关闭或守护程序停止运行为止（以较早者为准）。 如果重新启动该守护程序，则其消息日志级别将重置为 **LS_LOG_MASK** 的值，并且日志文件存储在 **LSF_LOGDIR ** 指定的目录中。

## 步骤

1. 设置 **bld** 的日志级别。

   bladmin blddebug [-l debug_level] [-c class_name]

   示例:

   ```shell
   bladmin blddebug -l 1 -c "LC_TRACE LC_FLEX"
   ```

   记录在本地主机上运行的 **bld** 的消息，并将日志消息级别设置为 LOG_DEBUG1。 日志类为 LC_TRACE LC_FLEX。

2. 将日志级别设置为 **blcollect**。

   bladmin blcdebug [-l debug_level] collector_name ... | all

   示例:

   bladmin blcdebug -l 3 all

   所有收集器的日志掩码都更改为 LOG_DEBUG3。

3. 将调试设置恢复为其配置值（在 lsf.licensescheduler 中用 **LS_LOG_MASK** 设置）。

   bladmin blddebug -o

   bladmin blcdebug -o

## 示例

有关这些命令及其选项的详细说明，请参阅 IBM Spectrum LSF Command 参考.