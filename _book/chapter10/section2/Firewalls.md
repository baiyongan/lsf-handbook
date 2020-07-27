# Firewalls

Configuration for LSF, License Scheduler, and **taskman** interoperability.

**Parent topic:**

[Installing and starting License Scheduler](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/license_scheduler/chap_install_start_ls.html?view=kc)

## Set up firewall communication

### About this task

The **mbatchd** and **bld** listening ports (inbound connections) must be open on either side of the firewall.

- **mbatchd**: Set by **LSB_MBD_PORT** in lsf.conf
- **bld**: Set by **PORT** in lsf.licensescheduler

### Procedure

- If a firewall is between the **mbatchd** and **bld** hosts, both listening ports must be open.
- If a firewall is between **bld** and **blcollect** hosts (for example, **blcollect** is configured to run locally on the license servers and **bld** is on the LSF master host), the **bld** listening port must be open.
- If a firewall is between **taskman** and **bld** (where jobs use **taskman** to interface with License Scheduler), the **bld** listening port must be open.