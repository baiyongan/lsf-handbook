# 重要的文件目录与配置文件

LSF configuration is administered through several configuration files, which you use to modify the behavior of your cluster.

## Four important LSF configuration files

The following are the four most important files you work with most often:

- LSF_CONFDIR/lsf.conf
- LSF_CONFDIR/lsf.cluster.cluster_name
- LSF_CONFDIR/lsf.shared
- LSB_CONFDIR/cluster_name/configdir/lsb.queues

These files are created during product installation according to the options you specified in the install.config file. After installation, you can change the configuration parameters in these files to suit the needs of your site.

- Who owns these files

  Except for LSF_CONFDIR/lsf.conf, which is owned by root, all of these files are owned by the primary LSF administrator, and readable by all cluster users.

- lsf.conf

  The most important file in LSF. It contains the paths to the configuration directories, log directories, libraries, and other global configuration information. The location of the lsf.conf file is defined by the LSF_ENVDIR variable. If LSF cannot find this file, it cannot start properly.By default, LSF checks the directory that is defined by the **LSF_ENVDIR** parameter for the location of the lsf.conf file. If the lsf.conf file is not in **LSF_ENVDIR**, LSF looks for it in the /etc directory.

- lsf.cluster.cluster_name

  Defines the host names, models, and types of all of the hosts in the cluster. It also defines the user names of the LSF administrators, and the locations of different shared resources for one cluster.

- lsf.shared

  This file is like a dictionary that defines all the keywords that are used by the cluster. You can add your own keywords to specify the names of resources or host types.

- lsb.queues

  Defines the workload queues and their parameters for one cluster.

## LSF directories

The following directories are owned by the primary LSF administrator and are readable by all cluster users:

------

| Directory        | Description                                   | Example                               |
| :--------------- | :-------------------------------------------- | :------------------------------------ |
| **LSF_CONFDIR**  | LSF configuration directory                   | /usr/share/lsf/cluster1/conf/         |
| **LSB_CONFDIR**  | Batch system configuration directory          | /usr/share/lsf/cluster1/conf/lsbatch/ |
| **LSB_SHAREDIR** | Job history directory                         | /usr/share/lsf/cluster1/work/         |
| **LSF_LOGDIR**   | Server daemon error logs, one for each daemon | /usr/share/lsf/cluster1/log/          |

------

The following directories are owned by root and are readable by all cluster users:

------

| Directory          | Description                                                  | Example                                       |
| :----------------- | :----------------------------------------------------------- | :-------------------------------------------- |
| **LSF_BINDIR**     | LSF user commands, which are shared by all hosts of the same type | /usr/share/lsf/cluster1/10.1/sparc-sol10/bin/ |
| **LSF_INCLUDEDIR** | Header files lsf/lsf.h and lsf/lsbatch.h                     | /usr/share/lsf/cluster1/10.1/include/         |
| **LSF_LIBDIR**     | LSF libraries, which are shared by all hosts of the same type | /usr/share/lsf/cluster1/10.1/sparc-sol10/lib/ |
| **LSF_MANDIR**     | LSF man pages                                                | /usr/share/lsf/cluster1/10.1/man/             |
| **LSF_MISC**       | Examples and other miscellaneous files                       | /usr/share/lsf/cluster1/10.1/misc/            |
| **LSF_SERVERDIR**  | Server daemon binary files, scripts, and other utilities, which are shared by all hosts of the same type | /usr/share/lsf/cluster1/10.1/sparc-sol10/etc/ |
| **LSF_TOP**        | Top-level installation directory                             | /usr/share/lsf/cluster1/                      |

------

Other configuration directories can be specified in the LSF_CONFDIR/lsf.conf file.

## LSF cluster configuration files

The following files are owned by the primary LSF administrator and are readable by all cluster users:

------

| File                                                         | Example                                                      |
| :----------------------------------------------------------- | :----------------------------------------------------------- |
| Global configuration files, which describe the configuration and operation of the cluster | /usr/share/lsf/cluster1/conf/ego/cluster1/kernel/ego.conf/usr/share/lsf/cluster1/conf/lsf.conf |
| Keyword definition file that is shared by all clusters. Defines cluster name, host types, host models, and site-specific resources | /usr/share/lsf/cluster1/conf/lsf.shared                      |
| Cluster configuration file that defines hosts, administrators, and location of site-defined shared resources | /usr/share/lsf/cluster1/conf/lsf.cluster.cluster1            |
| Mapping files for task names and their default resource requirements | /usr/share/lsf/cluster1/conf/lsf.task/usr/share/lsf/cluster1/conf/lsf.task.cluster1 |

------

## LSF batch workload system configuration files

The following files are owned by the primary LSF administrator and are readable by all cluster users:

------

| File                                                         | Example                                                      |
| :----------------------------------------------------------- | :----------------------------------------------------------- |
| Server hosts and their attributes, such as scheduling load thresholds, dispatch windows, and job slot limits. If no hosts are defined in this file, then all LSF server hosts listed in LSF_CONFDIR/lsf.cluster.cluster_name are assumed to be LSF batch server hosts. | /usr/share/lsf/cluster1/conf/lsbatch/cluster1/configdir/lsb.hosts |
| LSF scheduler and resource broker plug-in modules. If no scheduler or resource broker modules are configured, LSF uses the default scheduler plug-in module named schmod_default. | /usr/share/lsf/cluster1/conf/lsbatch/cluster1/configdir/lsb.modules |
| LSF batch system parameter file                              | /usr/share/lsf/cluster1/conf/lsbatch/cluster1/configdir/lsb.params |
| Job queue definitions                                        | /usr/share/lsf/cluster1/conf/lsbatch/cluster1/configdir/lsb.queues |
| Resource allocation limits, exports, and resource usage limits. | /usr/share/lsf/cluster1/conf/lsbatch/cluster1/configdir/lsb.resources |
| LSF user groups, hierarchical fairshare for users and user groups, and job slot limits for users and user groups. Also used to configure account mappings for the LSF multicluster capability. | /usr/share/lsf/cluster1/conf/lsbatch/cluster1/configdir/lsb.users |
| Application profiles, which contain common parameters for the same type of jobs, including the execution requirements of the applications, the resources they require, and how they are run and managed. This file is optional. Use the **DEFAULT_APPLICATION** parameter in the lsb.params file to specify a default application profile for all jobs. LSF does not automatically assign a default application profile. | /usr/share/lsf/cluster1/conf/lsbatch/cluster1/configdir/lsb.applicatons |

------

## LSF batch log files

------

| File                 | Example                                                  |
| :------------------- | :------------------------------------------------------- |
| Batch events log     | /usr/share/lsf/cluster1/work/ cluster1/logdir/lsb.events |
| Batch accounting log | /usr/share/lsf/cluster1/work/ cluster1/logdir/lsb.acct   |

------

## Daemon log files

LSF server daemon log files are stored in the directory that is specified by LSF_LOGDIR in LSF_CONFDIR/lsf.conf.

------

| File                                  | Example                                        |
| :------------------------------------ | :--------------------------------------------- |
| Load information manager (**lim**)    | /usr/share/lsf/cluster1/log/lim.log.hosta      |
| Remote execution server (**res**)     | /usr/share/lsf/cluster1/log/res.log.hosta      |
| Master batch daemon (**mbatchd**)     | /usr/share/lsf/cluster1/log/ mbatchd.log.hosta |
| Master scheduler daemon (**mbschd**)  | /usr/share/lsf/cluster1/log/mbschd.log.hosta   |
| Slave batch daemon (**sbatchd**)      | /usr/share/lsf/cluster1/log/sbatchd.log.hosta  |
| Process information manager (**pim**) | /usr/share/lsf/cluster1/log/ pim.log.hosta     |

------

**Who owns and who should write to LSF_LOGDIR**

**Note**Make sure that the primary LSF administrator owns the LSF log directory (**LSF_LOGDIR** parameter), and that root can write to this directory. If an LSF server cannot write to **LSF_LOGDIR** parameter, the error logs are created in /tmp.

## Where to go next

Use your new IBM Spectrum LSF cluster, described in [Work with LSF](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_admin_foundations/working_lsf.html?view=kc).