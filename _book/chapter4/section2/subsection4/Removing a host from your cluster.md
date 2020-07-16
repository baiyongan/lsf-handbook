# Removing a host from your cluster

Removing a host from LSF involves closing a host to prevent any additional jobs from running on the host and removing references to the host from the lsf.cluster.cluster_name file and other configuration files.

## About this task

CAUTION

Never remove the master host from LSF. If you want to change your current default master host, change the lsf.cluster.cluster_name file to assign a different default master host. Then remove the host that was formerly the master host.

## Procedure

1. Log on to the LSF host as root.

2. Run **badmin hclose** to close the host.

   Closing the host prevents jobs from being dispatched to the host and allows running jobs to finish.

3. Stop all running daemons manually.

4. Remove any references to the host in the Host section of the LSF_CONFDIR/lsf.cluster.cluster_name file.

5. Remove any other references to the host, if applicable, from the following configuration files:

   - LSF_CONFDIR/lsf.shared
   - LSB_CONFDIR/cluster_name/configdir/lsb.hosts
   - LSB_CONFDIR/cluster_name/configdir/lsb.queues
   - LSB_CONFDIR/cluster_name/configdir/lsb.resources

6. Log off the host to be removed, and log on as root or the primary LSF administrator to any other host in the cluster.

7. Run the **lsadmin reconfig** command to reconfigure LIM.

   ```
   % lsadmin reconfig
   Checking configuration files ...
   No errors found.
   Do you really want to restart LIMs on all hosts? [y/n] y
   Restart LIM on <hosta> ...... done
   Restart LIM on <hostc> ...... done
   ```

   The **lsadmin reconfig** command checks for configuration errors.

   If no errors are found, you are asked to confirm that you want to restart **lim** on all hosts and **lim** is reconfigured. If unrecoverable errors are found, reconfiguration exits.

8. Run the **badmin mbdrestart** command to restart **mbatchd**.

   ```
   % badmin reconfig
   Checking configuration files ...
   No errors found.
   Do you want to reconfigure? [y/n] y
   Reconfiguration initiated
   ```

   The **badmin mbdrestart** command checks for configuration errors.

   If no unrecoverable errors are found, you are asked to confirm reconfiguration. If unrecoverable errors are found, reconfiguration exits.

9. If you configured LSF daemons to start automatically at system startup, remove the LSF section from the host’s system startup files.

   For more information about automatic LSF daemon startup, see [Setting up automatic LSF startup](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_admin_foundations/auto_startup.html?view=kc#auto_startup76)

10. If any users of the host use the **lstcsh** shell as their login shell, change their login shell to tcsh or csh. Remove **lstcsh** from the /etc/shells file.

## Results

- Use dynamic host configuration to remove hosts to the cluster without manually changing the LSF configuration. For more information about removing hosts dynamically, see [IBM Platform LSF Cluster Management and Operations](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_welcome/lsf_kc_cluster_ops.html?view=kc).
- If you get errors, see [../lsf_admin/chap_troubleshooting_lsf.html#v3523448](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_admin/chap_troubleshooting_lsf.html?view=kc#v3523448) for help with some common configuration errors.