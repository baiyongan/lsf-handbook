# License Scheduler modes

When you configure your installation of License Scheduler, you must choose which of project mode and cluster mode best suits your needs for each license you use. Both project mode and cluster mode can be configured in one installation, however, all different licenses that are required by a job must belong to the same mode.

- cluster mode

  Distributes license tokens to clusters, where LSF scheduling takes over.![img](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/license_scheduler/cluster_mode_ls.jpg)Cluster mode emphasizes high utilization of license tokens over other considerations such as ownership. License ownership and sharing can still be configured, but within each cluster instead of across multiple clusters. Preemption of jobs (and licenses) also occurs within each cluster instead of across clusters.License tokens are reused by LSF when a job finishes, without waiting for confirmation from **lmstat** or **rlmstat** that license tokens are available and reported in the next **blcollect** cycle. This results in higher license utilization for short jobs.Cluster mode was introduced in License Scheduler 8.0.

- project mode

  Distributes license token to projects configured across all clusters.![img](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/license_scheduler/proj_mode_ls.jpg)Project mode emphasizes ownership of license tokens by specific projects which span multiple clusters. When License Scheduler is running in project mode, License Scheduler checks demand from license owners across all LSF clusters before allocating license tokens in project mode. The process of collecting and evaluating demand for all projects in all clusters slows down each scheduling cycle. License tokens are distributed in the next scheduling cycle after **lmstat** or **rlmstat** confirms license token availability.Project mode was the only choice available before License Scheduler 8.0.

## Difference between cluster mode and project mode

The following figure illustrates license utilization in cluster mode for short jobs with the corresponding **lmstat** or **rlmstat** reporting times:

![img](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/license_scheduler/ls_cluster_mode_alloc.jpg)

In cluster mode, when one job finishes running, the next job gets its license immediately without having to wait for the next **lmstat** or **rlmstat** interval. For example, four jobs that require license 2 are able to run without waiting for **lmstat** or **rlmstat** to report token distribution.

The following figure illustrates license utilization in project mode for short jobs with the **lmstat** or **rlmstat** reporting times:

![img](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/license_scheduler/ls_project_mode_alloc.jpg)

In project mode, each job must wait for **lmstat** or **rlmstat** to report token distribution before it can get a license and start running. In this example, three jobs that require license 2 are able to start within the **lmstat** or **rlmstat** intervals illustrated.

## When to use cluster mode

Cluster mode is most appropriate for your needs if:

- Your primary goal is to maximize license use.
- Ownership of licenses is a secondary consideration.
- Many jobs are short relative to the **blcollect** cycle (60 seconds by default, set by **LM_STAT_INTERVAL**).

## When to use project mode

Project mode is most appropriate for your needs if the following applies:

- Your primary goal is to ensure ownership of the group.
- Maximizing license use is a secondary consideration.
- Most jobs are long relative to the **blcollect** cycle (60 seconds by default, set by **LM_STAT_INTERVAL**).