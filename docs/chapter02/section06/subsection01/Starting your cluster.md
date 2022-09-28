# 启动集群

使用 **lsadmin** 和 **badmin** 命令启动 LSF 守护程序。

## 步骤

- 以 root 用户身份登录到每个 LSF 服务器主机。

   如果您以 非root 用户身份安装了单用户集群，请以 LSF 主管理员身份登录。

   从 LSF 主节点开始，然后在所有 LSF 主机上重复这些步骤。

- 使用以下命令启动LSF集群：

   ```shell
   # lsadmin limstartup
   # lsadmin resstartup
   # badmin hstartup
   ```

   在使用任何 LSF 命令之前，请等待几分钟，让 **lim** 守护程序所有主机执行以下操作：

   - 互相联系
   - 选择主节点
   - 交换初始化信息

