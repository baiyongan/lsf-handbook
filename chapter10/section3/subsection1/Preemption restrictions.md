# 抢占限制

在以下情况下，不能抢占作业：

- 抢占受参数限制，例如：**MAX_JOB_PREEMPT**，**PREEMPT_RESERVE** 或 **LM_REMOVE_INTERVAL**。
- 可抢占作业的服务器不是当前的检查服务域。
- 提交作业的时间长度已到，该时间长度已过期。

由许可证计划程序管理的使用许可证的 **LSF** 作业和 **taskman** 作业都可以被抢占。为确保优先级较低的作业不会被多次抢占，可以使用 **LS_ENABLE_MAX_PREEMPT** 启用最大抢占次数限制。

许可证调度程序 **taskman** 作业抢占限制由 lsf.licensescheduler 中的参数 **LS_MAX_TASKMAN_PREEMPT** 控制。

