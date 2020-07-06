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
| **mbschd**  | Master Batch Scheduler Daemon: performs the scheduling functions of LSF and sends job scheduling decisions to MBD for dispatch. Runs on the LSF master server host |
| **sbatchd** | Slave Batch Daemon (SBD): accepts job execution requests from MBD, and monitors the progress of jobs. Controls job execution, enforces batch policies, reports job status to MBD, and starts MBD. |
| **pim**     | Process Information Manager (PIM): monitors resources that are used by submitted jobs while they are running. PIM is used to enforce resource limits and load thresholds, and for fairshare scheduling |
| **res**     | Remote Execution Server (RES): accepts remote execution requests from all load-sharing applications and handles I/O on the remote host for load sharing processes. |

------



## 用户命令

### 查看集群信息的命令

------

| 命令        | 描述                                                         |
| :---------- | :----------------------------------------------------------- |
| **bhosts**  | Displays hosts and their static and dynamic resources        |
| **blimits** | Displays information about resource allocation limits of running jobs |
| **bparams** | Displays information about tunable batch system parameters   |
| **bqueues** | Displays information about batch queues                      |
| **busers**  | Displays information about users and user groups             |
| **lshosts** | Displays hosts and their static resource information         |
| **lsid**    | Displays the current LSF version number, cluster name, and master host name |
| **lsinfo**  | Displays load-sharing configuration information              |
| **lsload**  | Displays dynamic load indexes for hosts                      |

------



### 监测作业与任务的命令

------

| Command     | Description                                                  |
| :---------- | :----------------------------------------------------------- |
| **bacct**   | Reports accounting statistics on completed LSF jobs          |
| **bapp**    | Displays information about jobs that are attached to application profiles |
| **bhist**   | Displays historical information about jobs                   |
| **bjobs**   | Displays information about jobs                              |
| **bpeek**   | Displays stdout and stderr of unfinished jobs                |
| **bsla**    | Displays information about service class configuration for goal-oriented service-level agreement scheduling |
| **bstatus** | Reads or sets external job status messages and data files    |

------



### 提交与控制作业的命令

------

| Command      | Description                                                  |
| :----------- | :----------------------------------------------------------- |
| **bbot**     | Moves a pending job relative to the last job in the queue    |
| **bchkpnt**  | Checkpoints a checkpointable job                             |
| **bkill**    | Sends a signal to a job                                      |
| **bmig**     | Migrates a checkpointable or rerunnable job                  |
| **bmod**     | Modifies job submission options                              |
| **brequeue** | Kills and requeues a job                                     |
| **bresize**  | Releases slots and cancels pending job resize allocation requests |
| **brestart** | Restarts a checkpointed job                                  |
| **bresume**  | Resumes a suspended job                                      |
| **bstop**    | Suspends a job                                               |
| **bsub**     | Submits a job                                                |
| **bswitch**  | Moves unfinished jobs from one queue to another              |
| **btop**     | Moves a pending job relative to the first job in the queue   |

------



## bsub 命令

 **bsub** [options] command[arguments] 命令中的部分选项

------

| 选项                                                         | 描述                                                         |
| :----------------------------------------------------------- | :----------------------------------------------------------- |
| **-ar**                                                      | Specifies the job is autoresizable                           |
| **-H**                                                       | Holds the job in the PSUSP state at submission               |
| **-I\|-Ip\|-Is**                                             | Submits a batch interactive job. **-Ip** creates a pseudo-terminal. **-Is** creates a pseudo-terminal in shell mode. |
| **-K**                                                       | Submits a job and waits for the job to finish                |
| **-r**                                                       | Makes a job rerunnable                                       |
| **-x**                                                       | Exclusive execution                                          |
| **-app** application_profile_name                            | Submits the job to the specified application profile         |
| **-b** begin_time                                            | Dispatches the job on or after the specified date and time in the form [[month:]day:]:minute |
| **-C** core_limit                                            | Sets a per-process (soft) core file size limit (KB) for all the processes that belong to this job |
| **-c** cpu_time[/host_name \| /host_model]                   | Limits the total CPU time the job can use. CPU time is in the form [hour:]minutes |
| **-cwd** "current_working_directory"                         | Specifies the current working directory for the job          |
| **-D** data_limit                                            | Sets the per-process (soft) data segment size limit (KB) for each process that belongs to the job |
| **-E** "pre_exec_command [arguments]"                        | Runs the specified pre-exec command on the execution host before the job runs |
| **-Ep** "post_exec_command [arguments]"                      | Runs the specified post-exec command on the execution host after the job finishes |
| **-e** error_file                                            | Appends the standard error output to a file                  |
| **-eo** error_file                                           | Overwrites the standard error output of the job to the specified file |
| **-F** file_limit                                            | Sets per-process (soft) file size limit (KB) for each process that belongs to the job |
| **-f** "local_file op[remote_file]" ...                      | Copies a file between the local (submission) host and remote (execution) host.op is one of >, <, <<, ><, <> |
| **-i** input_file \| **-is** input_file                      | Gets the standard input for the job from specified file      |
| **-J** "job_name[index_list]%job_slot_limit"                 | Assigns the specified name to the job. Job array index_list has the form start[-end[:step]], and %job_slot_limit is the maximum number of jobs that can run at the same time. |
| **-k** "chkpnt_dir \[chkpnt_period][method=method_name]"     | Makes a job checkpointable and specifies the checkpoint directory, period in minutes, and method |
| **-M** mem_limit                                             | Sets the per-process (soft) memory limit (KB)                |
| **-m** "host_name \[@cluster_name][[!] \| +[pref_level]] \| host_group[[!] \|+[pref_level]] \| compute_unit[[!] \|+[pref_level]]..." | Runs job on one of the specified hosts. Plus (+) after the names of a host or group indicates a preference. Optionally, a positive integer indicates a preference level. Higher numbers indicate a greater preference. |
| **-n** min_proc[,max_proc]                                   | Specifies the minimum and maximum numbers of processors that are required for a parallel job |
| **-o** output_file                                           | Appends the standard output to a file                        |
| **-oo** output_file                                          | Overwrites the standard output of the job to the specified file |
| **-p** process_limit                                         | Limit the number of processes for the whole job              |
| **-q** "queue_name ..."                                      | Submits job to one of the specified queues                   |
| **-R** "res_req" [-R "res_req" ...]                          | Specifies host resource requirements                         |
| **-S** stack_limit                                           | Sets a per-process (soft) stack segment size limit (KB) for each process that belongs to the job |
| **-sla** service_class_name                                  | Specifies the service class where the job is to run          |
| **-T** thread_limit                                          | Sets the limit of the number of concurrent threads for the whole job |
| **-t** term_time                                             | Specifies the job termination deadline in the form [[month:]day:]hour:minute |
| **-v** swap_limit                                            | Sets the total process virtual memory limit (KB) for the whole job |
| **-W** run_time[/host_name \| /host_model]                   | Sets the runtime limit of the job in the form [hour:]minute  |
| **-h**                                                       | Prints command usage to stderr and exits                     |
| **-V**                                                       | Prints LSF release version to stderr and exits               |

------