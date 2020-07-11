# Run interactive tasks

The **lsrun** command runs a task on either the current local host or remotely on the best available host, provided it can find the necessary resources and the appropriate host type. The **lsgrun** command is similar to **lsrun**, but it runs a task on a group of hosts.

The following command runs the **ls** command. In this case, the command ran through LSF on the local host:

```
% lsrun ls -l /usr/share/lsf/cluster1/conf/
total 742
-rw-r--r--   1 root     lsf        11372 Jul 16 16:23 cshrc.lsf
-rw-r--r--   1 root     lsf          365 Oct 25 10:55 hosts
drwxr-xr-x   3 lsfadmin lsf          512 Jul 16 15:53 lsbatch
-rw-r--r--   1 lsfadmin lsf         1776 Nov 23 15:13 lsf.conf
-rw-r--r--   1 lsfadmin lsf         8453 Nov 16 17:46 lsf.shared
-rw-r--r--   1 lsfadmin lsf          578 Jul 16 15:53 lsf.task
-rw-r--r--   1 root     lsf        10485 Jul 16 17:08 profile.lsf
```

You can also specify a host where you want to run a command. For example, the following command runs the **hostname** command on the remote host hosta:

```
% lsrun -v -m hosta hostname
<<Execute hostname on remote host hosta>>
hosta
```

The following command runs the **hostname** command on three remote hosts:

```
% lsgrun -v -m "hosta hostb hostc" hostname
<<Executing hostname on hosta>>
hosta
<<Executing hostname on hostb>>
hostb
<<Executing hostname on hostc>>
hostc
```