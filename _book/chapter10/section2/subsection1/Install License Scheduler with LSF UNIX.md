# Install License Scheduler with LSF (UNIX)

## Before you begin

You must have write access to the LSF_TOP directories.

## Procedure

1. Log on as root to the installation file server host.

2. Download, uncompress, and extract the LSF License Scheduler packages for the platforms you need.

   For example, for x86 64-bit systems that run Linux kernel 2.6.x and compiled with glibc 2.3.x, download lsf10.1_licsched_lnx26-x64.tar.Z.

3. Extract the distribution file.

   For example:

   `# zcat lsf10.1_licsched_lnx26-x64.tar.Z | tar xvf -`

4. Change to the extracted distribution directory.

   For example:

   `# cd lsf10.1_licsched_linux2.6-glibc2.3-x86_64`

5. Run the **setup** script as root:

   `# ./setup`

   ##### **Note**

   If you are installing License Scheduler into a non-LSF environment or doing a silent install, edit ./setup.config prior to your installation.

6. Enter y (yes) to confirm that the path to lsf.conf is correct.

   To enter a path to a different lsf.conf, type n (no) and specify the full path to the lsf.conf file you want to use.

7. Enter y to confirm that the path to lsf.cluster.cluster_name is correct.

   To enter a path to a different lsf.cluster.cluster_name file, type n (no) and specify the full path to the lsf.cluster.cluster_name file you want to use.

8. Enter y to confirm that you want to use the LSF Administrators list for License Scheduler with LSF.

   To enter a different list of administrators for License Scheduler, enter a space-separated list of administrator user names. You can change your License Scheduler administrators list later, if necessary.

9. If you are installing LSF License Scheduler Standard Edition, copy the LSF License Scheduler entitlement file (ls.entitlement) to the $LSF_ENVDIR directory.

   If you do not copy the entitlement file to $LSF_ENVDIR before starting LSF License Scheduler, LSF License Scheduler runs as Basic Edition.

## What to do next

[Start License Scheduler](https://www.ibm.com/support/knowledgecenter/en/SSWRJV_10.1.0/license_scheduler/lic_sched_start.html?view=kc)

##### **Note**

Before starting LSF License Scheduler, if you are installing LSF License Scheduler Basic Edition, configure License Scheduler Basic Edition and LSF as described in [Configure License Scheduler Basic Edition ](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/license_scheduler/ls_edition_basic_config.html?view=kc#ls_edition_basic_config). If you are installing LSF License Scheduler Standard Edition, configure LSF License Scheduler Standard Edition and LSF as described in [Configuring License Scheduler](https://www.ibm.com/support/knowledgecenter/en/SSWRJV_10.1.0/license_scheduler/chap_config_ls.html?view=kc).