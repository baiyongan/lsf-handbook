# 重要的文件目录与配置文件

LSF 配置，通过几个配置文件进行管理，您可以使用这些文件来修改集群的行为。

## 四个重要的 LSF 配置文件

以下是您最常使用的四个最重要的文件：

- LSF_CONFDIR/lsf.conf
- LSF_CONFDIR/lsf.cluster.cluster_name
- LSF_CONFDIR/lsf.shared
- LSB_CONFDIR/cluster_name/configdir/lsb.queues

这些文件，是在产品安装期间根据您在 install.config 文件中指定的选项创建的。 安装后，您可以更改这些文件中的配置参数，以适合您的站点的需求。

- ##### 谁拥有这些文件

  除了由 root 拥有的 LSF_CONFDIR/lsf.conf 外，所有这些文件均由 LSF 主管理员拥有，并且所有集群用户均可读取。

- ##### lsf.conf

  LSF 中最重要的文件。 它包含配置目录，日志目录，库和其他全局配置信息的路径。 lsf.conf 文件的位置由LSF_ENVDIR 变量定义。 如果 LSF 找不到此文件，则它将无法正常启动。默认情况下，LSF会检查 **LSF_ENVDIR** 参数定义的目录中的 lsf.conf 文件的位置。 如果 lsf.conf 文件不在 **LSF_ENVDIR** 中，则 LSF 在 /etc 目录中查找它。

- ##### lsf.cluster.cluster_name

  定义集群中所有主机的主机名，型号和类型。 它还定义了 LSF 管理员的用户名，以及一个集群的不同共享资源的位置。

- ##### lsf.shared

  该文件就像一个字典，定义了集群使用的所有关键字。 您可以添加自己的关键字，来指定资源或主机类型的名称。

- ##### lsb.queues

  为一个集群定义作业负载队列及其参数。

## LSF 目录

以下目录归 LSF 主管理员所有，并且所有集群用户均可读取：

------

| 目录             | 描述                                     | 示例                                  |
| :--------------- | :--------------------------------------- | :------------------------------------ |
| **LSF_CONFDIR**  | LSF 配置目录                             | /usr/share/lsf/cluster1/conf/         |
| **LSB_CONFDIR**  | 批处理系统配置目录                       | /usr/share/lsf/cluster1/conf/lsbatch/ |
| **LSB_SHAREDIR** | 作业历史目录                             | /usr/share/lsf/cluster1/work/         |
| **LSF_LOGDIR**   | 服务器守护程序错误日志，每个守护程序一个 | /usr/share/lsf/cluster1/log/          |

------

以下目录归 root 拥有，并且所有集群用户均可读取：

------

| 目录               | 描述                                                         | 示例                                          |
| :----------------- | :----------------------------------------------------------- | :-------------------------------------------- |
| **LSF_BINDIR**     | LSF 用户命令，由相同类型的所有主机共享                       | /usr/share/lsf/cluster1/10.1/sparc-sol10/bin/ |
| **LSF_INCLUDEDIR** | 头文件 lsf/lsf.h 和 lsf/lsbatch.h                            | /usr/share/lsf/cluster1/10.1/include/         |
| **LSF_LIBDIR**     | LSF 库，由相同类型的所有主机共享                             | /usr/share/lsf/cluster1/10.1/sparc-sol10/lib/ |
| **LSF_MANDIR**     | LSF manual 手册                                              | /usr/share/lsf/cluster1/10.1/man/             |
| **LSF_MISC**       | 示例和其他杂项文件                                           | /usr/share/lsf/cluster1/10.1/misc/            |
| **LSF_SERVERDIR**  | 服务器守护程序二进制文件，脚本和其他实用程序，由相同类型的所有主机共享 | /usr/share/lsf/cluster1/10.1/sparc-sol10/etc/ |
| **LSF_TOP**        | 顶级安装目录                                                 | /usr/share/lsf/cluster1/                      |

------

可以在 LSF_CONFDIR/lsf.conf 文件中指定其他配置目录。

## LSF 集群配置文件

以下文件归 LSF 主管理员所有，并且所有集群用户均可读取：

------

| 文件描述                                                     | 示例                                                         |
| :----------------------------------------------------------- | :----------------------------------------------------------- |
| 全局配置文件，描述集群的配置和操作                           | /usr/share/lsf/cluster1/conf/ego/cluster1/kernel/ego.conf  /usr/share/lsf/cluster1/conf/lsf.conf |
| 所有集群共享的关键字定义文件。 定义集群名称，主机类型，主机模型和特定于站点的资源 | /usr/share/lsf/cluster1/conf/lsf.shared                      |
| 群集配置文件，用于定义主机，管理员和站点定义的共享资源的位置 | /usr/share/lsf/cluster1/conf/lsf.cluster.cluster1            |
| 任务名称及其默认资源要求的映射文件                           | /usr/share/lsf/cluster1/conf/lsf.task /usr/share/lsf/cluster1/conf/lsf.task.cluster1 |

------

## LSF 批处理作业负载系统配置文件

以下文件归 LSF 主管理员所有，并且所有集群用户均可读取：

------

| 文件描述                                                     | 示例                                                         |
| :----------------------------------------------------------- | :----------------------------------------------------------- |
| 服务器主机及其属性，例如计划负载阈值，调度窗口和作业槽位限制。 如果在此文件中未定义任何主机，则假定LSF_CONFDIR/lsf.cluster.cluster_name中列出的所有 LSF 服务器主机都是 LSF 批处理服务器主机。 | /usr/share/lsf/cluster1/conf/lsbatch/cluster1/configdir/lsb.hosts |
| LSF 调度程序和资源代理插件模块。 如果未配置任何调度程序，或资源代理模块，则 LSF 使用默认调度程序插件模块schmod_default。 | /usr/share/lsf/cluster1/conf/lsbatch/cluster1/configdir/lsb.modules |
| LSF 批处理系统参数文件                                       | /usr/share/lsf/cluster1/conf/lsbatch/cluster1/configdir/lsb.params |
| 作业队列定义                                                 | /usr/share/lsf/cluster1/conf/lsbatch/cluster1/configdir/lsb.queues |
| 资源分配限制，导出和资源使用限制。                           | /usr/share/lsf/cluster1/conf/lsbatch/cluster1/configdir/lsb.resources |
| LSF 用户组，用户和用户组的分层公平共享，以及用户和用户组的作业位置限制。 还用于为 LSF 多集群功能配置帐户映射。 | /usr/share/lsf/cluster1/conf/lsbatch/cluster1/configdir/lsb.users |
| 应用程序概要文件，其中包含相同类型作业的通用参数，包括应用程序的执行要求，所需的资源以及运行和管理方式。 该文件是可选的。 使用 lsb.params 文件中的**DEFAULT_APPLICATION** 参数，为所有作业指定默认的应用程序配置文件。 LSF 不会自动分配默认的应用程序配置文件。 | /usr/share/lsf/cluster1/conf/lsbatch/cluster1/configdir/lsb.applicatons |

------

## LSF 批处理日志文件

------

| 文件描述       | 示例                                                     |
| :------------- | :------------------------------------------------------- |
| 批处理事件日志 | /usr/share/lsf/cluster1/work/ cluster1/logdir/lsb.events |
| 批处理记帐日志 | /usr/share/lsf/cluster1/work/ cluster1/logdir/lsb.acct   |

------

## 守护程序日志文件

LSF 服务器守护程序日志文件，存储在 LSF_CONFDIR/lsf.conf 中由 LSF_LOGDIR 指定的目录中。

------

| 文件                                  | 示例                                           |
| :------------------------------------ | :--------------------------------------------- |
| Load information manager (**lim**)    | /usr/share/lsf/cluster1/log/lim.log.hosta      |
| Remote execution server (**res**)     | /usr/share/lsf/cluster1/log/res.log.hosta      |
| Master batch daemon (**mbatchd**)     | /usr/share/lsf/cluster1/log/ mbatchd.log.hosta |
| Master scheduler daemon (**mbschd**)  | /usr/share/lsf/cluster1/log/mbschd.log.hosta   |
| Slave batch daemon (**sbatchd**)      | /usr/share/lsf/cluster1/log/sbatchd.log.hosta  |
| Process information manager (**pim**) | /usr/share/lsf/cluster1/log/ pim.log.hosta     |

------

##### **注意：** 谁拥有，谁应该写给LSF_LOGDIR

确保 LSF 主管理员拥有 LSF 日志目录（**LSF_LOGDIR**参数），并且 root 可以写入该目录。 如果 LSF 服务器无法写入 **LSF_LOGDIR** 参数，则在 /tmp 中创建错误日志。.

