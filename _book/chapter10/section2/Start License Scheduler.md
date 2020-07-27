# 启动许可证计划程序

## 关于此任务

You can configure LSF to start the License Scheduler daemon (**bld**) on the License Scheduler host as well as on candidate License Scheduler hosts that can take over license distribution in the case of a network failure. The LSF LIM daemon starts **bld** automatically.

## 步骤

1. Log on as the primary LSF administrator.

2. Set your LSF environment:

   - For **csh** or **tcsh**:

   % source LSF_TOP/conf/cshrc.lsf

   - For **sh**, **ksh**, or **bash**:

     `$ `. LSF_TOP/conf/profile.lsf

3. In LSF_CONFDIR/lsf.conf, specify a space-separated list of hosts for the **LSF_LIC_SCHED_HOSTS** parameters:

   LSF_LIC_SCHED_HOSTS="hostname_1 hostname_2 ... hostname_n"

   Where:

   hostname_1, hostname_2, hostname_n are hosts on which the LSF LIM daemon starts the License Scheduler daemon. The order of the host names is ignored.

   ##### Note

   Set the **LSF_LIC_SCHED_HOSTS** parameter to the same list of candidate hosts you used in the lsf.licensescheduler **HOSTS** parameter. The LSF_LIC_SCHED_HOSTS parameter is not used in any other function.

4. Run **lsadmin reconfig** to reconfigure the LIM.

5. Use **ps -ef** to make sure that **bld** is running on the candidate hosts.

6. Run **badmin mbdrestart** to restart **mbatchd**.

7. If you specified a **LIC_COLLECTOR** name in your service domains, start each license collector manually:

   blcollect -m "host_list" -p lic_scheduler_port -c lic_collector_name

   Where:

   - host_list

     Specifies a space-separated list of License Scheduler candidate hosts to which license information is sent. Use fully qualified host names.

   - lic_scheduler_port

     Corresponds to the License Scheduler listening port, which is set in lsf.licensescheduler.

   - lic_collector_name

     Specifies the name of the license collector you set for LIC_COLLECTOR in the service domain section of lsf.licensescheduler.

     For example:

     blcollect -m "hostD.designcenter_b.com hostA.designcenter_a.com" -p 9581 -c CenterB

     A file named collectors/CenterB is created in your LSF_WORKDIR.

     ##### Note

     If you do not specify a license collector name in a License Scheduler service domain, the master **bld** host starts a default **blcollect**.