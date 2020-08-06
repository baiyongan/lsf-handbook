# 关于错误日志

错误日志维护有关 License Scheduler 操作的重要信息。

##### 提示

日志文件会随着时间增长。 偶尔清除或备份这些文件（手动或使用自动脚本）。

每次记录消息时都会重新打开日志文件，因此，如果重命名或删除守护程序日志文件，则守护程序会自动创建一个新的日志文件。

日志文件的位置通过 lsf.conf 中的参数 **LSF_LOGDIR** 指定。

LSF License Scheduler 系统守护程序的错误日志文件名是：

- bld.log.host_name
- blcollect.log.host_name

## 关于 blcollect 日志消息

**blcollect** 记录的消息包括以下信息：

- Time: 消息记录时间。
- **blcollect** 名称: 服务域名，即许可证服务器主机名，由 blcollect 根据 lsf.licensescheduler 中的定义进行访问。
- 功能收集的状态报告：**blcollect** 信息是否成功收集。
- 详细信息：**blcollect** 收集的令牌数量，令牌名称，许可证令牌的许可证服务器名称。



- ##### 管理日志文件

- ##### 临时更改日志级别