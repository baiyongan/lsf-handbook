# Set up fod

## About this task

The **fod** daemon manages failover for the **blcollect** daemons. **fod** can restart any failed **blcollect** processes if the local host (and thus the local **fod**) is down. The failover host **fod** starts new **blcollect** daemons until the primary host comes back online and the primary **fod** contacts the secondary **fod**.

The fod files are in the License Scheduler package, but must be copied, configured, and started manually.

## Procedure

1. Install the failover daemon (**fod**) files on each host.

   1. Create a directory to hold the **fod** files, with subdirectories bin, conf, etc, and man.

      For example: /usr/local/fod

   2. Copy all user command files and the fod.shell file to .../bin.

   3. Copy the fod.conf file to .../conf.

   4. Copy the fod file to .../etc.

   5. Copy the fodapps.1, fodhosts.1 and fodid.1 files to .../man/man1.

   6. Copy the fod.conf.5 file to .../man/man5.

   7. Copy the fodadmin.8 file to .../man/man8.

2. Edit the fod.shell file, and set the **FOD_ROOT** parameter to the name of your new directory.

   For example: FOD_ROOT=/usr/local/fod

3. Set the environment variables.

   1. Set the **PATH** environment variable to include the /bin directory.
   2. Set the **FOD_ENVDIR** environment variable to $FOD_ROOT/conf.
   3. Set the **MANPATH** environment variable to include the /man directory.

4. In fod.conf, set the required parameters.

   - **FOD_ADMIN**: The License Scheduler administrator
   - **FOD_PORT**: The TCP listening port and UDP port for the failover daemon
   - **FOD_WORK_DIR**: The working directory
   - **FOD_LOG_DIR**: The log directory

   For example:

   FOD_CLUSTERNAME = fod

   FOD_ADMIN = lsadmin

   FOD_PORT = 9583

   FOD_WORK_DIR = /usr/local/fod/work

   FOD_LOG_DIR = /usr/local/fod/work

5. In the **Hosts** section of fod.conf, specify the hosts where the failover daemons run.

   If your hosts run in different DNS domains, you must use a fully qualified domain name when you specify the host name. The first host in the **Hosts** section is the first host on which the failover daemon runs (the master failover daemon host).

   ```
   Begin Hosts
   HOSTNAME
   fodhost1.domain_name
   fodhost2
   End Host
   ```

6. Modify the **Applications** section of fod.conf.

   ```
   Begin Applications
   NAME         PATH                                  PARAMS     FATAL_EXIT_VALUE
   blcollect   /pcc/apps/lsf6/6.0/sparc-sol7-64/etc   (-2 -m "sasun3 augustus claudius" -p 9581 -c lan -i 20
   -D /sparc-sol7-64/etc)   (-)        
   End Applications
   ```

7. Start **fod** on each host.

   1. Log on as the IBM Spectrum LSF License Scheduler administrator.

   2. Source the LSF environment.

      - For **csh** or **tsh** run source LSF_TOP/conf/cshrc.lsf
      - For **sh**, **ksh**, or **bash**, run . LSF_TOP/conf/profile.lsf

   3. Launch the failover daemons by running the fod.shell file.

      Check the progress of a successful launch by running **ps -ef**.

      View the **fod** log under **$LSF_LOGDIR**.

      Check configuration from $FOD_ROOT/etc by running **fod -C**.