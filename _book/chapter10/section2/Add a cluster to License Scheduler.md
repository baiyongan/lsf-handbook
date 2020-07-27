# Add a cluster to License Scheduler

## Before you begin

You must be a License Scheduler administrator.

## About this task

You can add a new cluster to an existing License Scheduler implementation.

When adding LSF Advanced Edition clusters, you only need to add the submission clusters to LSF License Scheduler, because the submission clusters will forward LSF License Scheduler jobs to their execution clusters.

## Procedure

1. Download the License Scheduler package.

   **Note**Acquire the same version of master **bld** binary files and other architectures that are used in existing member clusters.

2. Install the License Scheduler package on the new cluster.

3. Use an existing lsf.licensescheduler from $LSF_ENVDIR of another cluster with the same **bld** master.

4. Add new cluster name to the Clusters section of lsf.licensescheduler.

5. Add or modify license distribution policies that are defined in lsf.licensescheduler.

6. Maintain one central lsf.licensescheduler file and have all the clusters access it.

   **Remember**

   The lsf.licensescheduler file in each cluster must be identical.

   You can accomplish this using either of the following methods:

   - Create a symbolic link from each cluster’s $LSF_ENVDIR to the central lsf.licensescheduler file.
   - Use a CRON-based synchronization script to synchronize the changes that are made from the central lsf.licensescheduler file to the corresponding lsf.licensescheduler files in all the clusters.

7. Check that there is no firewall or network issue with communication from the PORT in the lsf.licensescheduler file

8. Run bladmin reconfig on all hosts where **bld** is running.

9. On the newly added cluster, run lsadmin limrestart and then badmin mbdrestart.