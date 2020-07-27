# Upgrade License Scheduler

## Before you begin

You must have License Scheduler installed before you can upgrade. You must be a cluster administrator.

## About this task

You can upgrade to a new version of License Scheduler without uninstalling and reinstalling.

## Procedure

1. Download the new version of the License Scheduler distribution tar files.

2. Deactivate all queues.

   Deactivating all queues pends any running jobs and prevents new jobs from being dispatched.

   badmin qinact all

3. If you have the IBM Spectrum LSF Application Center installed, shut it down.

   pmcadmin stop

4. Back up your existing **LSF_CONFDIR**, **LSB_CONFDIR**, and **LSB_SHAREDIR** according to the procedures at your site.

5. Optional. To use the fast dispatch project mode in LSF License Scheduler, upgrade LSF to version higher than 9.1.1.

   After completing the upgrade, restart LSF.

6. Use the setup script to upgrade LSF License Scheduler.

   1. Source cshrc.lsf or profile.lsf in old LSF cluster.
   2. Navigate to the location of your tar files and extract.
   3. Run the setup script.

7. If you are installing License Scheduler Standard Edition, copy the License Scheduler entitlement file (ls.entitlement) to the $LSF_ENVDIR directory.

   If you do not copy the entitlement file to $LSF_ENVDIR before starting License Scheduler, License Scheduler runs as Basic Edition.

8. Start License Scheduler.

   1. Source cshrc.lsf or profile.lsf.

   2. Run bladmin reconfig.

   3. Run ps -ef to make sure the **bld** is running on the candidate hosts.

   4. Run badmin mbdrestart.

   5. Activate the queues.

      badmin qact all

9. If you have the IBM Spectrum LSF Application Center installed, restart it.

   pmcadmin start

   **Note**

   IBM Spectrum LSF Application Center displays License Scheduler workload for both project mode and cluster mode.