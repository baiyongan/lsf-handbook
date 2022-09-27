# 1.1 LSF 简介 

## Spectrum LSF: 高效的集群管理系统

计算机通过执行程序，帮助科研人员进行科学研究。通常，计算机的使用者不关心程序的执行过程，他们只希望更快更有效地获取运算结果。而为了提供强大的计算能力，大量的计算资源以集群的形式出现。集群系统的使用和有效管理都面临着挑战。

LSF（Load Sharing Facility）是一款分布式集群管理系统软件，负责计算资源的管理和批处理作业的调度。它给用户提供统一的集群资源访问接口，让用户透明地访问整个集群资源。同时提供了丰富的功能和可定制的策略。LSF 具有良好的可伸缩性和高可用性，支持几乎所有的主流操作系统。它通常是高性能计算环境中不可或缺的基础软件。

LSF 虽然是一款商业软件，但它同时也提供免费的社区版供大家下载和使用。

## 简单的使用

LSF 的使用者可以大约分为两类，普通用户和集群系统管理员。普通用户可以通过命令，将计算程序提交给集群执行，获取计算结果。系统管理员可以通过配置文件和管理命令，管理集群以及统计计算资源的使用情况。

##### 图 1. LSF 结构图

![img](https://www.ibm.com/developerworks/cn/linux/l-lo-efficient-cluster-manage-system-LSF/image001.png)

普通用户提交可执行程序或脚本给 LSF。LSF 将已提交的程序称为作业。作业在LSF 的队列 (Queue) 里排队 (PEND) ，等待调度。

##### 清单 1.  提交作业

```shell
lsfrhel01 # bsub –R "linux" sleep 1000
Job <1> is submitted to default queue <normal>.
lsfrhel01 # bjobs
JOBID   USER    STAT  QUEUE      FROM_HOST   EXEC_HOST   JOB_NAME   SUBMIT_TIME
1       tom     PEND  normal     lsfrhel01               *eep 1000  May  9 15:42
```

LSF 根据配置的调度策略，把作业分配到最合适的计算节点上执行 (RUN) 。用户可以通过命令行查看，控制作业的执行过程。除此之外，LSF 还为用户提供了作业修改，需求描述，作业控制等多种命令行工具。

##### 清单 2. 查看运行作业

```shell
lsfrhel01 # bjobs
JOBID   USER    STAT  QUEUE      FROM_HOST   EXEC_HOST   JOB_NAME   SUBMIT_TIME
1       tom     RUN   normal     lsfrhel01   lsfrhel02   *eep 1000  May  9 15:42
```

系统管理员通常需要了解整个集群系统中作业和资源的使用状况，LSF 提供的命令帮助管理员快速直观地看到系统概况：系统中队列的状态，机器的状态，作业的资源使用概况，等等。除此之外，LSF 还为管理员提供了丰富的集群配置，控制，管理等功能。

##### 清单 3. 查看 LSF 系统信息

```shell
lsfrhel01 # bqueues normal
QUEUE_NAME      PRIO STATUS          MAX JL/U JL/P JL/H NJOBS  PEND   RUN  SUSP
normal           30  Open:Active       -    -    -    -     1     0     1     0
 
lsfrhel01 # bhosts
HOST_NAME          STATUS       JL/U    MAX  NJOBS    RUN  SSUSP  USUSP    RSV
lsfrhel01          ok              -      4      0      0      0      0      0
lsfrhel02          ok              -      8      1      1      0      0      0
 
lsfrhel01 # bacct
Accounting information about jobs that are:
  - submitted by users tom,
  - accounted on all projects.
  - completed normally or exited
  - executed on all hosts.
  - submitted to all queues.
  - accounted on all service classes.
------------------------------------------------------------------------------
 
SUMMARY:      ( time unit: second )
 Total number of done jobs:       1      Total number of exited jobs:     4
 Total CPU time consumed:       4.4      Average CPU time consumed:     0.9
 Maximum CPU time of a job:     4.3      Minimum CPU time of a job:     0.0
 Total wait time in queues: 276962.0
 Average wait time in queue:55392.4
 Maximum wait time in queue:276953.0      Minimum wait time in queue:    2.0
 Average turnaround time:     60739 (seconds/job)
 Maximum turnaround time:    276953      Minimum turnaround time:        12
 Average hog factor of a job:  0.00 ( cpu time / turnaround time )
 Maximum hog factor of a job:  0.00      Minimum hog factor of a job:  0.00
 Average expansion factor of a job:  55610.95 ( turnaround time / run time )
 Maximum expansion factor of a job:  276953.00
 Minimum expansion factor of a job:  1.00
 Total Run time consumed:      6981      Average Run time consumed:    1396
 Maximum Run time of a job:    6914      Minimum Run time of a job:       0
 Total throughput:           409.09 (jobs/hour)  during    0.01 hours
 Beginning time:       May  9 15:39      Ending time:          May  9 15:40
```

## 基本概念

LSF 是资源管理的工具，它管理的主要对象有三个方面：机器（节点），作业和用户。

一般情况下，集群中的机器都是对等的，称为服务节点（Sever Host）。它们既可以提交作业，也可以执行作业。按照职能的不同，服务节点可以有不同的身份。管理作业调度资源的节点称为主节点（Master host），一个集群只有一个主节点。对于一次作业提交来说，提交作业的节点为提交节点（Submission host），被分配并执行作业的节点是执行节点（Execution host）。

##### 图 2. 节点角色

![img](https://www.ibm.com/developerworks/cn/linux/l-lo-efficient-cluster-manage-system-LSF/image002.png)

为了便于机器的管理，LSF 提供节点组（Host group）的概念。任意的机器集合可以被作为整体命名，通过名字在集群范围内整体引用。一种典型的用法是将节点按照内存大小进行分类：大内存节点组和小内存节点组。不同的作业可以请求不同的节点组，LSF 按照请求，分配该节点组中的机器来执行作业。节点组还有一个灵活的特性：为方便管理，同一台机器可以定义到不同的节点组。

##### 图 3. 节点分组

![img](https://www.ibm.com/developerworks/cn/linux/l-lo-efficient-cluster-manage-system-LSF/image003.png)

作业占用机器资源进行计算。每一个机器被划分成若干个槽位（slot） 。每一个槽位通常可以容纳一个作业运行。 通常情况下，每一个槽位和一个CPU 核心（core）相对应。**槽位是一个容易混淆的概念，为便于理解，可以将槽位等同于CPU 核心来看待。**对于并行作业来说，比如MPI 作业，每一个都需要占用更多的槽位加速计算。

作业的管理是以队列（Queue）为单位的，调度的策略也是按照队列定制的。作为作业的容器，可以配置多个队列定制不同策略。LSF 按照队列的优先级，从高到低调度每一个队列中的作业，为其分配资源。高优先级队列的作业对资源的使用具有优先权。

##### 图 4. 调度方式

![img](https://www.ibm.com/developerworks/cn/linux/l-lo-efficient-cluster-manage-system-LSF/image004.png)

　　

用户是作业提交者，也是资源的真正使用者。对于资源和作业的管理，不少策略都是以用户为单位。为了更好管理用户，LSF 引入用户组（user group）。若干用户集合可以统一命名，并使用该命名统一引用。例如，一个人属于一个部门，一个部门可以作为一个用户组，这种情况下就可以使用部门名字命名和引用。

## 体系结构

LSF 采用传统的客户机服务器模式，主节点负责整个集群的管理，从节点负责管理运行其上的作业的管理。每一个服务节点包含三个后台进程：

- **Sbatchd**

批处理作业管理进程。负责在本节点上执行作业，监控作业状态以及收集其使用的资源。同时根据用户请求或者系统策略触发，控制作业的状态，比如发送SIGSTOP 给作业、挂起作业运行等。

- **RES**

远程执行服务进程。负责执行远程客户请求的任务，主要用于并行作业的远程任务启动、监控以及控制。

- **LIM**

采集本节点的负载信息进程。将收集到的资源负载信息周期上报给主节点上的LIM。主节点的LIM 拥有整个集群资源状态，为其它服务提供集群系统范围内的资源当前快照。



主管理节点在这个基础上，包括两个额外的进程：

- **Mbatchd**

集群管理服务进程。它是 LSF 的中心：通过主节点的 LIM 获取机器以及相关资源信息，处理远程用户的作业提交请求，委托 mbschd 将作业调度到相关资源上，发送调度结果到指定机器，并通过和 sbatchd 的交互，监控作业使用的资源，控制作业的执行过程。

- **Mbschd**

调度策略服务进程。从 mbachd 获取作业和资源信息，根据定制策略，为 mbatchd 提供作业调度服务。

##### 图 5. 体系结构

![img](https://www.ibm.com/developerworks/cn/linux/l-lo-efficient-cluster-manage-system-LSF/image005.png)

当一个新作业提交的时候，集群管理服务进程检查作业的合法性，并将作业放入到指定的队列中等待调度。经过调度的作业，将获得执行机器上的slot、内存等资源。LSF 负责保留相关资源并将作业指派到已分配机器上执行。作业的状态和实际使用的资源通过批处理作业管理进程报告给集群管理进程。

集群系统构建在分布式网络节点上，节点的失效和网路设备的故障都会导致集群系统的基础环境改变。集群系统的高可用性功能可以保证即使在底层设备故障，LSF 系统仍然可以提供可靠稳定的服务。**LSF 采用主备模式实现系统的故障恢复。**LSF 的主节点将运行时事件信息写入网络文件系统。当主节点失效后，相关备节点进行选举，选出新的主节点。新的主节点从事件信息文件中恢复作业信息、机器状态，最终获取集群控制权，恢复LSF 状态。

为了更进一步扩展 LSF 的资源管理范围和方式，在单一集群基础上，LSF 还提供多集群互联技术（Multi-Cluster）。多集群通过互联，共享跨集群资源，提供更强大的计算能力。下面是一种典型的多集群架构，集群 1 负责接收作业提交和转发，集群 2 和 集群 3 负责作业执行。

##### 图 6. 多集群结构

![img](https://www.ibm.com/developerworks/cn/linux/l-lo-efficient-cluster-manage-system-LSF/image006.png)

## 资源调度

LSF 收集每一个节点的处理器、内存、交换区、临时存储区等资源信息。主节点掌握全局资源信息。资源的管理和调度以这些信息为基础。

##### 清单 4. 查看节点资源负载信息

```shell
lsfrhel01 # lshosts
HOST_NAME      type    model  cpuf ncpus maxmem maxswp server RESOURCES
lsfrhel01    X86_64   PC6000 116.1     2   1.4G   1.4G    Yes (mg)
lsfrhel02    X86_64   PC6000 116.1     2   1.4G   1.4G    Yes ()
lsfrhel01 # lsload
HOST_NAME       status  r15s   r1m  r15m   ut    pg  ls    it   tmp   swp   mem
lsfrhel01           ok   0.4   0.0   0.0   0%   0.0   1   179   10G  1.4G  1.1G
lsfrhel02           ok   1.5   0.3   0.3   1%   0.1   2     1 2391M  1.2G  603M
```

**作业在使用资源的时候，主要考虑三个方面**：如何根据作业的资源描述**选择**合适的执行机器，如何**预留**机器资源减少运行时的资源竞争，以及如何**限制**作业对资源的使用避免作业过度消耗资源。

首先是选择执行机。每一个作业会有不同的资源需求。可以通过 LSF 定义的资源描述模式请求资源，运行节点由LSF 根据作业对资源描述来匹配。当一个作业需要一定量内存的时候，"select[mem>512]" 表示选择内存大于512M 的机器来运行作业。调度器为其选择拥有合适资源的机器。

其次是确保执行机上的资源分配。既然我们选择了大内存的机器，那么别人的作业也可以选择大内存的机器。如果很多作业都在大内存机器上运行，资源竞争会导致内存短缺，作业最终无法占用到请求的资源。为了更好的确保资源，我们需要在作业运行时保留这些资源不会再分配给别人的作业。"rusage[mem=512]" 表示保留 512M                内存给作业，节点当前可用内存将会有 512M 分配给该作业，节点可分配资源将减少512M 的内存。通过 LSF                的策略，可用内存的分配得到控制，已经保留的内存将不会再分配给其它的作业。

最后是保证资源不被过度消耗。资源的保留是通过 LSF 的策略保证，但是作业的进程在运行时，却尚未受 LSF                控制。我们需要在执行节点上，对作业的系统资源设置限制，保证作业（进程）本身不会吃掉过多的内存。通常我们可以设置一个资源上限，防止作业过度消耗资源。比如，内存限制 '1024M'，防止作业使用超过1G 的内存。

##### 清单 5. 提交内存需求的作业

```shell
$ bsub -M 1024 -R "select[mem>512] rusage[mem=512]" sleep 1000
Job <2> is submitted to default queue <normal>.
$ bjobs  -l 644
 
Job <644>, User <tom>, Project <default>, Status <RUN>, Queue <normal>, Command
                     <sleep 1000>
Wed Dec 28 16:04:00: Submitted from host <lsfrhel01 >, CWD <$HOME/workplace/tes
                     t>, Requested Resources <select[mem>512] rusage[mem=512]>;
 
 MEMLIMIT
      1 G
Wed Dec 28 16:04:00: Started 1 Task(s) on Host(s) <lsfrhel02>, Allocated 1 Slot
                    (s) on Host(s) <lsfrhel02>, Execution Home </home/tom>, Exe
                     cution CWD </home/tom/workplace/test>;
Wed Dec 28 16:05:00: Resource usage collected.
                     The CPU time used is 4 seconds.
                     MEM: 6 Mbytes;  SWAP: 0 Mbytes;  NTHREAD: 4
                     PGID: 23106;  PIDs: 23106 23108 23110
 
 SCHEDULING PARAMETERS:
           r15s   r1m  r15m   ut      pg    io   ls    it    tmp    swp    mem
 loadSched   -     -     -     -       -     -    -     -     -      -      -
 loadStop    -     -     -     -       -     -    -     -     -      -      -
 
 RESOURCE REQUIREMENT DETAILS:
 Combined: select[(mem>512) && (type == local)] order[r15s:pg] rusage[mem=512.0
                     0]
 Effective: select[(mem>512) && (type == local)] order[r15s:pg] rusage[mem=512.
                     00]
```

**对于资源的选择、预留和限制，内存只是一个例子。 LSF 还支持很多种资源，比如 CPU、交换区、临时目录大小等等。**虽然这些默认管理的资源始终是有限的，但是 LSF 还提供了资源管理的扩展机制。用户可以统过编写自己的 ELIM 来收集自定义的资源。比如，收集系统的网络带宽以及网络负载，作业可以通过资源描述，选择拥有相应带宽的节点执行作业。资源的种类很多，LSF 提供布尔类型、字符串类型和数字类型来描述多种多样的资源。

## 定制策略

LSF 提供了非常丰富的调度策略供 LSF 系统管理员选择配置。策略针对作业和资源，从提高资源利用率、优化资源分配、提高用户满意度等各个方面为资源的使用者和管理者提供可配置策略。

**默认的策略是先来先服务（FCFS）**。顾名思义，先提交的作业先调度，优先获得资源。排在后面的作业必须等待前面的作业运行完成才能开始。后提交作业可能在很长时间得不到机会运行。考虑到资源分配的公平问题，比如部门之间应该平等使用资源，**公平共享（Fairshare）策略**得以引入。通过配置以部门为单位的用户组平等分享资源，不同用户的作业优先考虑资源所有权。避免了先来先服务导致的资源不平等，从而优化资源分配。

公平共享是从资源分配公平性上考虑问题的，它达到的是一个最终资源使用公平的平衡。但是在使用过程中，如果其他人或者部门没有作业，那么整个集群的资源将会被分配给目前已经提交的作业。作业执行期间，即便新的作业拥有更多的资源优先使用权，也要等待其他作业执行完毕，释放资源后才能执行。这样在短时期内资源使用是不公平的。对于拥有资源使用权却无法执行的情况，**资源保障（Resource Guarantee）策略**可以为用户保留资源，随时可用。这是在牺牲资源利用率基础上提高用户满意度。

对于并行作业，通常要求很多的 slot，当系统资源紧张的时候，即使等待很久依然无法运行。当系统释放一个 slot                的时候，这个作业因为发现资源不够，便放弃对资源的优先权。排在后面的只需要一个 slot 的作业将获取资源执行。这个过程反复着，并行作业始终无法获取足够资源。为了解决这个问题引入了资源保留策略。虽然当前资源不够运行的，但是这个资源暂时被并行作业占有，等待后面不断释放的资源，直到 slot 满足作业的需求。

但是长时间的等待还是会浪费这些空闲资源，因此又加入**回填策略**。在不影响并行作业启动时间的前提下，可以将短作业优先调度到已经被保留的 slot 上。

对于特权或者紧急的用户或者应用，当系统资源完全使用的时候。为了尽快执行，**抢占（Preemption）策略**可以通过抢占已执行作业的资源，执行自己的作业。

除此之外，为了满足用户需求，LSF 提供了**资源预留（Advanced Reservation）、SLA** 等等。为了提高资源利用率，LSF 提供了**NUMA绑定（Affinity）策略**等等。对于详尽的策略，可以参考 LSF 管理员手册。LSF 的很多策略都可以自由组合，通过管理员的配置，最终形成丰富的，满足各种需求的定制策略。

即便所有的策略都不能满足你的要求，**LSF 的调度策略还实现了插件机制。新的扩展可以通过 LSF 提供的API 实现新的策略**。

## 总结

在高性能计算领域，作业管理系统是一种成熟的系统软件技术。LSF 作为其中的佼佼者，提供了统一的访问接口，丰富的调度策略，灵活的配置和部署。LSF 的体系结构和部署方式让它可以有效管理一定规模的集群系统，目前商业版可以支持多达数千台节点和数百万作业的管理。LSF 的故障恢复机制足以保证集群系统的高可用性。在分布式计算技术不断发展的今天，作为传统的批处理管理软件，依然发挥着重要的作用。

## 参考资源

- 下载 [IBM Spectrum LSF Community Edition](https://www-01.ibm.com/marketing/iwm/iwm/web/preLogin.do?source=swerpzsw-lsf-3)，安装，试用LSF 的基本功能
- 参考 [IBM Spectrum LSF Knowledge Center](http://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_welcome/lsf_welcome.html),了解更多LSF 的使用和集群管理方法
- 参考 [IBM Spectrum LSF](http://www-03.ibm.com/systems/spectrum-computing/products/lsf/) 首页,察看更多LSF 产品和技术的最新信息

