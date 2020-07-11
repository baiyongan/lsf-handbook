# 常见 LSF 问题

Most problems are due to incorrect installation or configuration. Before you start to troubleshoot LSF problems, always check the error log files first. Log messages often point directly to the problem.

**Parent topic:**

[Troubleshooting LSF problems](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_admin/chap_troubleshooting_lsf.html?view=kc)

## Finding LSF error logs

When something goes wrong, LSF server daemons log error messages in the LSF log directory (specified by the **LSF_LOGDIR** parameter in the lsf.conf file).

### Procedure

Make sure that the primary LSF administrator owns **LSF_LOGDIR**, and that root can write to this directory.

If an LSF server is unable to write to **LSF_LOGDIR**, then the error logs are created in /tmp. LSF logs errors to the following files:

- lim.log.host_name
- res.log.host_name
- pim.log.host_name
- mbatchd.log.master_host
- mbschd.log.master_host
- sbatchd.log.host_name
- vemkd.log.master_host

If these log files contain any error messages that you do not understand, contact IBM Support.

## Diagnosing and fixing most LSF problems

General troubleshooting steps for most LSF problems.

### Procedure

1. Run the **lsadmin ckconfig -v** command and note any errors that are shown in the command output.

   Look for the error in one of the problems described in this section. If none of these troubleshooting steps applies to your situation, contact IBM Support.

2. Use the following commands to restart the LSF cluster:

   ```
   # lsadmin limrestart all
   # lsadmin resrestart all
   # badmin hrestart all
   ```

3. Run the **ps -ef** command to see whether the LSF daemons are running.

   Look for the processes similar to the following command output:

   ```
   root 17426     1  0   13:30:40 ?    0:00 /opt/lsf/cluster1/10.1/sparc-sol10/etc/lim
   root 17436     1  0   13:31:11 ?    0:00 /opt/lsf/cluster1/10.1/sparc-sol10/etc/sbatchd
   root 17429     1  0   13:30:56 ?    0:00 /opt/lsf/cluster1/10.1/sparc-sol10/etc/res
   ```

4. Check the LSF error logs on the first few hosts that are listed in the Host section of the LSF_CONFDIR/lsf.cluster.cluster_name file.

   If the **LSF_MASTER_LIST** parameter is defined in the LSF_CONFDIR/lsf.conf file, check the error logs on the hosts that are listed in this parameter instead.

## Cannot open lsf.conf file

You might see this message when you run the **lsid** file. The message usually means that the LSF_CONFDIR/lsf.conf file is not accessible to LSF.

### About this task

By default, LSF checks the directory that is defined by the **LSF_ENVDIR** parameter for the lsf.conf file. If the lsf.conf file is not in **LSF_ENVDIR**, LSF looks for it in the /etc directory.

For more information, see [Setting up the LSF environment with cshrc.lsf and profile.lsf](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_admin_foundations/set_lsf_env.html?view=kc#set_lsf_env4387).

### Procedure

- Make sure that a symbolic link exists from /etc/lsf.conf to lsf.conf
- Use the csrhc.lsf or profile.lsf script to set up your LSF environment.
- Make sure that the cshrc.lsf or profile.lsf script is available for users to set the LSF environment variables.

## LIM dies quietly

When the LSF LIM daemon exits unexpectedly, check for errors in the LIM configuration files.

### Procedure

Run the following commands:

lsadmin ckconfig -v

This command displays most configuration errors. If the command does not report any errors, check in the LIM error log.

## LIM communication times out

Sometimes the LIM is up, but running the **lsload** command prints the following error message:Communication time out.

### About this task

If the LIM just started, LIM needs time to get initialized by reading configuration files and contacting other LIMs. If the LIM does not become available within one or two minutes, check the LIM error log for the host you are working on.

To prevent communication timeouts when the local LIM is starting or restarting, define the parameter **LSF_SERVER_HOSTS** in the lsf.conf file. The client contacts the LIM on one of the **LSF_SERVER_HOSTS** and runs the command. At least one of the hosts that are defined in the list must have a LIM that is up and running.

When the local LIM is running but the cluster has no master, LSF applications display the following message:

```
Cannot locate master LIM now, try later.
```

### Procedure

Check the LIM error logs on the first few hosts that are listed in the Host section of the lsf.cluster.cluster_name file. If the **LSF_MASTER_LIST** parameter is defined in the lsf.conf file, check the LIM error logs on the hosts that are listed in this parameter instead.

## Master LIM is down

Sometimes the master LIM is up, but running the **lsload** or **lshosts** command displays the following error message: Master LIM is down; try later.

### About this task

If the /etc/hosts file on the host where the master LIM is running is configured with the host name that is assigned to the loopback IP address (127.0.0.1), LSF client LIMs cannot contact the master LIM. When the master LIM starts up, it sets its official host name and IP address to the loopback address. Any client requests get the master LIM address as 127.0.0.1, and try to connect to it, and in fact tries to access itself.

### Procedure

Check the IP configuration of your master LIM in /etc/hosts.

The following example incorrectly sets the master LIM IP address to the loopback address:

```
127.0.0.1   localhost   myhostname
```

The following example correctly sets the master LIM IP address:

```
127.0.0.1    localhost
192.168.123.123   myhostname
```

For a master LIM running on a host that uses an IPv6 address, the loopback address is

```
::1 
```

The following example correctly sets the master LIM IP address by using an IPv6 address:

```
::1    localhost ipv6-localhost ipv6-loopback 
 
fe00::0     ipv6-localnet 
 
ff00::0     ipv6-mcastprefix
ff02::1     ipv6-allnodes
ff02::2     ipv6-allrouters
ff02::3     ipv6-allhosts
```

## User permission denied

If the remote host cannot securely determine the user ID of the user that is requesting remote execution, remote execution fails with the following error message: User permission denied..

### Procedure

1. Check the RES error log on the remote host for more detailed error message.

2. If you do not want to configure an identification daemon (**LSF_AUTH** in lsf.conf), all applications that do remote executions must be owned by root with the **setuid** bit set. Run the following command:

   ```
   chmod 4755 filename
   ```

3. If the application binary files are on an NFS-mounted file system, make sure that the file system is not mounted with the **nosuid** flag.

4. If you are using an identification daemon (the **LSF_AUTH** parameter in the lsf.conf file), the **inetd** daemon must be configured. The identification daemon must not be run directly.

5. Inconsistent host names in a name server with /etc/hosts and /etc/hosts.equiv can also cause this problem. If the **LSF_USE_HOSTEQUIV** parameter is defined in the lsf.conf file, check that the /etc/hosts.equiv file or the HOME/.rhosts file on the destination host has the client host name in it.

6. For Windows hosts, users must register and update their Windows passwords by using the **lspasswd** command. Passwords must be 3 characters or longer, and 31 characters or less.

   For Windows password authentication in a non-shared file system environment, you must define the parameter **LSF_MASTER_LIST** in the lsf.conf file so that jobs run with correct permissions. If you do not define this parameter, LSF assumes that the cluster uses a shared file system environment.

## Remote execution fails because of non-uniform file name space

A non-uniform file name space might cause a command to fail with the following error message: chdir(...) failed: no such file or directory.

### About this task

You are trying to run a command remotely, but either your current working directory does not exist on the remote host, or your current working directory is mapped to a different name on the remote host.

If your current working directory does not exist on a remote host, do not run commands remotely on that host.

### Procedure

- If the directory exists, but is mapped to a different name on the remote host, you must create symbolic links to make them consistent.

- LSF can resolve most, but not all, problems by using **automount**. The automount maps must be managed through NIS.

  Contact IBM Support if you are running automount and LSF is not able to locate directories on remote hosts.

## Batch daemons die quietly

When the LSF batch daemons **sbatchd** and **mbatchd** exit unexpectedly, check for errors in the configuration files.

### About this task

If the **mbatchd** daemon is running but the **sbatchd** daemon dies on some hosts, it might be because **mbatchd** is not configured to use those hosts.

### Procedure

- Check the **sbatchd** and **mbatchd** daemon error logs.
- Run the **badmin ckconfig** command to check the configuration.
- Check for email in the LSF administrator mailbox.

## sbatchd starts but mbatchd does not

When the **sbatchd** daemon starts but the mbatchd daemon is not running, it is possible that **mbatchd** is temporarily unavailable because the master LIM is temporarily unknown. The following error message is displayed: sbatchd: unknown service.

### Procedure

1. Run the **lsid** command to check whether LIM is running.

   If LIM is not running properly, follow the steps in the following topics to fix LIM problems:

   - [LIM dies quietly](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_admin/troubleshooting_common_problems_lsf.html?view=kc#srhsryh)
   - [LIM communication times out](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_admin/troubleshooting_common_problems_lsf.html?view=kc#hjsryhnra)
   - [Master LIM is down](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_admin/troubleshooting_common_problems_lsf.html?view=kc#rshnjyrsnjh)

2. Check whether services are registered properly.

## Avoiding orphaned job processes

LSF uses process groups to track all the processes of a job. However, if the application forks a child, the child becomes a new process group. The parent dies immediately, and the child process group is orphaned from the parent process, and cannot be tracked.

### About this task

For more information about process tracking with Linux cgroups, see [Memory and swap limit enforcement based on Linux cgroup memory subsystem](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_admin/cgroup_mem_enforce9111.html?view=kc#cgroup_mem_enforce9111).

### Procedure

1. When a job is started, the application runs under the job RES or root process group.

2. If an application creates a new process group, and its parent process ID (PPID) still belongs to the job, PIM can track this new process group as part of the job.

   The only reliable way to not lose track of a process is to prevent it from using a new process group. Any process that daemonizes itself is lost when child processes are orphaned from the parent process group because it changes its process group right after it is detached.

## Host not used by LSF

The **mbatchd** daemon allows the **sbatchd** daemon to run only on the hosts that are listed in the Host section of the lsb.hosts file. If you configure an unknown host in the following configurations, **mbatchd** logs an error message: HostGroup or HostPartition sections of the lsb.hosts file, or as a HOSTS definition for a queue in the lsb.queues file.

### About this task

If you try to configure a host that is not listed in the Host section of the lsb.hosts file, the **mbatchd** daemon logs the following message.

```
mbatchd on host: LSB_CONFDIR/cluster1/configdir/file(line #): Host hostname is not used by lsbatch; ignored
```

If you start the **sbatchd** daemon on a host that is not known by the **mbatchd** daemon, **mbatchd** rejects the **sbatchd**. The **sbatchd** daemon logs the following message and exits.

```
This host is not used by lsbatch system.
```

### Procedure

- Add the unknown host to the list of hosts in the Host section of the lsb.hosts file.

- Start the LSF daemons on the new host.

- Run the following commands to reconfigure the cluster:

  `lsadmin reconfig`

  `badmin reconfig`

## UNKNOWN host type or model

A model or type UNKNOWN indicates that the host is down or the LIM on the host is down. You need to take immediate action to restart LIM on the UNKNOWN host.

### Procedure

1. Start the host.

2. Run the **lshosts** command to see which host has the UNKNOWN host type or model.

   ```
   lshosts
   HOST_NAME  type       model   cpuf   ncpus  maxmem   maxswp  server   RESOURCES 
   hostA   UNKNOWN      Ultra2   20.2       2    256M    710M      Yes   ()
   ```

3. Run the **lsadmin limstartup** command to start LIM on the host.

   ```
   lsadmin limstartup hostA
   Starting up LIM on <hostA> .... done
   ```

   If EGO is enabled in the LSF cluster, you can run the following command instead:

   ```
   egosh ego start lim hostA
   Starting up LIM on <hostA> .... done
   ```

   You can specify more than one host name to start LIM on multiple hosts. If you do not specify a host name, LIM is started on the host from which the command is submitted.

   To start LIM remotely on UNIX or Linux, you must be root or listed in the lsf.sudoers file (or the ego.sudoers file if EGO is enabled in the LSF cluster). You must be able to run the **rsh** command across all hosts without entering a password.

4. Wait a few seconds, then run the **lshosts** command again.

   The **lshosts** command displays a specific model or type for the host or DEFAULT. If you see DEFAULT, it means that automatic detection of host type or model failed, and the host type that is configured in the lsf.shared file cannot be found. LSF works on the host, but a DEFAULT model might be inefficient because of incorrect CPU factors. A DEFAULT type might also cause binary incompatibility because a job from a DEFAULT host type can be migrated to another DEFAULT host type.

## DEFAULT host type or model

If you see DEFAULT in **lim -t**, it means that automatic detection of host type or model failed, and the host type that is configured in the lsf.shared file cannot be found. LSF works on the host, but a DEFAULT model might be inefficient because of incorrect CPU factors. A DEFAULT type might also cause binary incompatibility because a job from a DEFAULT host type can be migrated to another DEFAULT host type.

### Procedure

1. Run the **lshosts** command to see which host has the DEFAULT host model or type.

   ```
   lshosts
   HOST_NAME     type    model     cpuf   ncpus  maxmem  maxswp   server  RESOURCES 
   hostA     DEFAULT  DEFAULT        1       2    256M   710M       Yes  ()
   ```

   If Model or Type are displayed as DEFAULT when you use the **lshosts** command and automatic host model and type detection is enabled, you can leave it as is or change it.

   If the host model is DEFAULT, LSF works correctly but the host has a CPU factor of 1, which might not make efficient use of the host model.

   If the host type is DEFAULT, there might be binary incompatibility. For example, if one host is Linux and another is AIX, but both hosts are set to type DEFAULT, jobs that are running on the Linux host might be migrated to the AIX host and vice versa, which might cause the job to file.

2. Run **lim -t** on the host whose type is DEFAULT:

   ```
   lim -t
   Host Type             : NTX64
   Host Architecture     : EM64T_1596
   Total NUMA Nodes      : 1
   Total Processors      : 2
   Total Cores           : 4
   Total Threads         : 2
   Matched Type          : NTX64
   Matched Architecture  : EM64T_3000
   Matched Model         : Intel_EM64T
   CPU Factor            : 60.0
   ```

   **Note**The value of HostType and Host Architecture.

3. Edit the lsf.shared file to configure the host type and host model for the host.

   1. In the HostType section, enter a new host type. Use the host type name that is detected with the **lim -t** command.

      ```
      Begin HostType
      TYPENAME 
      DEFAULT 
      CRAYJ
      NTX64
      ...
      End HostType
      ```

   2. In the HostModel section, enter the new host model with architecture and CPU factor. Use the architecture that is detected with the **lim -t** commmand. Add the host model to the end of the host model list. The limit for host model entries is 127. Lines commented out with # are not counted in the 127-line limit.

      ```
      Begin HostModel
      MODELNAME   CPUFACTOR     ARCHITECTURE # keyword
      Intel_EM64T      20             EM64T_1596
      End HostModel
      ```

4. Save changes to the lsf.shared file.

5. Run the **lsadmin reconfig** command to reconfigure LIM.

6. Wait a few seconds, and run the **lim -t** command again to check the type and model of the host.