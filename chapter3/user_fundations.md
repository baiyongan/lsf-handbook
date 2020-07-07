# Chapter 3 用户操作基础

Get an overview of IBM Spectrum LSF workload management concepts and operations.

**[IBM Spectrum LSF overview](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_foundations/chap_lsf_overview_foundations.html?view=kc)**
Learn how LSF takes your job requirements and finds the best resources to run the job.**[Inside an LSF cluster](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_foundations/chap_lsf_cluster.html?view=kc)**
Learn about the various daemon processes that run on LSF hosts, LSF cluster communications paths, and how LSF tolerates host failure in the cluster.

**[Inside workload management](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_foundations/chap_lsf_inside_workload_management.html?view=kc)**
Understand the LSF job lifecycle. Use the **bsub** to submit jobs to a queue and specify job submission options to modify the default job behavior. Submitted jobs wait in queues until they are scheduled and dispatched to a host for execution. At job dispatch, LSF checks to see which hosts are eligible to run the job.

**[LSF with EGO enabled](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_foundations/chap_lsf_ego_enabled.html?view=kc)**
Enable the enterprise grid orchestrator (EGO) with LSF to provide a system infrastructure to control and manage cluster resources. Resources are physical and logical entities that are used by applications. LSF resources are shared as defined in the EGO resource distribution plan.