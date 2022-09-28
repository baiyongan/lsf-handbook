# 检查 blstat 是否支持 lmstat

有些问题是由于 LSF License Scheduler 收集器不支持许可证管理器所致。

## 步骤

1. 创建shell脚本以输出（例如，echo）目标 **lmstat** 输出。
2. 将 lsf.licensescheduler 中的 **LMSTAT_PATH** 指向 shell 脚本。
3. 如果未设置 **LIC_COLLECTOR**，请重新启动 **bld** 以重新启动 **blcollect**。 如果设置了 **LIC_COLLECTOR **，请杀死 **blcollect**，然后手动重启 **blcollect**。
4. 观察 **blcollect** 日志以查看是否存在任何错误，以确定 **blcollect** 是否能够正确解析 **lmstat** 输出。