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

定义搜索队列，以确定要处理的作业的顺序。 LSF 管理员为队列分配了优先级，其中数值越高，优先级越高。 LSF按从高到低的优先级为队列提供服务。 如果多个队列具有相同的优先级，则 LSF 按照先来先服务的顺序，调度这些队列中的所有作业。

## 自动队列选择

提交作业时，LSF 会考虑作业要求，并自动从候选默认队列列表中，选择合适的队列。

LSF 根据以下约束条件选择合适的队列：

- ##### 用户访问限制

  不允许该用户提交作业的队列，不会予以考虑。

- ##### 节点限制

  如果作业明确指定了可以在其上运行作业的主机节点列表，则必须将所选的队列，配置为作业发送到列表中的主机。

- ##### 队列状态

  不考虑关闭的队列。

- ##### 排他执行限制

  如果作业需要排他执行，则未配置为接受排他作业的队列，将不予考虑。

- ##### 作业所需的资源

  作业请求的资源，必须在所选队列的资源分配限制内。

如果多个队列满足上述要求，则选择满足要求的候选队列中，列出的第一个队列。