# 架构

LSF License Scheduler 管理许可证令牌，而不是直接控制许可证。 使用 LSF License Scheduler，作业在启动应用程序之前会收到许可证令牌。 IBM Spectrum LSF（LSF）和 IBM Spectrum LSF Advanced Edition（LSF Advanced Edition）可用的令牌数量，与许可证服务器上可用的许可证数量相对应，因此，如果令牌不可用，则作业不会启动。 这样，正在运行的作业所请求的许可证数量，不会超过可用许可证的数量。

作业开始时，应用程序不知道 LSF License Scheduler。 应用程序以通常的方式从许可证服务器中签出许可证。



![img](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/license_scheduler/lic_sched_daemons.jpg)图 1. 守护程序交互

## 调度策略如何工作

使用 LSF License Scheduler，LSF 可以收集有关待处理作业的许可要求的信息，以有效地分发可用的许可。 其他 LSF 调度策略独立于 LSF License Scheduler 策略。

开始作业时，基本的 LSF 调度排在第一位。 LSF License Scheduler 对作业调度优先级没有影响。 根据每个集群  中配置的优先级策略，将作业视为要分发。

例如，在 LSF License Scheduler 公平共享策略（此作业所属的许可证项目）适用之前，作业必须具有要在其上启动的候选 LSF 主机。

其他 LSF Fairshare 策略基于 CPU 时间，运行时间和使用情况。 如果配置了 LSF Fairshare 调度，则 LSF 确定哪个用户或队列具有最高优先级，然后考虑其他资源。 这样，其他 LSF Fairshare 策略的优先级高于 LSF License Scheduler。

## 当 mbatchd 脱机时

当集群运行时，**mbatchd** 保持与 **bld** 的 TCP 连接。 当集群断开连接时（例如，集群关闭或重新启动时），**bld** 会删除有关集群中作业的所有信息。 LSF 许可证计划程序将断开连接的集群中的作业签出的许可证，视为非 LSF 许可证使用。

当 **mbatchd** 重新联机时，**bld** 会立即收到有关当前分配给集群的令牌数量的更新信息。

## 当 bld 脱机时



如果 **mbatchd** 失去了与 **bld** 的连接，则 **mbatchd** 无法获得 **bld** 的令牌分配决定来更新自己的令牌。

但是，由于**mbatchd** 每分钟都会在 $LSF_TOP/work/data/featureName.ServiceDomainName.dat 文件中记录令牌状态，因此，如果连接断开，则 **mbatchd** 将使用最后记录的信息来调度作业。

```shell
f3.LanServer1.dat 
# f3 LanServer1 3 2
# p1 50 p2 50  
  12/3         14:20:38        2    0    2    0         1    0    1    0    
  12/3         14:21:39        2    0    2    0         1    0    1    0    
  12/3         14:22:40        3    3    0    0         0    0    0    0    
  12/3         14:23:41        3    3    0    0         0    0    0    0    
  12/3         14:24:42        1    0    1    0         2    0    2    0    
  12/3         14:25:43        1    0    1    0         2    0    2    0    
  12/3         14:26:44        1    0    1    0         2    0    2    0    
  12/3         14:27:55        1    0    1    0         2    0    2    0    
```

LanServer1 上的 f3 具有三个令牌和两个项目。 项目 p1 和 p2 共享许可证 50:50。

在 14:27:55，**bld** 向 p1 分配了一个令牌，该令牌有 0 个正在使用，1 个免费，0 个备用。 同时，**bld** 向 p2 分配了两个令牌，这些令牌有 0 个正在使用，2 个空闲和 0 个保留。

**mbatchd** 将继续基于基于 14:27:55 记录的令牌分布的作业进行调度，直到与 **bld** 的连接重新建立。

