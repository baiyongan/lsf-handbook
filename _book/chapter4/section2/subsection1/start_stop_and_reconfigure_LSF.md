# 开启、结束与重配置 LSF

Use LSF administration commands **lsadmin** and **badmin** to start and stop LSF daemons, and reconfigure cluster properties.

## Two LSF administration commands (lsadmin and badmin)

**Important**Only LSF administrators or root can run these commands.

To start and stop LSF, and to reconfigure LSF after you change any configuration file, use the following commands:

- The **lsadmin** command controls the operation of the **lim** and **res** daemons.
- The **badmin** command controls the operation of the **mbatchd** and **sbatchd** daemons.

## If you installed LSF as a non-root user

By default, only root can start LSF daemons. If the **lsfinstall** command detected that you installed as non-root user, you chose to configure either a multi-user cluster or a single-user cluster:

- Multi-user configuration

  Only root can start LSF daemons. Any user can submit jobs to your cluster.For information about changing ownership and permissions for the **lsadmin** and **badmin**commands, see [Troubleshooting LSF problems](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_admin/chap_troubleshooting_lsf.html?view=kc).To permit LSF administrators to start and stop LSF daemons, set up the /etc/lsf.sudoers file, as described in [Configure LSF Startup](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_admin_foundations/config_startup.html?view=kc).

- Single-user

  Your user account must be primary LSF administrator. You are able to start LSF daemons, but only your user account can submit jobs to the cluster. Your user account must be able to read the system kernel information, such as /dev/kmem.

**[Setting up the LSF environment with cshrc.lsf and profile.lsf](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_admin_foundations/set_lsf_env.html?view=kc)**
Before you use LSF, you must set up the LSF execution environment with the cshrc.lsf or profile.lsf file.**[Starting your cluster](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_admin_foundations/start_cluster.html?view=kc)**
Use the **lsadmin** and **badmin** commands to start the LSF daemons.**[Stopping your cluster](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_admin_foundations/stop_cluster.html?view=kc)**
Use the **lsadmin** and **badmin** commands to stop the LSF daemons.**[Reconfiguring your cluster with lsadmin and badmin](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_admin_foundations/reconfig_cluster.html?view=kc)**
Use the **lsadmin** and **badmin** commands to reconfigure LSF after you change any configuration file.