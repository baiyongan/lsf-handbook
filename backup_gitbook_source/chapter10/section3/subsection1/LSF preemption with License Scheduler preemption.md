# LSF 抢占与 License Scheduler 抢占

对于 LSF 作业，参数 **MAX_JOB_PREEMPT** 设置可以抢占作业的最大次数。 可以在 lsb.params，lsb.queues 或 lsb.applications 中定义 **MAX_JOB_PREEMPT**，其中应用程序设置覆盖队列设置，队列设置覆盖集群范围的 lsb.params 定义。

即使在 LSF 中没有可用的槽位，属于在 License Scheduler 中拥有所有权的许可证项目的作业，也可以触发抢占。 与 lsf.conf 中的 LSF_LIC_SCHED_PREEMPT_SLOT_RELEASE=Y 一起配置，许可证作业抢占与基于 LSF 槽位的抢占一起使用。 在 lsb.params 中一起配置 PREEMPTABLE_RESOURCES=mem，在 lsf.conf 中一起配置 LSF_LIC_SCHED_PREEMPT_SLOT_RELEASE=Y，许可证作业抢占与 LSF 内存资源抢占一起工作。

## 示例

项目 proj1 拥有3个许可 AppX。

在 lsf.conf 中配置了 **MXJ = 5**, 以及 **LSF_LIC_SCHED_PREEMPT_SLOT_RELEASE=Y**。

提交了五个作业，并在 proj2 中使用 AppX 启动了这些作业。 然后，将两个作业提交给 proj1，并等待 AppX 许可证令牌。 尽管槽位已满，但请求将发送到 License Scheduler，后者会识别所有权并抢占 proj2 中的两个作业。 作业被挂起，它们的许可证和槽位都被释放，并且 proj1 中的两个作业可以运行。

## LSF JOB_CONTROLS 配置

如果 LSF 管理员在 lsb.queues 中定义 JOB_CONTROLS，以使作业控制（例如信号 SIGTSTP ）在许可调度程序抢占发生时生效，则还必须在 lsf.conf 中定义 **LSF_LIC_SCHED_PREEMPT_STOP = Y  **才能使许可调度程序抢占来工作 。

