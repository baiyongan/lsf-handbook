# 1.7 LSF 快速上手

本文主要是关于 LSF 命令、守护进程、配置文件、日志文件以及重要的集群配置参数的快速介绍。



## Unix 及 Linux 系统下的安装目录示意图

![Sample UNIX and Linux installation directories](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_quick_reference/lsf_unix_dirmap.jpg)





## 守护进程的错误日志文件

守护进程的错误日志文件，存储在由 **LSF_LOGDIR** 变量定义的文件目录下面，该变量值在 lsf.conf 文件中指定。

------

| LSF base system daemon log files | LSF batch system daemon log files |
| :------------------------------- | :-------------------------------- |
| pim.log.host_name                | mbatchd.log.host_name             |
| res.log.host_name                | sbatchd.log.host_name             |
| lim.log.host_name                | mbschd.log.host_name              |

------

如果在 ego.conf 文件中定义了变量 **EGO_LOGDIR** ，那么 lim.log.host_name 文件则存储在由变量 EGO_LOGDIR 指定的文件目录中。



## 配置文件

lsf.conf, lsf.shared, 和 lsf.cluster.cluster_name 文件， 位于由 **LSF_CONFDIR** 变量定义的文件目录下面，该变量值在 lsf.conf 文件中指定。

lsb.params, lsb.queues, lsb.modules, 和 lsb.resources 文件，位于 **LSB_CONFDIR**/cluster_name/configdir/ 目录下面。

------

| 文件                     | 描述                                                         |
| :----------------------- | :----------------------------------------------------------- |
| install.config           | LSF 的安装与配置选项                                         |
| lsf.conf                 | 描述集群配置和操作的通用环境配置文件                         |
| lsf.shared               | 所有群集共享的定义文件。用于定义群集名称、主机类型、主机型号和站点定义的资源 |
| lsf.cluster.cluster_name | 用于定义主机、管理员和站点定义的共享资源的位置的集群配置文件 |
| lsb.applications         | 定义应用程序配置文件，来指定同类型作业的公共参数             |
| lsb.params               | 配置 LSF 批处理参数                                          |
| lsb.queues               | 批处理队列配置文件                                           |
| lsb.resources            | 配置资源分配限制、导出和资源使用限制                         |
| lsb.serviceclasses       | 将LSF集群中的服务级别协议（SLA）定义为服务类，该服务类定义了 SLA 的属性 |
| lsb.users                | 配置用户组、用户和用户组的分层公平共享，以及用户和用户组的作业槽数限制 |

------



## lsf.conf 配置文件中的集群配置参数

------

| 参数                 | 描述                                                         | Unix 默认值                              |
| :------------------- | :----------------------------------------------------------- | :--------------------------------------- |
| **LSF_BINDIR**       | 包含 LSF 用户命令的目录，由相同类型的所有主机共享            | LSF_TOP/version/OStype/bin               |
| **LSF_CONFDIR**      | 所有 LSF 配置文件的目录                                      | LSF_TOP/conf                             |
| **LSF_ENVDIR**       | 包含 lsf.conf 文件的目录。必须由root 用户所拥有。            | /etc (if **LSF_CONFDIR** is not defined) |
| **LSF_INCLUDEDIR**   | 包含 LSF API 头文件 lsf.h 和 lsbatch.h的目录                 | LSF_TOP/version/include                  |
| **LSF_LIBDIR**       | LSF 库，由相同类型的所有主机共享                             | LSF_TOP/version/OStype/lib               |
| **LSF_LOGDIR**       | （可选）LSF 守护程序日志的目录。必须由 root 拥有。           | /tmp                                     |
| **LSF_LOG_MASK**     | 从 LSF 命令记录错误消息的级别                                | **LOG_WARNING**                          |
| **LSF_MANDIR**       | 包含 LSF 手册页的目录                                        | LSF_TOP/version/man                      |
| **LSF_MISC**         | 示例C程序和Shell脚本，以及外部LIM（**elim**）的模板          | LSF_TOP/version/misc                     |
| **LSF_SERVERDIR**    | 由 LSF 守护程序启动的所有服务器二进制文件和 Shell 脚本以及外部可执行文件的目录。必须由root拥有，并由相同类型的所有主机共享 | LSF_TOP/version/OStype/etc               |
| **LSF_TOP**          | 顶级安装目录。 LSF_TOP 的路径必须共享，并且集群中的所有主机都可以访问。它不能是根目录（/）。 | Not definedRequired for installation     |
| **LSB_CONFDIR**      | LSF批处理配置目录的目录，包含用户和主机列表，操作参数和批处理队列 | LSF_CONFDIR/lsbatch                      |
| **LSF_LIVE_CONFDIR** | LSF 实时重新配置目录的目录，该目录由 **bconf** 命令编写。    | LSB_SHAREDIR/cluster_name/live_confdir   |
| **LSF_SHAREDIR**     | 每个集群的 LSF 批处理作业历史记录和记帐日志文件的目录，必须由首要的 LSF 管理员拥有 | LSF_TOP/work                             |
| **LSF_LIM_PORT**     | 用于与 lim 守护程序进行通信的 TCP 服务端口                   | 7879                                     |
| **LSF_RES_PORT**     | 用于与 **res** 守护程序通信的 TCP 服务端口                   | 6878                                     |
| **LSF_MBD_PORT**     | 用于与 **mbatchd** 守护程序进行通信的 TCP 服务端口           | 6881                                     |
| **LSF_SBD_PORT**     | 用于与 **sbatchd** 守护程序进行通信的TCP服务端口             | 6882                                     |

------



## 管理命令

注：只有 LSF 管理员和 root 用户可以使用这些命令。

------

| 命令            | 描述                                                         |
| :-------------- | :----------------------------------------------------------- |
| **lsadmin**     | LSF 管理员工具，用于控制 LSF 集群中 LIM 和 RES 守护程序的运行，**lsadmin help** 显示所有子命令 |
| **lsfinstall**  | 使用 install.config 输入文件安装 LSF                         |
| **lsfrestart**  | 在本地集群中的所有主机上重新启动 LSF 守护程序                |
| **lsfshutdown** | 关闭本地集群中所有主机上的 LSF 守护程序                      |
| **lsfstartup**  | 在本地集群中的所有主机上启动 LSF 守护程序                    |
| **badmin**      | 用于控制 LSF 批处理系统（**sbatchd**，**mbatchd**，主机和队列）的 LSF 管理工具 **badmin help** 显示所有子命令 |
| **bconf**       | 更改活动内存中的 LSF 配置                                    |

------



## 守护进程

------

| 进程名      | 描述                                                         |
| :---------- | :----------------------------------------------------------- |
| **lim**     | Load Information Manager (LIM): 负载信息管理器：收集有关集群中所有服务器主机的负载和资源信息，并通过 LSLIB 为应用程序提供主机选择服务。 LIM 维护有关静态系统资源和动态负载索引的信息 |
| **mbatchd** | Master Batch Daemon (MBD): 主批处理守护程序：接受并保存所有批处理作业。 MBD通过联系 主LIM 定期检查所有服务器主机上的负载索引。 |
| **mbschd**  | Master Batch Scheduler Daemon：主批处理调度守护程序：执行LSF的调度功能，并将作业调度决策发送到 MBD 以进行调度。 该服务在 LSF 主服务器主机上运行 |
| **sbatchd** | Slave Batch Daemon (SBD)：从属批处理守护程序（SBD）：接受来自 MBD 的作业执行请求，并监视作业进度。 控制作业执行，强制执行批处理策略，将作业状态报告给 MBD，然后启动 MBD。 |
| **pim**     | Process Information Manager (PIM): 进程信息管理器（PIM）：监视提交的作业在运行时所使用的资源。 PIM 用于强制执行资源限制和负载阈值以及公平分配调度。 |
| **res**     | Remote Execution Server (RES): 远程执行服务器（RES）：接受来自所有负载共享应用程序的远程执行请求，并处理远程主机上的I / O以进行负载共享过程。 |

------



## 用户命令

### 查看集群信息的命令

------

| 命令        | 描述                                        |
| :---------- | :------------------------------------------ |
| **bhosts**  | 显示主机及其静态和动态资源                  |
| **blimits** | 显示正在运行的作业的资源分配限制的相关信息  |
| **bparams** | 显示可调批次系统参数的相关信息              |
| **bqueues** | 显示批处理队列的相关信息                    |
| **busers**  | 显示用户和用户组的相关信息                  |
| **lshosts** | 显示主机及其静态资源信息                    |
| **lsid**    | 显示当前的 LSF 版本号，集群名称和主控主机名 |
| **lsinfo**  | 显示负载分担配置信息                        |
| **lsload**  | 显示主机的动态负载索引                      |

------



### 监测作业与任务的命令

------

| 命令        | 描述                                                       |
| :---------- | :--------------------------------------------------------- |
| **bacct**   | 报告已完成的 LSF 作业的会计统计数据                        |
| **bapp**    | 显示附加到应用程序配置文件的作业的相关信息                 |
| **bhist**   | 显示作业的相关历史信息                                     |
| **bjobs**   | 显示作业的相关信息                                         |
| **bpeek**   | 显示未完成作业的标准输出和标准错误                         |
| **bsla**    | 显示服务类配置的相关信息，以用于面向目标的服务级别协议调度 |
| **bstatus** | 读取或设置外部作业状态消息和数据文件                       |

------



### 提交与控制作业的命令

------

| 命令         | 描述                                     |
| :----------- | :--------------------------------------- |
| **bbot**     | 移动正在等待的作业到队列的末尾           |
| **bchkpnt**  | 检查点可检查的工作                       |
| **bkill**    | 向作业发送信号，一般用于结束作业         |
| **bmig**     | 迁移可检查点的或可重新运行的作业         |
| **bmod**     | 修改作业的提交选项                       |
| **brequeue** | 杀死并重新安排作业                       |
| **bresize**  | 释放槽位并取消挂起的作业调整大小分配请求 |
| **brestart** | 重新启动检查点作业                       |
| **bresume**  | 恢复暂停的作业                           |
| **bstop**    | 暂停作业                                 |
| **bsub**     | 提交作业                                 |
| **bswitch**  | 将未完成的作业从一个队列移至另一队列     |
| **btop**     | 移动正在等待的作业到队列首部             |

------



## bsub 命令

 **bsub** [options] command [arguments] 命令中的部分选项

------

| 选项                                                         | 描述                                                         |
| :----------------------------------------------------------- | :----------------------------------------------------------- |
| **-ar**                                                      | 指定作业可自动调整大小                                       |
| **-H**                                                       | 提交时将工作保持在 PSUSP 状态                                |
| **-I\|-Ip\|-Is**                                             | 提交批处理交互式作业。 **-Ip **创建伪终端。 **-is **在shell模式下创建一个伪终端。 |
| **-K**                                                       | 提交作业并等待作业完成                                       |
| **-r**                                                       | 使作业可重新运行                                             |
| **-x**                                                       | 排他执行                                                     |
| **-app** application_profile_name                            | 将作业提交到指定的应用程序配置文件                           |
| **-b** begin_time                                            | 在[[month：] day：]：minute 格式的指定日期和时间或之后调度作业 |
| **-C** core_limit                                            | 为属于此作业的所有进程设置每个进程（soft）核心文件的大小限制（KB） |
| **-c** cpu_time[/host_name \| /host_model]                   | 限制作业可以使用的总CPU时间。 CPU时间的格式为[hour:]minutes  |
| **-cwd** "current_working_directory"                         | 指定作业的当前工作目录                                       |
| **-D** data_limit                                            | 为属于作业的每个进程设置每个进程（soft）数据段的大小限制（KB） |
| **-E** "pre_exec_command [arguments]"                        | 在作业运行之前，在执行主机上运行指定的pre-exec命令           |
| **-Ep** "post_exec_command [arguments]"                      | 作业完成后，在执行主机上运行指定的post-exec命令              |
| **-e** error_file                                            | 将标准错误输出附加到文件                                     |
| **-eo** error_file                                           | 将作业的标准错误输出覆盖到指定文件                           |
| **-F** file_limit                                            | 为属于作业的每个进程设置每个进程（soft）文件大小限制（KB）   |
| **-f** "local_file op[remote_file]" ...                      | 在本地（提交）主机和远程（执行）主机之间复制文件。op是>，<，<<，> <，<>之一 |
| **-i** input_file \| **-is** input_file                      | 从指定文件获取作业的标准输入                                 |
| **-J** "job_name[index_list]%job_slot_limit"                 | 为作业分配指定的名称。 作业数组 index_list  的格式 start [-end [：step]]，而 ％job_slot_limit 是可以同时运行的最大作业数。 |
| **-k** "chkpnt_dir \[chkpnt_period][method=method_name]"     | 使作业可检查，并指定检查点目录，以分钟为单位的时间段和方法   |
| **-M** mem_limit                                             | 设置每个进程（soft）的内存限制（KB）                         |
| **-m** "host_name \[@cluster_name][[!] \| +[pref_level]] \| host_group[[!] \|+[pref_level]] \| compute_unit[[!] \|+[pref_level]]..." | 在指定的主机之一上运行作业。 主机或组的名称后的加号（+）表示首选项。 可选地有，正整数表示偏好级别。 数字越高表示偏好越大。 |
| **-n** min_proc[,max_proc]                                   | 指定并行作业所需的最小和最大处理器数量                       |
| **-o** output_file                                           | 将标准输出附加到文件                                         |
| **-oo** output_file                                          | 将作业的标准输出覆盖到指定文件                               |
| **-p** process_limit                                         | 限制整个作业的进程数量                                       |
| **-q** "queue_name ..."                                      | 将作业提交到指定的队列之一                                   |
| **-R** "res_req" [-R "res_req" ...]                          | 指定主机资源要求                                             |
| **-S** stack_limit                                           | 为属于作业的每个进程设置每个进程（soft）堆栈段大小限制（KB） |
| **-sla** service_class_name                                  | 指定要在其中运行作业的服务类                                 |
| **-T** thread_limit                                          | 设置整个作业的并发线程数限制                                 |
| **-t** term_time                                             | 以 [[month：] day：] hour：minute 的形式指定作业终止的截止日期 |
| **-v** swap_limit                                            | 设置整个作业的总进程虚拟内存限制（KB）                       |
| **-W** run_time[/host_name \| /host_model]                   | 以[hour：] minute形式设置作业的运行时限制                    |
| **-h**                                                       | 将命令用法打印到 stderr 并退出                               |
| **-V**                                                       | 将 LSF 发行版本打印到 stderr 并退出                          |

------