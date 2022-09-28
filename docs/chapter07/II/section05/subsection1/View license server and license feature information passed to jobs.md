# 查看传递给作业的许可证服务器和许可证功能信息

## 任务说明

您可以显示分配给许可证功能的每个服务域所使用的许可证服务器。

## 步骤

运行 blstat -S.

```shell
blstat -S
FEATURE: feature1
SERVICE_DOMAIN: domain1
SERVERS     INUSE  FREE
 server1      1      0
 server2      0      1
 TOTAL        1      1
SERVICE_DOMAIN: domain2
SERVERS     INUSE  FREE
 server3      1      0
 TOTAL        1      0
```

许可证功能部件 1 被分配给 domain1 服务域中的 server1 和 server2，以及 domain2 服务域中的 server3。当作业以 “ rusage [feature1 = 1]” 作为 rusage 字符串提交时，该作业将使用 feature1 许可功能。



## 查看许可证使用情况

### 步骤

运行 **blstat -s** 以显示许可证使用情况。

```shell
blstat -s
FEATURE: p1_f2
SERVICE_DOMAIN: app_1 TOTAL_LICENSE: 10
LSF_USE LSF_DESERVE LSF_FREE   NON_LSF_USE NON_LSF_DESERVE  NON_LSF_FREE
     0       10         10          0           0                 0 
FEATURE: p1_f1
SERVICE_DOMAIN: app_1 TOTAL_LICENSE: 5  
LSF_USE LSF_DESERVE LSF_FREE   NON_LSF_USE NON_LSF_DESERVE  NON_LSF_FREE
     0       5          5           0           0                 0 
```

如果有任何违反分发策略的行为，**blstat** 会在行的开头用星号（*）标记这些违反行为。

## 查看作业负载分配信息

### 步骤

运行 **blinfo -a** 以显示 WORKLOAD_DISTRIBUTION 信息。

```shell
blinfo -a
FEATURE      MODE       SERVICE_DOMAIN  TOTAL  DISTRIBUTION
g1           Project    LS              10     [p1, 50.0%] [p2, 50.0%]
                                  WORKLOAD_DISTRIBUTION
                                  [LSF 66.7%, NON_LSF 33.3%]
```

## 排序许可证功能信息

### 任务说明

您可以按字母顺序，按总许可证或可用许可证，对许可证功能信息进行排序。

总许可证的价值，是根据向该功能部件提供许可证的所有服务域应得到的 LSF 工作负载应获得的许可证数量计算的，而不管非 LSF 工作负载是否从 LSF 工作负载借用了许可证。

### 步骤

- 按字母顺序排序:

  blstat -o alpha

- 按总许可证排序:

  blstat -o total

  总许可证数量最多的功能会首先显示。

- 按可用许可证排序:

  blstat -o avail

  首先显示具有可用许可证数量最多的功能。

  您也可以运行带有选项 **-Lp**, **-t**, **-D**, **-G**, **-s**, **-S** 的 **blstat -o**。

  ##### 提示

  当 **blstat -o** 与不同选项一起使用时，“total licenses” 和 “licenses available” 的值计算方式不同：

  - 选项 **-Lp**, **-t**, **-D**, **-G**: 许可证总数，是指从已配置的所有服务域分配给 LSF 作业负载的许可证总数，为该功能提供许可证。 由非 LSF 作业负载借用的许可证，将从该总和中减去。
  - 选项 **-s**, **-S**: 许可证总数，是指配置为向该功能提供许可证的所有服务域中的所有许可证（由许可证供应商守护程序提供）。

## 查看执行主机上运行的多个作业的限制

如果用户提交的多个作业在同一执行主机上运行，则 **blstat** 可能不会显示正确的许可证使用信息。 这是因为 **lmstat** 仅提供每个许可证签出的用户和主机信息，而没有为 LSF License Scheduler 提供将许可证签出与特定 LSF 作业匹配的其他信息。

LSF License Scheduler 尝试根据用户，执行主机和 rusage 字符串，将许可证签出与每个 LSF 作业进行匹配。如果在同一执行主机上运行的多个作业，是由同一用户提交并请求相同的许可证，则 **lmstat** 提供的信息不足以使 LSF License Scheduler 为每个 LSF 作业提供完全匹配的信息。 LSF License Scheduler 估计作业，但这可能不正确。

例如：

- 有多个提供相同功能的服务域，并且用户提交在同一执行主机上运行的多个作业。

  尽管 LSF License Scheduler 正确分配了令牌，但是 **blstat** 可能不会显示正确的令牌用法（例如 TOTAL_INUSE，TOTAL_RESERVE 或 TOTAL_FREE）。 不正确的令牌计入 OTHERS。

- 一台许可证服务器具有多个项目，一个用户提交多个作业，其中一些作业一次保留令牌。 保留令牌的作业与其他 LSF License Scheduler 作业在同一主机上运行。

  尽管 LSF License Scheduler 正确分配了令牌，但 **blstat** 可能会显示相反的令牌用法，因此某些 INUSE 令牌计入 RESERVED 中，而某些 RESERVED 令牌计入 INUSE 中。