# Configure LSF License Scheduler Basic Edition

Configure LSF and LSF License Scheduler Basic Edition.

**Parent topic:**

[Install License Scheduler](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/license_scheduler/install_ls.html?view=kc)

## Configuring LSF License Scheduler Basic Edition and LSF

### About this task

Configure LSF to use LSF License Scheduler Basic Edition as a replacement for an **elim** to collect external load indices where the external resources are licenses managed by FlexNet or Reprise License Manager.

The following example assumes that LSF cluster named cluster1 uses an **elim** for a license resource named f1.

### Procedure

1. In the LSF environment, disable the existing **elim** for the license resource by removing the license feature configuration from the lsf.shared and lsf.cluster.cluster_name files.

   For example, remove the configuration for f1 from the lsf.shared and lsf.cluster.cluster_name files.

2. Configure the lsf.licenscheduler file with the appropriate hosts and the license feature.

   For example, configure the following sections in lsf.licenscheduler:

   ```shell
   Begin Parameters
   PORT=1700
   HOSTS=hostA
   ADMIN=lsadmin
   LM_STAT_INTERVAL=15
   LMSTAT_PATH=/usr/bin
   End Parameters
   
   Begin Clusters
   CLUSTERS
   cluster1
   End Clusters
   
   Begin ServiceDomain
   NAME=LanServer
   LIC_SERVERS=((19999@hostA))
   End ServiceDomain
   
   Begin Feature
   NAME=f1
   CLUSTER_MODE=Y
   CLUSTER_DISTRIBUTION=LanServer(cluster1)
   End Feature
   ```

3. Start LSF License Scheduler and LSF.

   For more details, refer to [Start License Scheduler](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/license_scheduler/lic_sched_start.html?view=kc#v2367204).

### What to do next

From LSF, use **bsub** to submit a job without a duration requesting the f1 resource. For example,

bsub -R "rusage[f1=1]" myjob

## Upgrading from LSF License Scheduler Basic Edition to Standard Edition

### About this task

If you use LSF License Scheduler Basic Edition and wish to upgrade to LSF License Scheduler Standard Edition, obtain the LSF License Scheduler entitlement file, then upgrade LSF License Scheduler as follows:

### Procedure

1. Copy the LSF License Scheduler entitlement file (ls.entitlement) to the LSF_ENVDIR directory.

2. Restart LSF License Scheduler.

   bladmin reconfig

3. Restart the **mbatchd** on the LSF master host.

   badmin mbdrestart

## Supported parameters for LSF License Scheduler Basic Edition

The following is a list of specific lsf.licensescheduler parameters that LSF License Scheduler Basic Edition supports:

- Parameters section:

  - ADMIN
  - BLC_HEARTBEAT_FACTOR
  - CLUSTER_MODE (LSF License Scheduler Basic Edition only supports CLUSTER_MODE=Y)
  - HEARTBEAT_INTERVAL
  - HEARTBEAT_TIMEOUT
  - HOSTS
  - LIB_CONNTIMEOUT
  - LIB_RECVTIMEOUT
  - LM_STAT_INTERVAL
  - LM_STAT_TIMEOUT
  - LM_TYPE
  - LMSTAT_PATH
  - LOG_EVENT
  - LOG_INTERVAL
  - LS_DEBUG_BLC
  - LS_DEBUG_BLD
  - LS_DEBUG_CMD
  - LS_LOG_MASK
  - LS_MAX_STREAM_FILE_NUMBER
  - LS_MAX_STREAM_SIZE
  - LS_STREAM_SIZE
  - LS_STREAM_FILE
  - MBD_HEARTBEAT_INTERVAL
  - MBD_REFRESH_INTERVAL
  - RLMSTAT_PATH
  - STANDBY_CONNTIMEOUT

- Clusters section:

  - CLUSTERS (one cluster only, LSF License Scheduler Basic Edition ignores additional clusters)

- ServiceDomain section (one ServiceDomain section per license feature only,

   

  LSF License Scheduler

   

  Basic Edition ignores additional ServiceDomain sections in the same license feature):

  - NAME
  - LIC_SERVERS
  - LM_STAT_INTERVAL
  - LM_STAT_TIMEOUT
  - LM_TYPE
  - LIC_COLLECTOR

- Feature section:

  - NAME
  - CLUSTER_MODE (Optional. This parameter may be specified in the Parameters section instead, but LSF License Scheduler Basic Edition only supports CLUSTER_MODE=Y)
  - LM_LICENSE_NAME (Optional. LSF License Scheduler Basic Edition does not support the specification of multiple license manager feature names to combine into a single alias)
  - CLUSTER_DISTRIBUTION (LSF License Scheduler Basic Edition supports a single cluster with a single service domain only, and ignores any additional clusters or service domains).

##### Tip

A specific lsf.licensescheduler configuration template for LSF License Scheduler Basic Edition is available and contains specifications for all supported parameters. This file is named lsf.licensescheduler.basic and is included in the LSF License Scheduler installation package. LSF License Scheduler uses the Standard Edition configuration file by default, but LSF License Scheduler Basic Edition ignores unsupported Standard Edition parameters with a warning message. To ensure that LSF License Scheduler Basic Edition uses only supported parameters and to prevent the logging of the warning messages, back up the lsf.licensescheduler configuration file, then move the lsf.licensescheduler.basic file to the $LSF_ENVDIR directory and rename it to lsf.licensescheduler.