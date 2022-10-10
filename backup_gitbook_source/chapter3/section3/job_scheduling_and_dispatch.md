# 作业调度与分配

提交的作业在队列中等待，直到将它们调度并分配到主机以执行。

将作业提交给 LSF 时，许多因素控制着作业开始的时间和地点:

- 队列或主机的活动时间窗口
- 作业的资源需求
- 合格主机的可用性
- 各种作业槽位限制
- 作业依赖条件
- Fairshare 限制（已配置的用户共享策略）
- 负载条件



## 调度策略

为了解决各种问题，LSF 允许在同一集群中，使用多种调度策略。 LSF 有几种队列调度策略，例如排他，抢占，公平共享和分层公平共享。

- 先来先服务（FCFS）调度: 

  默认情况下，队列中的作业按 FCFS 顺序分派。 这意味着作业将根据其在队列中的顺序进行调度。

- 服务水平协议（SLA）调度: 

  LSF 中的 SLA 是 “及时” 的调度策略，用于调度 LSF 管理员和 LSF 用户之间约定的服务。 SLA 调度策略定义应从每个 SLA 运行多少作业，以达到配置的目标。

- 公平共享调度: 

  如果您为队列指定一个公平共享调度策略，或者如果已配置主机分区，则 LSF 会根据分配的用户份额，资源使用，或其他因素在用户之间调度作业。

- 抢占式调度: 

  您可以指定所需的行为，以便当两个或多个作业竞争同一资源时，一个作业优先于另一个作业。 抢占不仅适用于作业槽位，而且还适用于提前预订（为特定作业保留主机节点）和许可证（使用 IBM Platform License Scheduler）。

- 回填式调度：

  允许小型作业在为其他作业保留的作业槽位上运行，前提是，回填作业在保留时间到期，且资源使用到期之前完成。

## 调度与分配

定期安排作业（默认为5秒）。 一旦安排了作业，就可以立即将其分配给主机。

为了防止任何节点过载，默认情况下，LSF 在将作业分发到同一节点之间，会等待一小段时间。

### 分配顺序

作业不一定按提交顺序分派。

定义队列时，每个队列都有一个由 LSF 管理员设置的优先级编号。LSF 会尝试首先从优先级最高的队列中，启动作业。

LSF 按以下顺序考虑要分派的作业：

- 对于每个队列，从最高优先级到最低优先级。 如果多个队列具有相同的优先级，则 LSF 会按照先来先服务（FCFS）的顺序，调度这些队列中的所有作业。
- 对于队列中的每个作业，根据 FCFS 顺序。
- 如果有任何主机有资格运行此作业，将在最合格的主机上启动该作业，并标记该主机不具备启动任何其他作业的资格，直到经过 **JOB_ACCEPT_INTERVAL** 参数所指定的时间段为止。