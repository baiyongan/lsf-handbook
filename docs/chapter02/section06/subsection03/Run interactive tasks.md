# 运行交互式作业

如果可以找到所需的资源和适当的主机类型，则 **lsrun** 命令可以在当前本地主机或最佳可用主机上远程运行任务。 **lsgrun** 命令与 **lsrun** 命令类似，但是它在一组主机上运行任务。

以下命令运行 **ls** 命令。 在这种情况下，该命令在本地主机上通过 LSF 运行：

```shell
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

您还可以指定要在其中运行命令的主机。 例如，以下命令在远程主机 hosta 上运行 **hostname** 命令：

```shell
% lsrun -v -m hosta hostname
<<Execute hostname on remote host hosta>>
hosta
```

以下命令在三个远程主机上运行 **hostname** 命令：

```shell
% lsgrun -v -m "hosta hostb hostc" hostname
<<Executing hostname on hosta>>
hosta
<<Executing hostname on hostb>>
hostb
<<Executing hostname on hostc>>
hostc
```