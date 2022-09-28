# WAN example

A design center contains the following hosts configuration in a WAN:

LIM starts **bld** on the following hosts:

- lsf.conf in Design Center A

  `LSF_LIC_SCHED_HOSTS="hostA1.designcenter_a.com hostA2.designcenter_a.com hostA3.designcenter_a.com"`

- lsf.conf in Design Center B

  `LSF_LIC_SCHED_HOSTS="hostB1.designcenter_b.com hostB2.designcenter_b.com hostB3.designcenter_b.com"`

License Scheduler candidate hosts are listed in the following order of preference:

- lsf.licensescheduler in Design Center A

  `HOSTS=hostB1.designcenter_b.com hostB2.designcenter_b.com hostA1.designcenter_a.com hostA2.designcenter_a.com hostA3.designcenter_a.com`

- lsf.licensescheduler in Design Center B

  `HOSTS=hostB1.designcenter_b.com hostB2.designcenter_b.com hostB3.designcenter_b.com`

The following diagram shows hostB1.designcenter_b.com, the License Scheduler host for the WAN containing Design Center A and Design Center B.

![img](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/license_scheduler/wan_standby_for_example.jpg)

## How it works

The LSF LIM daemon starts the License Scheduler daemon (**bld**) on each host that is listed in **LSF_LIC_SCHED_HOSTS** in Design Center A and Design Center B.

Each host in the **HOSTS** list in Design Center A is a potential License Scheduler candidate in Design Center A and is running the **bld** daemon, but only one host becomes the License Scheduler host: the first host in the HOSTS list that is up and that is running the **bld** daemon. Similarly, the License Scheduler host in Design Center B is the first host in the HOSTS list that is up and that is running the **bld** daemon.

License Scheduler manages the licenses in Design Center A and Design Center B as follows:

- Both design centers list hostB1.designcenter_b.com at the top of their **HOSTS** lists.
- hostB1.designcenter_b.com is the License Scheduler host for Design Center A and for Design Center B.
- The rest of the hosts in both design centers remain on standby as candidate License Scheduler hosts.
- License Scheduler manages the license scheduling across the WAN connection.