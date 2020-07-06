# Starting your cluster

Use the **lsadmin** and **badmin** commands to start the LSF daemons.

## Procedure

1. Log in as root to each LSF server host.

   If you installed a single-user cluster as a non-root user, log in as primary LSF administrator.

   Start with the LSF master host, and repeat these steps on all LSF hosts.

2. Use the following commands to start the LSF cluster:

   ```
   # lsadmin limstartup
   # lsadmin resstartup
   # badmin hstartup
   ```

   Before you use any LSF commands, wait a few minutes for the **lim** daemon all hosts to do the following operations:

   - Contact each other
   - Select the master host
   - Exchange initialization information