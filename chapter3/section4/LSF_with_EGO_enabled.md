# 3.4 启用 EGO 的 LSF

Enable the enterprise grid orchestrator (EGO) with LSF to provide a system infrastructure to control and manage cluster resources. Resources are physical and logical entities that are used by applications. LSF resources are shared as defined in the EGO resource distribution plan.

**[EGO component overview](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_foundations/ego_component_overview_lsf.html?view=kc)**
EGO can be enabled with LSF to provide a system infrastructure to control and manage cluster resources.

**[Resources](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_foundations/resources_overview.html?view=kc)**
Resources are physical and logical entities that are used by applications to run. While resource is a generic term, and can include low-level things such as shared memory segments or semaphores. In LSF, EGO manages CPU slots.

**[How LSF shares resources through EGO](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_foundations/resources_how_ego_gives_to_lsf_overview.html?view=kc)**
LSF resources can be shared by defining an EGO resource distribution plan. LSF requests resources from the EGO resource manager. Based on the values specified in the resource distribution plan, the resource manager returns the number of available slots (m) and the names of the hosts on which the slots reside.