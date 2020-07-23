# Differences between LSF License Scheduler editions

LSF License Scheduler is available in two editions: Basic Edition and Standard Edition.

LSF License Scheduler Basic Edition is included with LSF Standard Edition and Advanced Edition, and is not intended to apply policies on how licenses are shared between clusters or projects. Rather, LSF License Scheduler Basic Edition is intended to replace an external load information manager (**elim**) to collect external load indicies for licenses managed by FlexNet or Reprise License Manager. To replace this **elim**, LSF License Scheduler Basic Edition limits the license use of jobs of a single cluster to prevent overuse of the licenses and tracks license use of individual jobs by matching license checkouts to these jobs.

LSF License Scheduler LSF License Schedulerfunctionality, including support for all modes (cluster mode, project mode, and fast dispatch project mode), multiple clusters, features and feature groups, multiple service domains per license feature.LSF License Scheduler      LSF Advanced Edition

**Important**A LSF License Scheduler entitlement file (ls.entitlement) is now required to run LSF License Scheduler Standard Edition. Copy the entitlement file (ls.entitlement) to the $LSF_ENVDIR directory before starting LSF License Scheduler to run as Standard Edition.

To install and run LSF License Scheduler Basic Edition, download and install the LSF License Scheduler packages as described in [Install License Scheduler](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/license_scheduler/install_ls.html?view=kc#v2358429), but follow any specific steps for installing and configuring LSF License Scheduler Basic Edition instead of Standard Edition.

LSF License Scheduler Standard Edition is assumed in all LSF License Scheduler documentation unless it is explicitly stated as describing LSF License Scheduler Basic Edition.

**Parent topic:**

[Introduction](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/license_scheduler/chap_introduction.html?view=kc)