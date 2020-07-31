# 管理用户、节点与队列

通过 cshrc.lsf 和 profile.lsf 使集群对用户可用。 从集群中添加或删除主机和队列。

##### 使用 cshrc.lsf 和 profile.lsf 为用户提供集群

确保所有 LSF 用户在其自己的 .cshrc 或 .profile 文件末尾都包含 cshrc.lsf 或 profile.lsf 文件，或者在使用 LSF 之前运行这两个文件之一。

##### 将主机添加到集群中

使用 LSF 安装脚本 **lsfinstall** 将新主机和主机类型添加到您的集群中。

##### 从集群中删除主机

从 LSF 中删除主机，包括关闭主机以防止主机上运行任何其他作业，以及从 lsf.cluster.cluster_name 文件和其他配置文件中删除对该主机的引用。

##### 添加队列

编辑 lsb.queues 文件以添加新的队列定义。 添加队列不会影响挂起或正在运行的作业。

##### 删除队列

编辑 lsb.queues 以除去队列定义。