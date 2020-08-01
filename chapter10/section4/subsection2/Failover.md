# Failover

## License maximization

The built-in functionality of License Scheduler helps ensure that your licenses are always being used efficiently. For example, if the **sbatchd** encounters any problems, the job acquires the state UNKNOWN. However, License Scheduler ensures that any in use licenses continue to be allocated, but charges them to the OTHERS category until the **sbatchd** recovers and the job state is known again.

## failover host

A master candidate host that runs the License Scheduler daemon (**bld**), and can take over license management if the master License Scheduler host fails or loses its connection to the network (in either a LAN or WAN environment).

## failover provisioning

The configuration of a list of failover hosts in the event of a host failure or network breakdown. License Scheduler can be configured for failover provisioning in both LANs and WANs.

**[Failover provisioning for LANs](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/license_scheduler/configure_lan_failover.html?view=kc)**
**[Failover provisioning for WANs](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/license_scheduler/failover_wans.html?view=kc)**
**[Set up fod](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/license_scheduler/fod_setup.html?view=kc)**