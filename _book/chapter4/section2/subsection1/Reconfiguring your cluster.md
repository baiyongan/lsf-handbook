# Reconfiguring your cluster

Use the **lsadmin** and **badmin** commands to reconfigure LSF after you change any configuration file.

## Procedure

1. Log in as root to each LSF server host.

   If you installed a single-user cluster as a non-root user, log in as primary LSF administrator.

2. Use the following commands to reconfigure the LSF cluster:

   - Reload modified

      

     LSF

      

     configuration files and restart

      

     lim

     :

     ```
     # lsadmin reconfig
     ```

   - Reload modified

      

     LSF

      

     batch configuration files:

     ```
     # badmin reconfig
     ```

   - Reload modified

      

     LSF

      

     batch configuration files and restart

      

     mbatchd

     :

     ```
     # badmin mbdrestart
     ```

   This command also reads the LSF_LOGDIR/lsb.events file, so it can take some time to complete if a lot of jobs are running.