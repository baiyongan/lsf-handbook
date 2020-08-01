# 从集群中删除主机

从 LSF 中删除主机，包括关闭主机以防止主机上运行任何其他作业，以及从 lsf.cluster.cluster_name 文件和其他配置文件中删除对该主机的引用。

## 任务说明

##### 注意

切勿从 LSF 中删除 master 主控节点。 如果要更改当前的默认主节点，请更改 lsf.cluster.cluster_name 文件以分配其他默认主控主机。 然后删除以前是主控节点的主机。

## 步骤

1. 以 root 用户身份登录到 LSF 主机。

2. 运行 **badmin hclose** 关闭主机。

     关闭主机可防止将作业分派到主机，并允许正在运行的作业完成。

3. 手动停止所有正在运行的守护程序。

4. 在 LSF_CONFDIR/lsf.cluster.cluster_name 文件的 “Host” 部分中删除对主机的所有引用。

5. 从以下配置文件中，删除对主机的任何其他引用（如果适用）：

   - LSF_CONFDIR/lsf.shared
   - LSB_CONFDIR/cluster_name/configdir/lsb.hosts
   - LSB_CONFDIR/cluster_name/configdir/lsb.queues
   - LSB_CONFDIR/cluster_name/configdir/lsb.resources

6. 注销要删除的主机，然后以 root 或 LSF 主管理员身份，登录到集群中的任何其他主机。

7. 运行 **lsadmin reconfig** 命令以重新配置 LIM。

   ```shell
   % lsadmin reconfig
   Checking configuration files ...
   No errors found.
   Do you really want to restart LIMs on all hosts? [y/n] y
   Restart LIM on <hosta> ...... done
   Restart LIM on <hostc> ...... done
   ```

   **lsadmin reconfig** 命令检查配置错误。

   如果未找到错误，将要求您确认要在所有主机上重新启动 **lim**，并且已重新配置 **lim**。 如果发现不可恢复的错误，则重新配置退出。

8. 运行 **badmin mbdrestart** 命令来重启 **mbatchd**.

   ```shell
   % badmin reconfig
   Checking configuration files ...
   No errors found.
   Do you want to reconfigure? [y/n] y
   Reconfiguration initiated
   ```

   **badmin mbdrestart** 命令检查配置错误。

   如果未找到不可恢复的错误，则要求您确认重新配置。 如果发现不可恢复的错误，则重新配置退出。

9. 如果您将 LSF 守护程序，配置为在系统启动时自动启动，请从主机的系统启动文件中删除 LSF 部分。

   有关自动 LSF 守护程序启动的更多信息, 请参阅 [Setting up automatic LSF startup](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_admin_foundations/auto_startup.html?view=kc#auto_startup76)

10. 如果主机的任何用户使用 **lstcsh** shell 作为其登录 shell，请将其登录 shell 更改为 tcsh 或 csh。 从 /etc/shells 文件中删除 **lstcsh**。

## 结论

- 使用动态主机配置将主机从集群中删除，而无需手动更改 LSF 配置。 有关动态删除主机的更多信息, 请参阅 [IBM Platform LSF Cluster Management and Operations](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_welcome/lsf_kc_cluster_ops.html?view=kc).
- 如果遇到错误，请参阅 [Troubleshooting LSF problems](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_admin/chap_troubleshooting_lsf.html) 帮助解决一些常见的配置错误。