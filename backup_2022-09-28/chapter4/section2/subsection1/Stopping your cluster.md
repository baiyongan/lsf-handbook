# 停止集群

使用 **lsadmin** 和 **badmin** 命令停止 LSF 守护程序。

## 步骤

- 以 root 用户身份登录到每个 LSF 服务器主机。

  如果您以 非root 用户身份安装了单用户集群，请以 LSF 主管理员身份登录。

- 使用以下命令停止 LSF 集群：:


```shell
# badmin hshutdown all
# lsadmin resshutdown all
# lsadmin limshutdown all
```