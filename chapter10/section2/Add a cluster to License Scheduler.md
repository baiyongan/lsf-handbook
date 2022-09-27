# 向 License Scheduler 中添加集群

## 开始之前

必须切换为 License Scheduler 管理员

## 任务说明

您可以将新集群，添加到现有的许可证计划程序实施中。

添加 LSF Advanced Edition 集群时，只需将提交集群添加到 LSF License Scheduler，因为提交集群会将 LSF License Scheduler 作业转发到其执行集群。

## 步骤

1. 下载许可证计划程序包。

   ##### 提示

   获取与现有成员集群中使用的主 **bld** 二进制文件和其他体系结构相同的版本。

2. 在新集群上安装许可计划程序软件包。

3. 使用另一个具有相同 **bld** 主服务器的集群的 $LSF_ENVDIR 中的现有 lsf.licensescheduler。

4. 将新的集群名称添加到 lsf.licensescheduler的 “Cluster” 部分。

5. 添加或修改 lsf.licensescheduler 中定义的许可证分发策略。

6. 维护一个中央 lsf.licensescheduler 文件，并让所有集群访问该文件。

   ##### 注意

   每个集群中的 lsf.licensescheduler 文件必须相同。

   您可以使用以下两种方法之一来完成此任务：

   - 创建从每个集群的 $LSF_ENVDIR 到中央 lsf.licensescheduler 文件的符号链接。
   - 使用基于 CRON 的同步脚本将从中央 lsf.licensescheduler 文件所做的更改，同步到所有集群中相应的lsf.licensescheduler 文件。

7. 检查 lsf.licensescheduler 文件中来自 PORT 的通信，是否存在防火墙或网络问题。

8. 在运行 **bld** 的所有主机上运行 bladmin reconfig。

9. 在新添加的集群上，运行 lsadmin limrestart，然后运行 badmin mbdrestart。