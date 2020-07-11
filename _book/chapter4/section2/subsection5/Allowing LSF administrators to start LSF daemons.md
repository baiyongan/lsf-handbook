# Allowing LSF administrators to start LSF daemons

To allow LSF administrators to start and stop LSF daemons, configure the /etc/lsf.sudoers file. If the lsf.sudoers file does not exist, only root can start and stop LSF daemons.

## About this task

Using the lsf.sudoers file requires you to enable the setuid bit. Since this allows LSF administration commands to run with root privileges, do not proceed if you do not want these commands to run with root privileges.

## Procedure

1. Log on as root to each LSF server host.

   Start with the LSF master host, and repeat these steps on all LSF hosts.

2. Create an /etc/lsf.sudoers file on each LSF host and specify the **LSF_STARTUP_USERS** and **LSF_STARTUP_PATH** parameters.

   ```
   LSF_STARTUP_USERS="lsfadmin user1"
   LSF_STARTUP_PATH=/usr/share/lsf/cluster1/10.1/sparc-sol2/etc
   ```

   **LSF_STARTUP_PATH** is normally the path to the LSF_SERVERDIR directory, where the LSF server binary files (**lim**, **res**, **sbatchd**, **mbatchd**, **mbschd**, and so on) are installed, as defined in your LSF_CONFDIR/lsf.conf file.

   The lsf.sudoers file must have file permission mode -rw------- (600) and be readable and writable only by root:

   ```
   # ls -la /etc/lsf.sudoers
   -rw-------   1 root     lsf           95 Nov 22 13:57 lsf.sudoers
   ```

3. Run the **lsfrestart** command to restart the cluster:

   ```
   # lsfrestart
   ```