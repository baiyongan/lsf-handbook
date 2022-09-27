# 集群特征

在安装后找到集群的名称，集群管理员以及定义主机节点的位置。

## 集群名称与管理员

根据 **lsfinstall -f install.config** 命令指定的安装选项，以及在 install.config 文件中选择的选项安装集群。您在安装时指定的集群名称，是 LSF_CONFDIR/lsf.cluster.cluster_name 文件的名称的一部分。

```shell
/usr/share/lsf/lsf_10/conf/lsf.cluster.lsf_10
```

LSF_CONFDIR/lsf.cluster.cluster_name 文件的 ClusterAdmins 部分中列出了集群管理员。

## LSF 主机节点

- 在 LSF_CONFDIR/lsf.cluster.cluster_name 文件的 Hosts 部分中，列出了集群中安装的主机类型。
- LSF 主节点，是在 LSF_CONFDIR/lsf.cluster.cluster_name 文件的 Hosts 部分中配置的第一台主机。
- 集群中定义的 LSF 服务器主机，在 LSF_CONFDIR/lsf.cluster.cluster_name 文件的 Hosts 部分的 “Server” 列中用 1 表示。
- 在集群中定义的 LSF 仅客户端主机，在 LSF_CONFDIR/lsf.cluster.cluster_name 文件的 Hosts 部分的 “Server” 列中用 0 表示。

