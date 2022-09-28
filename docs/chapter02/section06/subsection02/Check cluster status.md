# 检查集群状态

**lsid** 命令告诉您是否正确设置了 LSF 环境。 **lsload** 命令显示集群的当前负载级别。

## lsid 命令

lsid 命令显示集群的当前 LSF 版本号，集群名称和当前 LSF 主主机的主机名。

lsid 命令显示的 LSF 主名称可以有所不同，但通常是 LSF_CONFDIR/lsf.cluster.cluster_name 文件的 Hosts 部分中配置的第一台主机。

```shell
% lsid
IBM Spectrum LSF Standard 10.1.0.0, Apr 04 2016
Copyright International Business Machines Corp, 1992-2016.
US Government Users Restricted Rights - Use, duplication or disclosure restricted by GSA ADP Schedule Contract with IBM Corp.

My cluster name is cluster1
My master name is hosta
```

如果看到如下消息

```shell
Cannot open lsf.conf file
```

LSF_ENVDIR 环境变量可能未正确设置。 使用 cshrc.lsf 或 profile.lsf 文件来设置您的环境。 有关更多帮助，请参见 [Troubleshooting LSF problems](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_admin/troubleshooting_common_problems_lsf.html?view=kc#v3534299) 来寻求帮助。

## lsload 命令

**lsload**命令的输出为集群中的每个主机包含一行。 集群中所有主机的正常状态是 ok。

```shell
% lsload
HOST_NAME  status  r15s  r1m  r15m  ut   pg   ls  it  tmp  swp   mem
hosta      ok      0.0   0.0  0.1   1%   0.0  1   224 43G  67G   3G
hostc      -ok     0.0   0.0  0.0   3%   0.0  3   0   38G  40G   7G
hostf      busy    *6.2  6.9  9.5   85%  1.1  30  0   5G   400G  385G
hosth      busy    0.1   0.1  0.3   7%   *17  6   0   9G   23G   28G
hostv      unavail
```

对于任何负载指数超过其配置阈值的主机，将显示繁忙状态。 星号（*）标记了超出其阈值的负载索引，从而导致主机状态为繁忙。 值 o k前面的减号（-）表示 res 未在该主机上运行。

如果在启动或重新配置 LSF 之后看到以下消息之一，请等待几秒钟，然后再次尝试 **lsload** 命令，以使所有主机上的 lim 守护程序有时间初始化。

```shell
lsid: getentitlementinfo() failed: LIM is down; try later
```

或者

```shell
LSF daemon (LIM) not responding ... still trying
```

如果问题仍然存在，请参阅 [Troubleshooting LSF problems](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_admin/troubleshooting_common_problems_lsf.html?view=kc#v3534299) 。

## 其他有用的命令

- **bparams** 命令显示有关 LSF 批处理系统配置参数的信息。
- **bhist** 命令显示有关作业的历史信息。