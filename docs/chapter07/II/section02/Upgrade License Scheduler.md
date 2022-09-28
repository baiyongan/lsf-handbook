# 更新 License Scheduler

## 开始之前

必须先安装 License Scheduler，然后才能进行升级。 您必须是集群管理员。

## 任务说明

您可以升级到 License Scheduler 的新版本，而无需卸载和重新安装。

## 步骤

1. 下载 License Scheduler 新发布版本的 tar 文件。

2. 停用所有队列。

    取消激活所有队列会使所有正在运行的作业挂起，并阻止新作业被调度。

   badmin qinact all

3. 如果已安装 IBM Spectrum LSF Application Center，请关闭它。

   pmcadmin stop

4. 根据您站点上的过程备份现有的 **LSF_CONFDIR**，**LSB_CONFDIR** 和 **LSB_SHAREDIR**。

5. 可选的。 要在 LSF License Scheduler 中使用快速调度项目模式，请将 LSF 升级到高于 9.1.1 的版本。

   完成升级后，重新启动 LSF。

6. 使用安装脚本来升级 LSF License Scheduler。

   1. 在旧的 LSF 集群中 source cshrc.lsf 或 profile.lsf。
   2. 导航到 tar 文件的位置并解压缩。
   3. 运行安装脚本。

7. 如果要安装 License Scheduler Standard Edition，请将 License Scheduler 授权文件（ls.entitlement）复制到 $LSF_ENVDIR 目录。

   如果您没有在启动 License Scheduler 之前将授权文件复制到 $LSF_ENVDIR，则 License Scheduler 将以 Basic Edition 运行。

8. 启动许可证计划程序。

   1. Source cshrc.lsf 或 profile.lsf。

   2. 运行 bladmin reconfig。

   3. 运行 ps -ef 以确保候选主机上正在运行 **bld**。

   4. 运行 badmin mbdrestart.

   5. 激活队列。

      badmin qact all

9. 如果已安装 IBM Spectrum LSF Application Center，请重新启动它。

   pmcadmin start

   ##### 提示

   IBM Spectrum LSF Application Center 显示项目模式和集群模式的许可计划程序作业负载。