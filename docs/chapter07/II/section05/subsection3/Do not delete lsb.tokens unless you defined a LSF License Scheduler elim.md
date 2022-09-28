# 除非您定义了 LSF License Scheduler elim，否则不要删除lsb.tokens

lsb.tokens 文件包含有关分配给集群的功能的分配和使用情况信息。除非您为 LSF License Scheduler 定义了 **elim** 以确保即使 **mbatchd** 和 **bld** 之间的连接断开，LSF 仍可以调度 LSF License Scheduler 作业，否则不要删除或修改此文件。

当 **mbatchd** 与 **bld** 连接以获得负载更新时，**mbatchd** 从 **bld** 获取许可证使用信息并创建 lsb.tokens 文件 (位于 LSB_SHAREDIR/cluster_name/logdir) 以保存分配给集群的所有功能的分配和使用情况。lsf.licensescheduler 中的 **MBD_REFRESH_INTERVAL** 参数控制加载更新之间的最小间隔，还指定了 lsb.tokens 文件的更新间隔。

该文件可确保即使 **mbatchd** 和 **bld** 之间的连接断开，LSF 仍可以使用 lsb.tokens 中的最后许可证使用信息，来计划新的 LSF License Scheduler 作业。 如果删除 lsb.tokens，则 LSF 无法调度 LSF License Scheduler 作业。

## 创建 LSF 许可证调度程序 elim

如果 **mbatchd** 和 **bld** 之间的连接由于网络故障或 **bld** 断开而断开，您还可以定义一个动态资源，其名称与 LSF License Scheduler 功能相同，并且 创建一个 **elim** 以获取免费许可证的数量，以确保 LSF 仍可以计划待执行的LSF License Scheduler 作业。

在这种情况下，如果 **bld** 关闭或断开连接，则即使 **bld** 关闭，LSF 许可证调度程序资源也会覆盖 LSF 动态资源，并且任何作业都无法保留该资源。

为避免此问题，请在 LSF License Scheduler 关闭或断开连接时删除 lsb.tokens 文件。