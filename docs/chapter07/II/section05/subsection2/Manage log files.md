# 管理日志文件

## 任务说明

License Scheduler 会记录不同级别的错误消息，以便您可以选择记录所有消息，也可以仅记录被视为严重的消息。

## 步骤

1. 将 lsf.licensescheduler 中的 **LS_LOG_MASK** 设置为所需的日志记录级别。

   ##### 提示

   如果未定义 LS_LOG_MASK，则使用 lsf.conf 中的 LSF_LOG_MASK 的值。 如果未定义 LS_LOG_MASK 或 LSF_LOG_MASK，则默认值为 LOG_WARNING。

   日志级别（从最高到最低）：

   - LOG_WARNING: 默认。 仅基本错误消息。
   - LOG_DEBUG: 调试消息的数量最少，对于调试问题很有用。
   - LOG_DEBUG1: 调试消息多于 LOG_DEBUG。
   - LOG_DEBUG2: 最常用的调试级别。
   - LOG_DEBUG3: 所有调试消息。 谨慎使用。

   将记录指定级别和更高级别记录的消息，而较低级别的消息将被丢弃。

2. 定期清理或备份日志文件。