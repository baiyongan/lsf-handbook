# 移除队列

编辑 lsb.queues 以移除队列定义。

## 开始之前

##### 重要

删除队列之前，请确保该队列中没有正在运行的作业。

使用 **bqueues** 命令，可查看现有队列列表以及在这些队列中运行的作业。如果作业在要删除的队列中，则必须将挂起的，和正在运行的作业切换到另一个队列，然后删除该队列。 如果删除其中有待处理作业的队列，则作业将暂时移至 lost_and_found 队列。 作业状态不变。 正在运行的作业将继续，原始队列中暂挂的作业将在 lost_and_found 队列中暂挂。 作业保持待处理状态，直到用户或队列管理员使用 **bswitch** 命令，将作业切换为常规队列为止。 其他队列中的作业不受影响。

## 步骤

1. 以主要管理员身份登录到集群中的任何主机上。

2. 关闭队列以防止提交任何新作业。

   ```shell
   badmin qclose night
   Queue night is closed
   ```

3. 将所有暂挂和正在运行的作业切换到另一个队列。

   例如，**bswitch -q night idle 0** 命令从 night 队列到 idle 队列中选择作业。 作业ID号 0 切换所有作业。

   ```
   bjobs -u all -q night
   JOBID USER  STAT  QUEUE FROM_HOST   EXEC_HOST   JOB_NAME   SUBMIT_TIME 
   5308  user5  RUN   night    hostA     hostD         job5  Nov 21 18:16 
   5310  user5 PEND   night    hostA     hostC        job10  Nov 21 18:17
    
   bswitch -q night idle 0
   Job <5308> is switched to queue <idle> 
   Job <5310> is switched to queue <idle>
   ```

4. 编辑 LSB_CONFDIR/cluster_name/configdir/lsb.queues 文件，然后删除或注释掉要删除的队列的定义。

5. 将更改保存到 lsb.queues 文件。

6. 运行 **badmin reconfig** 命令以重新配置集群。

   ```shell
   % badmin reconfig
   Checking configuration files ...
   No errors found.
   Do you want to reconfigure? [y/n] y
   Reconfiguration initiated
   ```

   **badmin reconfig** 命令检查配置错误。 如果未找到不可恢复的错误，则要求您确认重新配置。 如果发现不可恢复的错误，则重新配置退出。

## 结论

如果遇到错误，请参见 [Troubleshooting LSF problems](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_admin/chap_troubleshooting_lsf.html?view=kc#v3523448) 以获取有关一些常见配置错误的帮助。

- 有关 [lsb.queues ](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_config_ref/lsb.queues.5.html?view=kc)文件的更多信息，请参见 [Configuration Reference](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_welcome/lsf_kc_config_ref.html?view=kc).
- 有关 [**badmin reconfig**](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_command_ref/badmin.8.html?view=kc) 命令的更多信息，请参见 [Command Reference](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_welcome/lsf_kc_cmd_ref.html?view=kc).