# 集群特征

Find the name of your cluster after installation, cluster administrators, and where hosts are defined.

## Cluster name and administrators

Your cluster is installed according to the installation options specified by the **lsfinstall -f install.config** command and the options you chose in the install.config file. The cluster name that you specified at installation is part of the name of the LSF_CONFDIR/lsf.cluster.cluster_name file.

```
/usr/share/lsf/lsf_10/conf/lsf.cluster.lsf_10
```

Cluster administrators are listed in the ClusterAdmins section of the LSF_CONFDIR/lsf.cluster.cluster_namefile.

## LSF hosts

- Host types that are installed in your cluster are listed in the Hosts section of theLSF_CONFDIR/lsf.cluster.cluster_name file.
- The LSF master host is the first host that is configured in the Hosts section ofLSF_CONFDIR/lsf.cluster.cluster_name file.
- LSF server hosts that are defined in your cluster are indicated by 1 in the server column of the Hosts section in theLSF_CONFDIR/lsf.cluster.cluster_name file.
- LSF client-only hosts that are defined in your cluster are indicated by 0 in the server column of the Hosts section in theLSF_CONFDIR/lsf.cluster.cluster_name file.

