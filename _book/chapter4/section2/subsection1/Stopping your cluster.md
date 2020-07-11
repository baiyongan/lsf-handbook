# Stopping your cluster

Use the **lsadmin** and **badmin** commands to stop the LSF daemons.

## Procedure

1. Log in as root to each LSF server host.

   If you installed a single-user cluster as a non-root user, log in as primary LSF administrator.

2. Use the following commands to stop the LSF cluster:

   ```
   # badmin hshutdown all
   # lsadmin resshutdown all
   # lsadmin limshutdown all
   ```