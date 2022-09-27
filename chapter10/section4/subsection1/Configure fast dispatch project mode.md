# Configure fast dispatch project mode

Use fast dispatch project mode to increase license utilization for project licenses. Fast dispatch project mode has the scheduling performance of cluster mode with the functionality of project mode, and is most appropriate for your needs if:

- Your primary goals are to maximize license use and ensure ownership of groups
- Most jobs are short relative to the **blcollect** cycle (60 seconds by default, set by **LM_STAT_INTERVAL**).

In fast dispatch project mode, LSF License Scheduler does not have to run the FlexNet command **lmstat** (or **lmutil)** or the Reprise License Manager command **rlmutil** (or **rlmstat**) to verify that a license is free before each job dispatch. As soon as a job finishes, the cluster can reuse its licenses for another job of the same project, which keeps gaps between jobs small. However, because LSF License Scheduler does not run **lmutil**, **lmstat**, **rlmutil**, or **rlmstat** to verify that the license is free, there is an increased chance of a license checkout failure for jobs if the license is already in use by a job in another project.

## Hierarchical project group paths

By default, hierarchical project groups in fast dispatch project mode are the same as hierarchical project groups in project mode. Fast dispatch project mode also supports the use of hierarchical project group paths, which helps LSF License Scheduler dispatch more jobs in fast dispatch project mode. To use hierarchical project group paths, you need LSF, Version 9.1.1, or later.

The following hierarchical group structure illustrates hierarchical project group paths:

![Hierarchical project groups with project group paths enabled for fast dispatch project mode](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/license_scheduler/licgrp2.jpg)

Enabling hierarchical project group paths enables the following:

- Features can use hierarchical project groups with project and project group names that are not unique, as long as the projects or project groups do not have the same parent. That is, you can define projects and project groups in more than one hierarchical project group.

  For example, the p4 project can be defined for project groups g4 and g6, each with its specific resource allocation within the project groups.

  **Note**Do not define a project group as a child of itself, because this results in a loop. For example, if project group g3 is a child of project group g1, do not define project g1 as a child of g3, as this will result in a loop of g1 and g3 being child project groups of one another.

- When specifying

   

  -Lp

   

  license_project

  , you can use paths to describe the project hierarchy without specifying the root group.

  For example, if you have topgrp as your root group, which has a child project group named g1 with a child project group named g3, which has a project named p1, you can use -Lp /g1/g3/p1 to specify this project.

- Hierarchical project groups have a default project named

   

  others

   

  with a default share value of 0. Any projects that do not match the defined projects in a project group are assigned into the

   

  others

   

  project. If the

   

  others

   

  project has a share value of 0, this project can still use licenses if the defined projects with shares are not using the licenses. Therefore, by default, the

   

  others

   

  project has the lowest priority within a project group.

  For example, if you have topgrp as your root group, which has a child project group named g1 with a child project group named g3, which has a project named p1, if you specify -Lp /g1/g3/project3 (which does not match a project), the effective license project is /g1/g3/others project. Similarly, specifying -Lp /g1/g3/gA/gB/gC/project3 results in an effective license project of /g1/g3/others because there are no subsequent child project groups under /g1/g3.

  If there is already a project named others, the preexisting others project specification overrides the default project.

Defining hierarchical project groups for fast dispatch project mode is the same as for project mode, allowing for project and project group names that are not unique.

For example, to define the previously-illustrated hierarchical project group in lsf.licensescheduler:

```
Begin ProjectGroup
GROUP              SHARES  OWNERSHIP LIMITS NON_SHARED
(topgrp (g1 g2)    (1 1)   ()        ()     ()
(g1 (g3 g4 others) (1 1 1) ()        ()     ()
(g2 (g5 g6)        (1 2)   ()        ()     ()
(g3 (p1 p2 others) (2 2 1) ()        ()     ()
(g4 (p3 p4)        (2 1)   ()        ()     ()
(g5 (p5 p1)        (1 3)   ()        ()     ()
(g6 (p6 p4)        (1 1)   ()        ()     ()
End ProjectGroup

Begin Feature
NAME=f1
GROUP_DISTRIBUTION=topgrp
SERVICE_DOMAINS=LanServer
End Feature
```

The others projects are explicitly defined for g1 and g3 (with a specific share), while the other project groups use the default others projects with 0 share.

The p1 project is defined for both g3 and g5, with a larger share if specified through the g5 project group. The p4 project is defined for both g4 and g6, with a larger share if specified through the g6 project group.

You can also specify different project groups with different root groups. Different features can use different root groups (as defined by the GROUP_DISTRIBUTION parameter), each with its own project group hierarchy and share policies.

When a job requests multiple features in fast dispatch project mode, LSF License Scheduler generates an effective license project for each feature. This means that it is possible for one job to have multiple effective license projects if the features use different project group hierarchies. LSF License Scheduler and LSF will calculate the effective license project for the feature based on its related project group hierarchy. The effective project is the path of the project resulting from the -Lp specification.

When specifying a project name without a hierarchical project group path in fast dispatch project mode with hierarchical group paths enabled, LSF License Scheduler uses the shortest path to the left that ends with the name of the project, as long as the cluster that submitted the job is authorized to use the selected project. If LSF License Scheduler cannot find such a project in the hierarchy, LSF License Scheduler uses the /others project.

For example, the following hierarchical group structure illustrates which clusters (c1 and c2) are authorized to use each project:

![Hierarchical project groups with authorized clusters](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/license_scheduler/licgrp3.jpg)

If you specify -Lp p2 from the c2 cluster (by submitting bsub -Lp p2 -R "rusage[f1=1]" myjob) without specifying a hierarchical group path, c2 is authorized to use /g2/p2 and /g2/g3/p2. The shortest path to the left that leads to p2 is /g2/p2, so the job is associated with the /g2/p2 hierarchical project.

- **[Configure lmremove or rlmremove preemption](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/license_scheduler/lmremove_preempt_config.html?view=kc)**
  Enable and configure **lmremove** (for FlexNet) or **rlmremove** (for Reprise License Manager) as a preemption action.

**Parent topic:**

[Configuring License Scheduler](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/license_scheduler/chap_config_ls.html?view=kc)

## Configure parameters

### Before you begin

Before configuring fast dispatch project mode, ensure that you enabled and configured project mode using projects or project groups. However, you can only specify one service domain per feature in fast dispatch project mode.

### Procedure

1. Fast dispatch project mode can be set globally, or for individual license features. Set individually when using fast dispatch project mode for some features and cluster mode or project mode for other features.

   1. If you are using fast dispatch project mode for all license features, define FAST_DISPATCH=Y in the Parameters section of lsf.licensescheduler.

   2. If you are using fast dispatch project mode for some license features, define FAST_DISPATCH=Y for individual license features in the Feature section of lsf.licensescheduler.

      The Feature section setting of **FAST_DISPATCH** overrides the global Parameter section setting.

2. Set the limit to which LSF License Scheduler considers the demand by each project in each cluster when allocating licenses.

   The default is 5.

   DEMAND_LIMIT=integer

   Define DEMAND_LIMIT in the Parameters section of lsf.licensescheduler to set the limit for all license features, or define DEMAND_LIMIT in the Feature section for individual license features. Setting in the Feature section overrides the global setting in the Parameters section.

   Periodically, each cluster sends a demand for each project. This is calculated in a cluster for a project by summing up the rusage of all jobs of the project pending due to lack of licenses. Whether to count a job's rusage in the demand depends on the job's pending reason. In general, the demand reported by a cluster only represents a potential demand from the project. It does not take into account other resources that are required to start a job. For example, a demand for 100 licenses is reported for a project. However, if LSF License Scheduler allocates 100 licenses to the project, the project does not necessarily use all 100 licenses due to slot available, limits, or other scheduling constraints.

   **mbatchd** in each cluster sends a demand for licenses from each project. In fast dispatch project mode, **DEMAND_LIMIT** limits the amount of demand from each project in each cluster that is considered when scheduling.

3. To enable hierarchical project group paths, define PROJECT_GROUP_PATH=Y in the Parameters section of lsf.licensescheduler.

   **Note**To use **PROJECT_GROUP_PATH**, you need LSF, Version 9.1.1, or later.

## Restart to implement configuration changes

### Procedure

1. Run bladmin reconfig to restart the bld.

2. If you deleted any Feature sections, restart mbatchd. In this case, a message is written to the log file, prompting the restart.

   If required, run badmin mbdrestart to restart each LSF cluster.

## View license allocation

### Procedure

Run blstat -c token_name to view information for a specific license token (as configured in a Feature section).

**blstat -c** output differs for fast dispatch project mode, project mode, and cluster mode.