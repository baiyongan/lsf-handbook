# 架构

LSF License Scheduler manages license tokens instead of controlling the licenses directly. Using LSF License Scheduler, jobs receive a license token before starting the application. The number of tokens available from IBM Spectrum LSF (LSF) andIBM Spectrum LSF Advanced Edition (LSF Advanced Edition) corresponds to the number of licenses available from the license server, so if a token is not available, the job does not start. In this way, the number of licenses that are requested by running jobs does not exceed the number of available licenses.

When a job starts, the application is not aware of LSF License Scheduler. The application checks out licenses from the license server in the usual manner.

Figure 1. Daemon interaction![img](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/license_scheduler/lic_sched_daemons.jpg)

## 调度策略如何工作

With LSF License Scheduler, LSF gathers information about the licensing requirements of pending jobs to efficiently distribute available licenses. Other LSF scheduling policies are independent from LSF License Scheduler policies.

The basic LSF scheduling comes first when starting a job. LSF License Scheduler has no influence on job scheduling priority. Jobs are considered for dispatch according to the prioritization policies configured in each cluster.

For example, a job must have a candidate LSF host on which to start before the LSF License Scheduler fairshare policy (for the license project this job belongs to) applies.

Other LSF fairshare policies are based on CPU time, run time, and usage. If LSF fairshare scheduling is configured, LSFdetermines which user or queue has the highest priority, then considers other resources. In this way, the other LSF fairshare policies have priority over LSF License Scheduler.

## 当 mbatchd 脱机时

When a cluster is running, the **mbatchd** maintains a TCP connection to **bld**. When the cluster is disconnected (such as when the cluster goes down or is restarted), the **bld** removes all information about jobs in the cluster. LSF License Scheduler considers licenses that are checked out by jobs in a disconnected cluster to be non-LSF use of licenses.

When **mbatchd** comes back online, the **bld** immediately receives updated information about the number of tokens that are currently distributed to the cluster.

## 当 bld 脱机时



If the **mbatchd** loses the connection with the **bld**, the **mbatchd** cannot get **bld**’s token distribution decisions to update its own.

However, because the **mbatchd** logs token status every minute in$LSF_TOP/work/data/featureName.ServiceDomainName.dat file, if the connection is lost, the **mbatchd** uses the last logged information to schedule jobs.

```shell
f3.LanServer1.dat 
# f3 LanServer1 3 2
# p1 50 p2 50  
  12/3         14:20:38        2    0    2    0         1    0    1    0    
  12/3         14:21:39        2    0    2    0         1    0    1    0    
  12/3         14:22:40        3    3    0    0         0    0    0    0    
  12/3         14:23:41        3    3    0    0         0    0    0    0    
  12/3         14:24:42        1    0    1    0         2    0    2    0    
  12/3         14:25:43        1    0    1    0         2    0    2    0    
  12/3         14:26:44        1    0    1    0         2    0    2    0    
  12/3         14:27:55        1    0    1    0         2    0    2    0    
```

f3 on LanServer1 has three tokens and two projects. Projects p1 and p2 share licenses 50:50.

At 14:27:55, the **bld** dispatched one token to p1, which has 0 in use, 1 free, 0 reserve. At the same time, the **bld**dispatched two tokens to p2, which has 0 in use, 2 free, and 0 reserve.

The **mbatchd** continues to schedule jobs that are based on the token distribution that is logged at 14:27:55 until the connection with the **bld** is re-established.

