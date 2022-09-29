# 重新配置集群

更改任何配置文件后，请使用 **lsadmin** 和 **badmin** 重新配置群集

## 步骤

- 以 root 用户身份登录到每个 LSF 服务器主机。

  如果您以 非root 用户身份安装了单用户集群，请以 LSF 主管理员身份登录。

- 使用以下命令重新配置 LSF 集群：

```shell
# 重新加载修改的 LSF 配置文件并重新启动 lim：
# lsadmin reconfig
# 重新加载修改后的 LSF 批处理配置文件：
# badmin reconfig
# 重新加载修改后的 LSF 批处理配置文件，然后重新启动 mbatchd：:
# badmin mbdrestart
```

此命令还会读取 LSF_LOGDIR/lsb.events文件，因此如果正在运行许多作业，则可能需要一些时间才能完成。

