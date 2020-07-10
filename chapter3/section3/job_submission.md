# 作业提交

使用 **bsub** 命令在命令行上提交作业。 您可以使用 **bsub** 命令指定许多选项来修改默认行为。 而作业必须提交到队列中。

## 队列

队列代表一组挂起等待的作业，它们按定义的顺序排列，并等待其使用资源的机会。 队列执行不同的作业调度和控制策略。

队列有以下特征:

- 优先级
- 名称
- 队列限制 (对主机、作业数、用户、组、或者处理器的限制)
- 标准 UNIX 和 Linux 限制（内存，交换，进程，CPU）
- 调度策略
- 管理员
- 运行条件
- 负载共享阈值条件
- UNIX **nice** 值 (设置 UNIX 和 Linux 调度程序优先级)

### 队列优先级

Defines the order in which queues are searched to determine which job will be processed. Queues are assigned a priority by the LSF administrator, where a higher number has a higher priority. Queues are serviced by LSF in order of priority from the highest to the lowest. If multiple queues have the same priority, LSF schedules all the jobs from these queues in first-come, first-served order.

## 自动队列选择

When you submit a job, LSF considers the requirements of the job and automatically chooses a suitable queue from a list of candidate default queues.

LSF selects a suitable queue according to the following constraints:

- User access restriction

  Queues that do not allow this user to submit jobs are not considered.

- Host restriction

  If the job explicitly specifies a list of hosts on which the job can be run, then the selected queue must be configured to send jobs to hosts in the list.

- Queue status

  Closed queues are not considered.

- Exclusive execution restriction

  If the job requires exclusive execution, then queues that are not configured to accept exclusive jobs are not considered.

- Job’s requested resources

  Resources that the job requests must be within the resource allocation limits of the selected queue.

If multiple queues satisfy the above requirements, then the first queue that is listed in the candidate queues that satisfies the requirements is selected.