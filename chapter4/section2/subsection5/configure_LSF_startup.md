# 配置 LSF 启动

使用 lsf.sudoers 文件，以便 LSF 管理员可以启动和停止 LSF 守护程序。 将 LSF 设置为自动启动。

##### 允许 LSF 管理员使用 lsf.sudoers 启动 LSF 守护程序

要允许 LSF 管理员启动和停止 LSF 守护程序，请配置 /etc/lsf.sudoers 文件。 如果 lsf.sudoers 文件不存在，则只有 root 可以启动和停止 LSF 守护程序。

##### 设置 LSF 自动启动

将 LSF 守护程序，配置为在集群中的每个 LSF 服务器主机上自动启动。