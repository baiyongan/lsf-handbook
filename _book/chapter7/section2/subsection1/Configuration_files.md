# Configuration files

LSF configuration files reference.

**Important**

Specify any domain names in all uppercase letters in all configuration files.

**[cshrc.lsf and profile.lsf](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_config_ref/cshrc.lsf.5.html?view=kc)**
The user environment shell files cshrc.lsf and profile.lsf set the LSF operating environment on an LSF host.**[hosts](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_config_ref/hosts.5.html?view=kc)**
For hosts with multiple IP addresses and different official host names configured at the system level, this file associates the host names and IP addresses in LSF.**[install.config](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_config_ref/install.config.5.html?view=kc)**
The install.config file contains options for LSF installation and configuration. Use the **lsfinstall -f install.config** command to install LSF with the options that are specified in the install.config file.**[lim.acct](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_config_ref/lim.acct.5.html?view=kc)**
The lim.acct file is the log file for the LSF Load Information Manager (LIM). Produced by the **lsmon** command, the lim.acct file contains host load information that is collected and distributed by LIM.**[lsb.acct](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_config_ref/lsb.acct.5.html?view=kc)**
The lsb.acct file is the batch job log file of LSF.**[lsb.applications](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_config_ref/lsb.applications.5.html?view=kc)**
The lsb.applications file defines application profiles. Use application profiles to define common parameters for the same type of jobs, including the execution requirements of the applications, the resources they require, and how they should be run and managed.**[lsb.events](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_config_ref/lsb.events.5.html?view=kc)**
The LSF batch event log file lsb.events is used to display LSF batch event history and for **mbatchd** failure recovery.**[lsb.globalpolicies](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_config_ref/lsb.globalpolicies.5.html?view=kc)**
This configuration file defines global policies for multiple clusters.**[lsb.hosts](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_config_ref/lsb.hosts.5.html?view=kc)**
**[lsb.modules](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_config_ref/lsb.modules.5.html?view=kc)**
The lsb.modules file contains configuration information for LSF scheduler and resource broker modules. The file contains only one section, named PluginModule.**[lsb.params](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_config_ref/lsb.params.5.html?view=kc)**
**[lsb.queues](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_config_ref/lsb.queues.5.html?view=kc)**
The lsb.queues file defines batch queues. Numerous controls are available at the queue level to allow cluster administrators to customize site policies.**[lsb.reasons](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_config_ref/lsb.reasons.5.html?view=kc)**
**[lsb.resources](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_config_ref/lsb.resources.5.html?view=kc)**
The lsb.resources file contains configuration information for resource allocation limits, exports, resource usage limits, and guarantee policies. This file is optional.**[lsb.serviceclasses](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_config_ref/lsb.serviceclasses.5.html?view=kc)**
**[lsb.threshold](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_config_ref/lsb.threshold.5.html?view=kc)**
The lsb.threshold configuration file defines energy-saving and CPU frequency policies. This file is optional.**[lsb.users](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_config_ref/lsb.users.5.html?view=kc)**
**[lsf.acct](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_config_ref/lsf.acct.5.html?view=kc)**
**[lsf.cluster](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_config_ref/lsf.cluster.5.html?view=kc)**
The cluster configuration file. There is one file for each cluster, called lsf.cluster.cluster_name. The cluster_name suffix is the name of the cluster defined in the Cluster section of the lsf.shared file. All LSF hosts are listed in this file, along with the list of LSF administrators and the installed LSF features.**[lsf.conf](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_config_ref/lsf.conf.5.html?view=kc)**
The lsf.conf file controls the operation of LSF. The lsf.conf file is created during installation and records all the settings chosen when LSF was installed. The lsf.conf file dictates the location of the specific configuration files and operation of individual servers and applications.**[lsf.datamanager](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_config_ref/lsf.datamanager.5.html?view=kc)**
The lsf.datamanager file controls the operation of IBM Spectrum LSF Data Manager features. Each cluster has one LSF data management configuration file, called lsf.datamanager.cluster_name. The cluster_name suffix is the name of the cluster that is defined in the Cluster section of the lsf.shared file. The file is read by the LSF data management daemon **dmd**. Since one LSF data manager can serve multiple LSF clusters, the contents of this file must be identical on each cluster that shares LSF data manager.**[lsf.licensescheduler](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_config_ref/lsf.licensescheduler.5.html?view=kc)**
The lsf.licensescheduler file contains LSF License Scheduler configuration information. All sections except ProjectGroup are required. In cluster mode, the Project section is also not required.**[lsf.shared](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_config_ref/lsf.shared.5.html?view=kc)**
The lsf.shared file contains common definitions that are shared by all load sharing clusters defined by lsf.cluster.cluster_name files.**[lsf.sudoers](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_config_ref/lsf.sudoers.5.html?view=kc)**
**[lsf.task](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_config_ref/lsf.task.5.html?view=kc)**
**[setup.config](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_config_ref/setup.config.5.html?view=kc)**
**[slave.config](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_config_ref/slave.config.5.html?view=kc)**
The slave.config file contains options for installing and configuring a server host that can be dynamically added or removed.