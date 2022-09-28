# Configure and start License Scheduler in a WAN

## About this task

In a WAN configuration:

## Procedure

1. As the root user, install License Scheduler on each cluster in the WAN configuration and select one cluster to be the main cluster.

2. In the cluster that contains the WAN license server, log on as the primary License Scheduler administrator.

3. Edit the following items in LSF_CONFDIR/lsf.licensescheduler:

   1. Specify a space-separated list of hosts for the HOSTS parameter:

      HOSTS=hostname_1 hostname_2 ... hostname_n

      Where:

      hostname_1 is the most preferred host for running License Scheduler.

      hostname_n is the least preferred host for running License Scheduler.

   2. In the Clusters section, specify the names of the clusters in the WAN.

      For example:

      ```
      Begin Clusters
      CLUSTERS
      design_SJ
      design_BOS
      End Clusters
      ```

4. In the cluster that contains the WAN license server, as the LSF primary administrator, edit LSF_CONFDIR/lsf.conf. Lines that begin with # are comments:

   Specify a space-separated list of hosts for the LSF_LIC_SCHED_HOSTS parameter:

   LSF_LIC_SCHED_HOSTS="hostname_1 hostname_2 ... hostname_n"

   Where:

   hostname_1, hostname_2, ..., hostname_n are hosts on which the LSF LIM daemon starts the License Scheduler daemon (**bld**).

   The first host that is listed in the HOSTS list is the default master License Scheduler host for the WAN.

   The order of the host names in LSF_LIC_SCHED_HOSTS is ignored.

5. In the other clusters in the WAN:

   1. Configure the LSF_LIC_SCHED_HOSTS parameter in lsf.conf with a local list of candidate hosts.
   2. Configure the HOSTS parameter in the Parameters section lsf.licensescheduler with the following list of hosts:
      - Start the list with the same list of candidate hosts as the HOSTS parameter in the cluster that contains the WAN license server.
      - Continue the list with the local cluster’s list of hosts from the LSF_LIC_SCHED_HOSTS parameter in lsf.conf.

6. In the cluster that contains the WAN license server and the other clusters in the WAN, run the following commands:

   1. Run **bld -C** to test for configuration errors.
   2. Run **bladmin reconfig** to configure License Scheduler.
   3. Run lsadmin reconfig to reconfigure LIM.
   4. Use ps -ef to make sure that **bld** is running on the candidate hosts.
   5. Run badmin reconfig to reconfigure **mbatchd**.

   **Tip**Although the **bld** daemon is started by LIM, **bld** runs under the account of the primary License Scheduler administrator. If you did not configure the LIM to automatically start the **bld** daemon on your License Scheduler hosts, run **$LSF_BINDIR/blstartup** on each host to start the **bld** daemon.