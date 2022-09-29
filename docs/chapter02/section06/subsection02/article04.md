# 查看批处理系统状态

使用 **bhosts** 命令查看 LSF 批处理作业负载系统是否正常运行。 **bqueues** 命令显示可用队列的状态及其配置参数。

要使用 LSF 批处理命令，集群必须已启动并正在运行。 有关启动 LSF 守护程序的信息，请参见 [Starting your cluster](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_admin_foundations/start_cluster.html?view=kc#start_cluster964) 。

## bhosts 命令

**bhosts** 命令显示集群中 LSF 批处理服务器主机的状态，以及有关批处理主机的其他详细信息：

- 单个用户允许的最大作业槽位数
- 系统中的作业总数，正在运行的作业，用户暂停的作业以及系统暂停的作业
- 预留作业槽位总数

集群中所有主机的正常状态都显示正常。

```shell
% bhosts
HOST_NAME          STATUS       JL/U    MAX  NJOBS    RUN  SSUSP  USUSP    RSV 
hosta              ok              -      -      0      0      0      0      0
hostb              ok              -      -      0      0      0      0      0
hostc              ok              -      -      0      0      0      0      0
hostd              ok              -      -      0      0      0      0      0
```

如果在启动或重新配置 LSF 时看到以下消息，请等待几秒钟，然后再次尝试 **bhosts** 命令，以使 **mbatchd **守护程序有时间进行初始化。

```shell
batch system daemon not responding ... still trying
```

如果问题仍然存在，请参阅 [Solving common LSF problems](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_admin/troubleshooting_common_problems_lsf.html?view=kc#v3534299) 以寻求帮助。

## bqueues 命令

LS F队列组织具有不同优先级，和不同调度策略的作业。

**bqueues ** 命令显示可用队列的状态及其配置参数。 要使队列接受和调度作业，状态必须为 Open:Active。

```shell
% bqueues
QUEUE_NAME      PRIO STATUS          MAX JL/U JL/P JL/H NJOBS  PEND   RUN  SUSP 
owners           43   Open:Active      -    -    -    -     0     0     0     0
priority         43   Open:Active      -    -    -    -     0     0     0     0
night            40    Open:Inact      -    -    -    -     0     0     0     0
chkpnt_rerun_qu  40   Open:Active      -    -    -    -     0     0     0     0
short            35   Open:Active      -    -    -    -     0     0     0     0
license          33   Open:Active      -    -    -    -     0     0     0     0
normal           30   Open:Active      -    -    -    -     0     0     0     0
idle             20   Open:Active      -    -    -    -     0     0     0     0
```

要查看更多详细的队列信息，请使用 **bqueues -l** 命令：

```shell
% bqueues -l normal

QUEUE: normal
  -- For normal low priority jobs, running only if hosts are lightly loaded.  This is the default queue.

PARAMETERS/STATISTICS
PRIO NICE STATUS          MAX JL/U JL/P JL/H NJOBS  PEND   RUN SSUSP USUSP  RSV
 30   20  Open:Active       -    -    -    -     0     0     0     0     0    0
Interval for a host to accept two jobs is 0 seconds

SCHEDULING PARAMETERS
           r15s   r1m  r15m   ut      pg    io   ls    it    tmp    swp    mem
 loadSched   -     -     -     -       -     -    -     -     -      -      -
 loadStop    -     -     -     -       -     -    -     -     -      -      -

SCHEDULING POLICIES:  FAIRSHARE  NO_INTERACTIVE
USER_SHARES:  [default, 1]

USERS: all
HOSTS:  all
```

bqueues -l 命令显示有关队列的以下信息：

- 什么类型的作业要在队列上运行
- 资源使用限制
- 能够使用队列的主机和用户
- 调度阈值：
  - loadSched 是 LSF 停止自动分派作业的阈值
  - loadStop 是 LSF 自动挂起作业的阈值

## 其他有用的命令

- **bparams** 命令显示有关 LSF 批处理系统配置参数的信息。
- **bhist ** 命令显示有关作业的历史信息。