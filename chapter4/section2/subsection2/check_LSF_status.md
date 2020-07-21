# 检查 LSF 状态

Use LSF administration commands to check cluster configuration, see cluster status, and LSF batch workload system configuration and status.

## Example command output

The LSF commands that are shown in this section show examples of typical output. The output that you see might differ according to your configuration.

The commands are described briefly so that you can easily use them to verify your LSF installation. See the [LSF Command Reference](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_welcome/lsf_kc_cmd_ref.html?view=kc) or the LSF man pages for complete usage and command options. You can use these commands on any LSF host.

If you get proper output from these commands, your cluster is ready to use. If your output has errors, see [Troubleshooting LSF problems](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_admin/chap_troubleshooting_lsf.html?view=kc#v3523448) for help.

**[Check cluster configuration with the lsadmin command](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_admin_foundations/check_config.html?view=kc)**
The **lsadmin** command controls the operation of an LSF cluster and administers the LSF daemons **lim** and **res**.

**[Check cluster status with the lsid and lsload commands](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_admin_foundations/cluster_status.html?view=kc)**
The **lsid** command tells you if your LSF environment is set up properly. The **lsload** command displays the current load levels of the cluster.

**[Check LSF batch system configuration with badmin](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_admin_foundations/batch_config.html?view=kc)**
The **badmin** command controls and monitors the operation of the LSF batch workload system.

**[Find out batch system status with bhosts and bqueues](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_admin_foundations/batch_status.html?view=kc)**
Use the **bhosts** command to see whether the LSF batch workload system is running properly. The **bqueues** command displays the status of available queues and their configuration parameters.

