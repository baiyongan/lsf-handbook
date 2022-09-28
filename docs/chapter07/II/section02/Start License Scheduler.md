# 启动许可证计划程序

## 任务说明

您可以将 LSF 配置为在 License Scheduler 主机以及可以在网络故障的情况下接管许可证分发的候选 License Scheduler 主机上启动 License Scheduler 守护程序（**bld**）。 LSF LIM 守护程序会自动启动 bld。

## 步骤

1. 以 主LSF 管理员身份登录。

2. 设置 LSF 环境:

   - 对于 **csh** 或 **tcsh**:

   % source LSF_TOP/conf/cshrc.lsf

   - 对于 **sh**, **ksh**, 或 **bash**:

     `$ `. LSF_TOP/conf/profile.lsf

3. 在 LSF_CONFDIR/lsf.conf 中，为 LSF_LIC_SCHED_HOSTS 参数指定以空格分隔的主机列表：LSF_LIC_SCHED_HOSTS =“ hostname_1 hostname_2 ... hostname_n”

   其中:

   hostname_1，hostname_2 和 hostname_n 是 LSF LIM 守护程序在其上启动许可证调度守护程序的主机。 主机名的顺序将被忽略。

   ##### Note

   将 **LSF_LIC_SCHED_HOSTS** 参数设置为与 lsf.licensescheduler **HOSTS** 参数中使用的候选主机相同的列表。 LSF_LIC_SCHED_HOSTS 参数未在任何其他函数中使用。

4. 运行 **lsadmin reconfig** 以重新配置 LIM。

5. 使用 **ps -ef** 确保候选主机上正在运行 **bld**。

6. 运行 **badmin mbdrestart** 来重启 **mbatchd**.

7. 如果您在服务域中指定了 **LIC_COLLECTOR** 名称，请手动启动每个许可证收集器：

   blcollect -m "host_list" -p lic_scheduler_port -c lic_collector_name

   其中:

   - host_list

     指定以空格分隔的许可证调度程序候选主机列表，许可证信息将发送到该列表。 使用标准主机名。

   - lic_scheduler_port

     对应于 lsf.licensescheduler 中设置的 License Scheduler 侦听端口。

   - lic_collector_name

     指定在 lsf.licensescheduler 的 “service domain” 部分中为 LIC_COLLECTOR 设置的许可证收集器的名称。

     例如:

     blcollect -m "hostD.designcenter_b.com hostA.designcenter_a.com" -p 9581 -c CenterB

     在您的 LSF WORKDIR 中创建了一个名为 collectors/Center 的文件。

     ##### Note

     如果您未在许可证调度程序的 ”service domain“ 中指定许可证收集器名称，则 主**bld** 节点将启动默认的**blcollect**。