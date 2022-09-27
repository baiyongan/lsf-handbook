# Failover provisioning for LANs

## About this task

Configuring failover ensures enhanced performance and reliable license distribution.

You only need one host to run License Scheduler, but you can configure your site for a failover mechanism with multiple candidate hosts to take over the scheduling if there is a failure. This configuration can be used in a local network or across multiple sites in a wider network.

## Procedure

Define the list of License Scheduler hosts in LSF_CONFDIR/lsf.conf and lsf.licensescheduler for your LAN (Designer Center A in this example).

1. lsf.conf: Specify a space-separated list of hosts for the **LSF_LIC_SCHED_HOSTS** parameter:

   LSF_LIC_SCHED_HOSTS="hostA.designcenter_a.com hostB.designcenter_a.com hostC.designcenter_a.com"

   **Tip**List the hosts in order of preference for running License Scheduler, from most preferred to least preferred.

2. lsf.licensescheduler: Specify a space-separated list of hosts for the HOSTS parameter:

   HOSTS=hostA.designcenter_a.com hostB.designcenter_a.com hostC.designcenter_a.com

   List the hosts in the same order as lsf.conf.

The LIM starts the **bld** (License Scheduler daemon) on each host in the **LSF_LIC_SCHED_HOSTS** list.

Every host in defined in **LSF_LIC_SCHED_HOSTS** is a failover candidate and runs the **bld** daemon.

![img](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/license_scheduler/lan_standby.jpg)

- hostA.designcenter_a.com is the License Scheduler host, and the remaining hosts are candidate hosts that are running the **bld** daemon, ready to take over the management of the licenses if there is a network failure
- Each host contains the list of candidate hosts in memory
- Each candidate License Scheduler host communicates with the License Scheduler host, License Scheduler (hostA)
- If the License Scheduler host fails, each candidate host checks to see if a more eligible host is running the License Scheduler daemon. If not, it becomes the failover host and inherits the communication links that existed between the original License Scheduler host and each candidate host. In this example, if License Scheduler on hostA fails, candidate License Scheduler hostB is the next most eligible host, and takes over the license scheduling.