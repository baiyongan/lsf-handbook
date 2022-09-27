# Service provisioning at the host and network levels

In the following example configuration, there are two potential points of failure: host and network.

## Host failure

If hostB1.designcenter_b.com fails, and **bld** stops running, a candidate License Scheduler host must take over the license management. The next host on the HOSTS list in both Design Center A and Design Center B is hostB2designcenter_b.com. License Scheduler fails over to this host if it is up and running.

![img](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/license_scheduler/wan_standby_host_fail.jpg)

## Network failure

If the network connection between Design Center A and Design Center B breaks, Design Center A can no longer communicate with the hosts in Design Center B, so hostB1.designcenter_b.com and hostB2.designcenter_b.com are no longer candidate license scheduling hosts for Design Center A. The next candidate host for Design Center A is hostA1.designcenter_a.com. License management then runs locally in Design Center A on hostA1.designcenter_a.com. In Design Center B, hostB1.designcenter_b.com continues to run License Scheduler, but only manages the local network if the wide area network connection is down.

The local License Scheduler host, hostA1.designcenter_a.com, checks for a heartbeat from hostB1.designcenter_b.com at regular intervals, then returns license management back to hostB1.designcenter_b.com when the network connection returns.

![img](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/license_scheduler/wan_standby_wan_fail.jpg)

**Parent topic:**

[Failover provisioning for WANs](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/license_scheduler/failover_wans.html?view=kc)