# 开启、结束与重配置 LSF

Use LSF administration commands **lsadmin** and **badmin** to start and stop LSF daemons, and reconfigure cluster properties.

## Two LSF administration commands (lsadmin and badmin)

**Important**Only LSF administrators or root can run these commands.

To start and stop , and to reconfigureLSFafter you change any configuration file, use the following commands:

## If you installed LSF as a non-root user

By default, only root can start    

- Multi-user configuration

  Only root can start LSF daemons. Any user can submit jobs to your cluster.For information about changing ownership and permissions for the **lsadmin** and **badmin**commands, see[Troubleshooting LSF problems](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_admin/chap_troubleshooting_lsf.html?view=kc).To permit LSF administrators to start and stop LSF daemons, set up the /etc/lsf.sudoers file, as described in[Configure LSF Startup](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_admin_foundations/config_startup.html?view=kc).

- Single-user

  Your user account must be primary LSF administrator. You are able to start LSF daemons, but only your user account can submit jobs to the cluster. Your user account must be able to read the system kernel information, such as/dev/kmem.

- **Setting up the LSF environment with cshrc.lsf and profile.lsf**
  Before you use LSF, you must set up the LSF execution environment with the cshrc.lsf or profile.lsf file.
- **Starting your cluster**
  Use the **lsadmin** and **badmin** commands to start the LSF daemons.
- **Stopping your cluster**
  Use the **lsadmin** and **badmin** commands to stop the LSF daemons.
- **Reconfiguring your cluster with lsadmin and badmin**
  Use the **lsadmin** and **badmin** commands to reconfigure LSF after you change any configuration file.

**Parent topic:**

[Work with LSF](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_admin_foundations/working_lsf.html?view=kc)

- [LSF Cluster Management and Operations](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_welcome/lsf_kc_cluster_ops.html?view=kc#lsf_kc_cluster_ops)