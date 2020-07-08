# 管理用户、节点与队列

Make your cluster available to users with cshrc.lsf and profile.lsf. Add or remove hosts and queues from your cluster.

**[Making your cluster available to users with cshrc.lsf and profile.lsf](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_admin_foundations/cshrc_profile_lsf.html?view=kc)**
Make sure that all LSF users include either the cshrc.lsf or profile.lsf file at the end of their own .cshrc or .profile file, or run one of these two files before you use LSF.**[Adding a host to your cluster](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_admin_foundations/add_hosts.html?view=kc)**
Use the LSF installation script **lsfinstall** to add new hosts and host types to your cluster.**[Removing a host from your cluster](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_admin_foundations/remove_hosts.html?view=kc)**
Removing a host from LSF involves closing a host to prevent any additional jobs from running on the host and removing references to the host from the lsf.cluster.cluster_name file and other configuration files.**[Adding a queue](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_admin/queue_add.html?view=kc)**
Edit the lsb.queues file to add the new queue definition. Adding a queue does not affect pending or running jobs.**[Removing a queue](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_admin/queue_remove.html?view=kc)**
Edit lsb.queues to remove a queue definition.