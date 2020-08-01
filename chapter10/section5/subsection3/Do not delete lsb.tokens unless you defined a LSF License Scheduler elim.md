# Do not delete lsb.tokens unless you defined a LSF License Scheduler elim

The lsb.tokens file contains allocation and usage information on features that are allocated to the cluster. Do not remove or modify this file unless you defined an **elim** for LSF License Scheduler to ensure that LSF can still schedule LSF License Scheduler jobs even if the connection between **mbatchd** and **bld** is broken.

When **mbatchd** connects with the **bld** to obtain load updates, **mbatchd** gets the license usage information from **bld** and creates the lsb.tokens file (located in LSB_SHAREDIR/cluster_name/logdir) to save the allocation and usage of all features that are allocated to the cluster. The **MBD_REFRESH_INTERVAL** parameter in lsf.licensescheduler, which controls the minimum interval between load updates, also specifies the interval between updates for the lsb.tokens file.

This file ensures that even if the connection between **mbatchd** and **bld** is broken, LSF can still use the last license usage information in lsb.tokens to schedule new LSF License Scheduler jobs. If you delete lsb.tokens, LSF is unable to schedule LSF License Scheduler jobs.

## Creating a LSF License Scheduler **elim**

If the connection between **mbatchd** and **bld** is broken because of a bad network or because **bld** is down, you can also define a dynamic resource with the same name as the LSF License Scheduler feature and create an **elim** to get the number of free licenses to ensure that LSF can still schedule pending LSF License Scheduler jobs.

In this case, if **bld** is down or disconnected, the LSF License Scheduler resource overrides the LSF dynamic resource even though **bld** is down, and cannot be reserved by any job.

To avoid this problem, remove the lsb.tokens file when LSF License Scheduler is down or disconnected.