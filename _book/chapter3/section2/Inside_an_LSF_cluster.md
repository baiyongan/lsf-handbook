# 3.2 LSF 细观

Learn about the various daemon processes that run on LSF hosts, LSF cluster communications paths, and how LSF tolerates host failure in the cluster.



**[LSF daemons and processes](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_foundations/lsf_host_processes_overview.html?view=kc)**
Multiple LSF processes run on each host in the cluster. The type and number of processes that are running depends on whether the host is a master host or a compute host.



**[LSF cluster communication paths](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_foundations/communication_paths_lsf.html?view=kc)**
Understand the communication paths between the LSFdaemons in the cluster.



**[Fault tolerance and automatic master host failover](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_foundations/failover_lsf_admin_perspective.html?view=kc)**
The robust architecture of LSF is designed with fault tolerance in mind. Every component in the system has a recovery operationso that vital components are monitored by another component and can automatically recover from a failure.



**[Security](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_foundations/security_lsf_overview.html?view=kc)**
Understand the LSF security model, authentication, and user roles.