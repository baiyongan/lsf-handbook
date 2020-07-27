# After configuration changes

## About this task

If you make configuration changes to License Scheduler, you must reconfigure License Scheduler to apply the changes. If you make configuration changes to LSF, you must also reconfigure LSF.

## Procedure

1. Run bld -C to test for configuration errors.

2. Run bladmin reconfig all.

3. If you changed lsf.conf or other LSF configuration files, run badmin mbdrestart and lsadmin reconfig.

   **Note**

   After certain License Scheduler configuration changes, you must run **badmin mbdrestart** for the changes to take effect. The following configuration changes require you to run **badmin mbdrestart**:

   - Project changes, additions, or deletions
   - Feature changes, additions, or deletions, including mode changes
   - Cluster locations changes

   You must also run **lsadmin reconfig** for any changes to the LIM to take effect (for example, if you changed LSF_LIC_SCHED_HOSTS).