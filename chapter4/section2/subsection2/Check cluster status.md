# Check cluster status

The **lsid** command tells you if your LSF environment is set up properly. The **lsload** command displays the current load levels of the cluster.

## lsid command

The **lsid** command displays the current LSF version number, cluster name, and host name of the current LSF master host for your cluster.

The LSF master name that is displayed by the **lsid** command can vary, but it is usually the first host that is configured in the 

Hosts

 section of the LSF_CONFDIR/lsf.cluster.cluster_name file.

```
% lsid
IBM Spectrum LSF Standard 10.1.0.0, Apr 04 2016
Copyright International Business Machines Corp, 1992-2016.
US Government Users Restricted Rights - Use, duplication or disclosure restricted by GSA ADP Schedule Contract with IBM Corp.

My cluster name is cluster1
My master name is hosta
```

If you see the message

```
Cannot open lsf.conf file
```

The LSF_ENVDIR environment variable is probably not set correctly. Use the cshrc.lsf or profile.lsf file to set up your environment. See [Troubleshooting LSF problems](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_admin/troubleshooting_common_problems_lsf.html?view=kc#v3534299) for more help

## lsload command

The output of the **lsload** command contains one line for each host in the cluster. Normal status is ok for all hosts in your cluster.

```
% lsload
HOST_NAME  status  r15s  r1m  r15m  ut   pg   ls  it  tmp  swp   mem
hosta      ok      0.0   0.0  0.1   1%   0.0  1   224 43G  67G   3G
hostc      -ok     0.0   0.0  0.0   3%   0.0  3   0   38G  40G   7G
hostf      busy    *6.2  6.9  9.5   85%  1.1  30  0   5G   400G  385G
hosth      busy    0.1   0.1  0.3   7%   *17  6   0   9G   23G   28G
hostv      unavail
```

A busy status is shown for hosts with any load index beyond their configured thresholds. An asterisk (*) marks load indexes that are beyond their thresholds, causing the host status to be busy. A minus sign (-) in front of the value ok means that res is not running on that host.

If you see one of the following messages after you start or reconfigure LSF, wait a few seconds and try the **lsload** command again to give the **lim** daemon on all hosts time to initialize.

```
lsid: getentitlementinfo() failed: LIM is down; try later
```

or

```
LSF daemon (LIM) not responding ... still trying
```

If the problem persists, see [Troubleshooting LSF problems](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_admin/troubleshooting_common_problems_lsf.html?view=kc#v3534299) for help.

## Other useful commands

- The **bparams** command displays information about the LSF batch system configuration parameters.
- The **bhist** command displays historical information about jobs.