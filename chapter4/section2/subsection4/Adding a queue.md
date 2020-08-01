# 添加队列

编辑 lsb.queues 文件以添加新的队列定义。 添加队列不会影响挂起或正在运行的作业。

## 步骤

1. 以管理员身份，登录到集群中的任何主机上。

2. 编辑 LSB_CONFDIR/cluster_name/configdir/lsb.queues 文件以添加新的队列定义。

   您可以从该文件复制另一个队列定义作为起点。 切记更改已复制队列的 **QUEUE_NAME** 参数。

3. 将更改保存到 lsb.queues 文件。

4. 准备好配置文件后，运行 **badmin ckconfig** 命令以检查新的队列定义。

   如果报告任何错误，请解决此问题，然后再次检查配置。

5. 运行 **badmin reconfig** 命令以重新配置集群。

   ```shell
   % badmin reconfig
   Checking configuration files ...
   No errors found.
   Do you want to reconfigure? [y/n] y
   Reconfiguration initiated
   ```

   **badmin reconfig** 命令还检查配置错误。 如果未找到不可恢复的错误，则要求您确认重新配置。 如果发现不可恢复的错误，则重新配置退出。

## 结论

如果遇到错误，请参阅 [Troubleshooting LSF problems](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_admin/chap_troubleshooting_lsf.html?view=kc#v3523448) 以获取有关一些常见配置错误的帮助。

- 有关 [lsb.queues](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_config_ref/lsb.queues.5.html?view=kc) 文件的更多信息，请参见 [Configuration Reference](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_welcome/lsf_kc_config_ref.html?view=kc)。
- 有关 [**badmin reconfig**](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_command_ref/badmin.8.html?view=kc) 命令的更多信息, 请参见 [Command Reference](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_welcome/lsf_kc_cmd_ref.html?view=kc).

## 示例

```shell
Begin Queue 
QUEUE_NAME = normal 
PRIORITY = 30 
STACKLIMIT= 2048 
DESCRIPTION = For normal low priority jobs, running only if hosts are lightly loaded. 
QJOB_LIMIT = 60     # job limit of the queue 
PJOB_LIMIT = 2     # job limit per processor 
ut = 0.2 
io = 50/240 
USERS = all 
HOSTS = all  
NICE = 20 
End Queue
```