# 检查集群配置

**lsadmin** 命令控制 LSF 集群的操作，并管理 LSF 守护程序 **lim** 和 **res**。

使用 **lsadmin ckconfig ** 命令检查 LSF 配置文件。 -v 选项显示有关 LSF 配置的详细信息：

以下输出中显示的消息是 **lsadmin ckconfig -v** 的典型消息。其他消息可能表明您的 LSF 配置有问题。

```shell
% lsadmin ckconfig -v
Checking configuration files ...

EGO 3.6.0 build 800000, Jul 25 2017
Copyright International Business Machines Corp. 1992, 2016.
US Government Users Restricted Rights - Use, duplication or disclosure restricted by GSA ADP Schedule Contract with IBM Corp.

  binary type: linux2.6-glibc2.3-x86_64
Reading configuration from /opt/lsf/conf/lsf.conf
Aug  3 13:45:27 2017 20884 6 3.6.0 Lim starting...
Aug  3 13:45:27 2017 20884 6 3.6.0 LIM is running in advanced workload execution mode.
Aug  3 13:45:27 2017 20884 6 3.6.0 Master LIM is not running in EGO_DISABLE_UNRESOLVABLE_HOST mode.
Aug  3 13:45:27 2017 20884 5 3.6.0 /opt/lsf/10.1/linux2.6-glibc2.3-x86_64/etc/lim -C
Aug  3 13:45:27 2017 20884 7 3.6.0 Could not construct product entitlement version array
Aug  3 13:45:27 2017 20884 Last message repeated 1 time(s).
Aug  3 13:45:27 2017 20884 6 3.6.0 initEntitlement: EGO_AUDIT_MAX_SIZE was not set. Default value <100> will be used.
Aug  3 13:45:27 2017 20884 6 3.6.0 initEntitlement: EGO_AUDIT_MAX_ROTATE was not set. Default value <20> will be used.
Aug  3 13:45:27 2017 20884 6 3.6.0 LIM is running as IBM Spectrum LSF Standard Edition.
Aug  3 13:45:27 2017 20884 6 3.6.0 reCheckClass: numhosts 1 so reset exchIntvl to 15.00
Aug  3 13:45:27 2017 20884 6 3.6.0 Checking Done.
---------------------------------------------------------
No errors found.
```

参阅 [Troubleshooting LSF problems](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_admin/chap_troubleshooting_lsf.html?view=kc#v3523448) 或者 [LSF Command Reference](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_welcome/lsf_kc_cmd_ref.html?view=kc) 以获取一些常见配置错误的帮助。