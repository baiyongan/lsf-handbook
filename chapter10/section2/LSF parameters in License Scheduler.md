# License Scheduler中的 LSF 参数

lsf.conf 中以 LSF_LIC_SCHED 开头的参数与 LSF 和 License Scheduler 都相关：

- ##### LSF_LIC_SCHED_HOSTS

  LIM 在候选 License Scheduler 主机上启动 License Scheduler 守护程序（**bld**）。

  ##### CAUTION

  如果您的集群是通过 UNIFORM_DIRECTORY_PATH 或 UNIFORM_DIRECTORY_PATH_EGO 安装的，则不能使用 LSF_LIC_SCHED_HOSTS。 不要为新安装或升级安装设置 UNIFORM_DIRECTORY_PATH 或 UNIFORM_DIRECTORY_PATH_EGO。 它们仅用于与早期版本兼容。

- ##### LSF_LIC_SCHED_PREEMPT_REQUEUE

  重新安排许可证调度程序抢占其许可证的作业。 作业被杀死并重新排队，而不是暂停。

- ##### LSF_LIC_SCHED_PREEMPT_SLOT_RELEASE

  释放已暂停的 “License Scheduler”  作业的内存和槽位资源。 这些资源仅可用于，请求至少一个与挂起的作业相同的许可证的挂起 License Scheduler 作业。

  默认情况下释放作业槽位，但是如果启用了内存抢占（即在 lsb.params 中设置了 PREEMPTABLE_RESOURCES = mem），则也会释放内存资源。

- ##### LSF_LIC_SCHED_PREEMPT_STOP

  使用作业控件停止被抢占的作业。 设置此参数后，将发送 UNIX SIGSTOP 信号来挂起作业，而不是 UNIX SIGTSTP。

- ##### LSF_LIC_SCHED_STRICT_PROJECT_NAMEs

  提交作业后，严格检查许可计划程序项目名称。 如果命名的项目拼写错误（区分大小写），则该作业将被拒绝。

## License Scheduler 使用的 LSF 参数 

- ##### LSB_SHAREDIR

  每个集群保存作业历史和记帐日志的目录

- ##### LSF_LOG_MASK

  LSF 守护程序的错误消息的记录级别

- ##### LSF_LOGDIR

  LSF 系统日志文件目录