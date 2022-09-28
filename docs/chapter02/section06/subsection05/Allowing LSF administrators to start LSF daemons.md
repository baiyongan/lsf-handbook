# 允许 LSF 管理员启动 LSF 守护程序

要允许 LSF 管理员启动和停止 LSF 守护程序，请配置 /etc/lsf.sudoers 文件。 如果 lsf.sudoers 文件不存在，则只有 root 可以启动和停止 LSF 守护程序。

## 任务说明

使用 lsf.sudoers 文件要求您启用 setuid bit。 因为这允许 LSF 管理命令以 root 特权运行，所以如果您不希望这些命令以 root 特权运行，请不要继续。

## 步骤

1. 以 root 用户身份登录到每个 LSF 服务器主机。

   从 LSF 主节点开始，然后在所有 LSF 主机上重复这些步骤。

2. 在每个 LSF 主机上创建一个 /etc/lsf.sudoers 文件，并指定 **LSF_STARTUP_USERS** 和 **LSF_STARTUP_PATH ** 参数。

   ```shell
   LSF_STARTUP_USERS="lsfadmin user1"
   LSF_STARTUP_PATH=/usr/share/lsf/cluster1/10.1/sparc-sol2/etc
   ```

   **LSF_STARTUP_PATH** 通常是 LSF_SERVERDIR 目录的路径，其中有 LSF 服务器二进制文件（**lim**，**res**，**sbatchd**，**mbatchd**，**mbschd** ，等等），如 LSF_CONFDIR/lsf.conf 文件中所定义。

   lsf.sudoers 文件必须具有文件许可权模式 -rw -------（600），并且只能由 root 读取和写入：

   ```shell
   # ls -la /etc/lsf.sudoers
   -rw-------   1 root     lsf           95 Nov 22 13:57 lsf.sudoers
   ```

3. 运行 **lsfrestart** 命令以重新启动集群：

   ```shell
   # lsfrestart
   ```