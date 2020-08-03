# Project mode optional settings

After you configure License Scheduler in project mode with projects or project groups, you can include some additional configuration that is not required, but can be useful.



## Active ownership

With ownership defined, projects with demand for licenses are able to reclaim licenses up to the assigned ownership share for the project. With active ownership enabled, ownership is expressed as a percent of the total ownership for active projects, and the actual ownership for each project decreases as more projects become active. Active ownership allows ownership to automatically adjust based on project activity.

Active ownership can be used with projects, groups of projects, and project groups. Set percentage ownership values to total more than 100% to benefit from active ownership.

### Configure active ownership

#### About this task

When active ownership is enabled, ownership settings for inactive projects are disregarded during license token distribution.

#### Procedure

1. Set LS_ACTIVE_PERCENTAGE=Y in the Feature section.

   All ownership values for inactive projects are set to zero, and if the total ownership percent exceeds 100%, the total ownership is adjusted.

   LS_FEATURE_PERCENTAGE=Y is automatically set, and owned and non-shared values are expressed in percent. If used with project groups, **OWNERSHIP**, **LIMITS** and **NON_SHARED** are expressed in percent.

2. Set the percentage of owned licenses in the **DISTRIBUTION** parameter (Feature section) for a total percentage that exceeds 100%.

   ```
   ...
   DISTRIBUTION=wanserver (Lp1 2/50 Lp2 1/30 Lp3 2/30 Lp4 3/30)
   LS_ACTIVE_PERCENTAGE=Y
   ...
   ```

   In this example, all four license projects are configured with a share and an owned value. Lp1 has the greatest number of owned licenses, and can use preemption to reclaim the most licenses.

   If only Lp1 is active, Lp1 owns 50% of licenses. Total active ownership is 50%, so no adjustment is made.

   If Lp1 and Lp2 are active, Lp1 owns 50% and Lp2 owns 30%. Total active ownership is 80%, so no adjustment is made.

   If Lp1, Lp2, and Lp3 are active, Lp1 owns 50%, Lp2 owns 30%, and Lp3 owns 30%. Total active ownership is 110%, so ownership is scaled to result in Lp1 owning 46%, Lp2 owning 27%, and Lp3 owning 27% (Exact numbers are rounded).

   If all projects are active, the total active ownership is 140%. Ownership is scaled to result in Lp1 owning 37%, Lp2 owning 21%, Lp3 owning 21%, and Lp4 owning 21% (Exact numbers are rounded).

## Default projects

Jobs requiring a license feature but not submitted to a license project for that feature are submitted to the default project. For jobs to run, a share of license tokens must be assigned to the default project.

If you do not want the default project to get shares of license tokens, you do not have to define a default project in the distribution policy for a feature, however jobs in the default project become pending by default.

To avoid having jobs that are submitted without a project pend, either assign shares to the default project, or disable default projects so jobs are rejected.

### Configure default project shares

#### About this task

Jobs cannot run in the default project unless shares are assigned.

#### Procedure

Define a **default** project in the Feature section **DISTRIBUTION** parameter.

Any job that is submitted without a project name that is specified by -Lp can now use tokens from the **default** project.

### Disable default projects

#### About this task

License token jobs that are submitted without a project that is specified are accepted and assigned to the default project, unless your configuration specifies that such jobs be rejected.

#### Procedure

Optionally, set LSF_LIC_SCHED_STRICT_PROJECT_NAME=y in lsf.conf.

Jobs that are submitted without a project that is specified are rejected, and the default license project is not used.

## Groups of projects

If you configure groups of projects, you can set shares and ownership for each group and distribute license features to groups of projects. Configure a license project to belong only to one group. Preemption first occurs between groups of projects, and then occurs between projects.

### Preemption with groups of projects

The following tables show changes in preemption behavior that is based on ownership that is configured for groups of projects, with a total of 20 licenses. With groups of projects that are configured, GroupA is able to preempt to reclaim 10 owned licenses. Since Lp2 is not using all five owned licenses, Lp1 can use more than the share it owns.

### Project license ownership only

------

| License project | Licenses owned | Licenses used |
| :-------------- | :------------- | :------------ |
| Lp1             | 5              | 6             |
| Lp2             | 5              | 0             |
| Lp3             | 5              | 7             |
| Lp4             | 5              | 7             |

------

### Groups of projects with license ownership

------

| Group  | License projects | Project licenses owned | Licenses that are used after preemptions |
| :----- | :--------------- | :--------------------- | :--------------------------------------- |
| GroupA | Lp1Lp2           | 55                     | 91                                       |
| GroupB | Lp3Lp4           | 55                     | 64                                       |

------

### Configure group license ownership

#### Procedure

In lsf.licensescheduler, set the **GROUP** parameter in the Feature section.

1. Set up groups and members.

```
Begin Feature 
NAME = AppY 
DISTRIBUTION = LanServer1(Lp1 5/5 Lp2 5/5 Lp3 5/5 Lp4 5/5) 
GROUP = GroupA(Lp1 Lp2) GroupB (Lp3 Lp4) 
End Feature
```

In this example, Lp1 and Lp2 belong to the group GroupA. Lp3 and Lp4 belong to the GroupB group.

## Configure interactive (taskman) jobs

### About this task

By default, interactive (**taskman**) jobs do not receive a share of the license token allocation, while all clusters receive equal shares.

You can allocate a share of all license features to interactive jobs in the Parameters section.

### Procedure

To globally enable a share of the licenses for interactive tasks, you must set the ENABLE_INTERACTIVE in lsf.licensescheduler.

In lsf.licensescheduler, edit the Parameters section:

```
Begin Parameters
...
ENABLE_INTERACTIVE = y
...
End Parameters
```

When the change in configuration takes effect, interactive tasks are allocated the same share (by default) as each cluster.

## Configure cluster and interactive allocations

### About this task

By default in project mode, each cluster receives one allocation share from a license feature, and interactive tasks receive no shares.

You can modify the allocation of license shares across clusters and to interactive tasks in individual Feature sections.

### Procedure

In the Features section of lsf.licensescheduler, set the **ALLOCATION** parameter.

ALLOCATION=project_name (cluster_name [number_shares] ... )

### Allocation examples

For example, this **ALLOCATION** setting matches the default when **ALLOCATION** is undefined and interactive jobs are enabled with ENABLE_INTERACTIVE=Y. An equal share is allocated to each cluster and to interactive jobs.

```
Begin Feature
NAME = AppX
DISTRIBUTION = LanServer1 (Lp1 1)
ALLOCATION = Lp1 (Cluster1 1 Cluster2 1 interactive 1)
End Feature
```

In this example, licenses are shared equally between cluster1 and interactive tasks, with cluster2 receiving nothing:

```
Begin Parameters
...
ENABLE_INTERACTIVE = y
...
End Parameters
Begin Feature
NAME = AppY
DISTRIBUTION = LanServer (Lp1 1)
ALLOCATION = Lp1(cluster1 2 cluster2 0 interactive 2)
End Feature
```

In the following example, even though the global allocation to interactive jobs is disabled (ENABLE_INTERACTIVE = N), **ALLOCATION** defined in the Feature section can assign a share to interactive jobs for this license feature.

```
Begin Feature
NAME = AppZ
DISTRIBUTION = LanServer (Lp1 1)
ALLOCATION = Lp1(cluster1 0 cluster2 1 interactive 2)
End Feature
```

Given a total of 12 licenses, 4 are allocated to cluster2 and 8 are allocated to interactive tasks.

## Configure feature groups

### About this task

Feature groups that are configured in one FeatureGroup section allow you to view the information for multiple features, which are grouped together.

### Procedure

In lsf.licensescheduler, configure a FeatureGroup section, listing the license features associated with that license.

- Each FeatureGroup section must have a unique name.
- The feature names in **FEATURE_LIST** must already be defined in Feature sections.
- **FEATURE_LIST** cannot be empty or contain duplicate feature names.
- Features can be in more than one FeatureGroup section.

```
Begin FeatureGroup
NAME = Corporate
FEATURE_LIST = ASTRO VCS_Runtime_Net Hsim Hspice
End FeatureGroup
 
Begin FeatureGroup
NAME = Offsite
FEATURE_LIST = Encounter NCSim  NCVerilog
End FeatureGroup
```

## Restart to implement configuration changes

### About this task

Changes that are made in lsf.licensescheduler require restarting the **bld**.

Changes that are made in lsf.conf require restating the LSF clusters.

### Procedure

1. Run badmin mbdrestart to restart each LSF cluster.
2. Run lsadmin limrestart or bladmin reconfig to restart the **bld**.

## View license feature group information

### About this task

When **FEATURE_LIST** is configured for a group of license features in lsf.licensescheduler, you can view detailed information about the groups.

### Procedure

Run **blinfo -g** or **blstat -g**.

For example, if the feature group called **myFeatureGroup1** has the members **feature2** and **feature3**:

blstat -g "myFeatureGroup1"

Information displays for **feature2** and **feature3** in descending alphabetical order.

Run **blstat -g** alone or with options **-Lp**, **-t**, **-D** ,-**G**, **-s**.

Run **blinfo -g** alone or with options **-a,** **-t**, **-C**, and **-A**.

## License feature locality

Use license feature locality to limit features from different service domains to a specific cluster so that License Scheduler does not grant tokens to jobs from license that legally cannot be used on the cluster that is requesting the token.

### How locality works

Setting locality means that license resources requested from different clusters are mapped to different tokens in License Scheduler

Features with different locality are treated as different tokens by License Scheduler. You must configure separate feature sections for same feature with different localities.

**Note**You must make sure that your features are configured so that the applications always first try to check out licenses locally.

When License Scheduler receives license requests from LSF, it knows where the request is from, and it interprets the request into demands for tokens usable by that cluster. For example, if clusterA sends a request to the **bld** asking for one **hspice** license, License Scheduler marks the demand for both hspice@clusterA and **hspice**. When the job gets either token to run, the demand is cleaned up for both tokens.

### Configure locality

#### About this task

Specify LOCAL_TO to limit features from different service domains to specific clusters, so License Scheduler grants tokens of a feature only to jobs from clusters that are entitled to them.

For example, if your license servers restrict the serving of license tokens to specific geographical locations, use LOCAL_TO to specify the locality of a license token if any feature cannot be shared across all the locations. This specification avoids having to define different distribution and allocation policies for different service domains, and allows hierarchical group configurations.

License Scheduler manages features with different localities as different resources.

#### Procedure

1. In lsf.licensescheduler’s Feature section, configure LOCAL_TO.

   For example: LOCAL_TO=Site1(clusterA clusterB) configures the feature for more than one cluster, where the cluster names are already defined in the Clusters section of lsf.licensescheduler.

   LOCAL_TO=clusterA configures locality for only one cluster. This is the same as LOCAL_TO=clusterA(clusterA).

   License Scheduler now treats license features that are served to different locations as different token names, and distributes the tokens to projects according to the distribution and allocation policies for the feature.

2. (Optional) View locality settings.

   1. Run blinfo -A.

      The feature allocation by cluster locality displays.

      ```
      FEATURE          PROJECT   ALLOCATION
      hspice           Lp1       [clusterA, 25.0%] [clusterB, 25.0%]
                                 [clusterC, 25.0%] [interactive, 25.0%]
                       Lp2       [clusterA, 50.0%] [clusterB, 50.0%]
      hspice@clusterA  Lp1       [clusterA, 100.0%]
                       Lp2       [clusterA, 100.0%]
      hspice@siteB     Lp1       [clusterB, 80.0%] [clusterC, 20%]
                       Lp2       [clusterB, 80.0%] [clusterC, 20%]
      hspice@clusterC  Lp1       [clusterC, 60.0%] [interactive, 40.0%]
                       Lp2       [clusterC, 60.0%] [interactive, 40.0%]
                       Lp3       [clusterC, 60.0%] [interactive, 40.0%]
      vcs              Lp1       [clusterA, 33.0%] [clusterB, 33.0%]
                                 [interactive, 33.0%]
                       Lp2       [clusterA, 50.0%] [clusterB, 50.0%]
      vcs@clusterA     Lp1       [clusterA, 100.0%]
                       Lp2       [clusterA, 100.0%]
      vcs@siteB        Lp1       [clusterB, 80.0%] [clusterC, 20%]
                       Lp2       [clusterB, 80.0%] [clusterC, 20%]
      vcs@clusterC     Lp1       [clusterC, 60.0%] [interactive, 40.0%]
                       Lp2       [clusterC, 60.0%] [interactive, 40.0%]
                       Lp3       [clusterC, 60.0%] [interactive, 40.0%]
      ```

   2. Run blinfo -C.

      The cluster locality information for the features displays.

      ```
      NAME: hspice     LM_LICENSE_NAME: hspice
       CLUSTER_NAME    FEATURE          SERVICE_DOMAINS
       clusterA        hspice           SD3 SD4
                       hspice@clusterA  SD1
       clusterB        hspice           SD3 SD4
                       hspice@siteB     SD3
       clusterC        hspice           SD3 SD4
                       hspice@siteB     SD3
                       hspice@clusterC  SD5
       
      NAME: vcs        LM_LICENSE_NAME: VCS_Runtime
       CLUSTER_NAME    FEATURE          SERVICE_DOMAINS
       clusterA        vcs              SD3 SD4
                       vcs@clusterA     SD1
       clusterB        vcs              SD3 SD4
                       vcs@siteB        SD3
       clusterC        vcs              SD3 SD4
                       vcs@siteB        SD3
                       vcs@clusterC     SD5
      ```

   3. Run blusers.

      ```
      FEATURE          SERVICE_DOMAIN  USER     HOST       NLICS    NTASKS
      hspice@clusterA  SD1             user1    host1      1        1
      hspice@siteB     SD2             user2    host2      1        1
      ```

   4. Run blstat.

      ```
      FEATURE: hspice
       SERVICE_DOMAIN: SD3 SD4
       TOTAL_INUSE: 0    TOTAL_RESERVE: 0    TOTAL_FREE: 22   OTHERS: 0
       PROJECT                 SHARE   OWN  INUSE RESERVE FREE   DEMAND 
       Lp1                    50.0 %   0     0    0      11       0
       Lp2                    50.0 %   0     0    0      11       0
      FEATURE: hspice@clusterA
       SERVICE_DOMAIN: SD1
       TOTAL_INUSE: 0    TOTAL_RESERVE: 0    TOTAL_FREE: 25   OTHERS: 0
       PROJECT                 SHARE   OWN  INUSE RESERVE FREE   DEMAND 
       Lp1                    50.0 %   0     0    0      12       0
       Lp2                    50.0 %   0     0    0      13       0
       
      FEATURE: hspice@siteB
       SERVICE_DOMAIN: SD2
       TOTAL_INUSE: 0    TOTAL_RESERVE: 0    TOTAL_FREE: 65   OTHERS: 0
       PROJECT                 SHARE   OWN  INUSE RESERVE FREE   DEMAND 
       Lp1                    50.0 %   0     0    0      32       0
       Lp2                    50.0 %   0     0    0      33       0
      ```

   5. Run bhosts -s.

      Different resource information displays depending on the cluster locality of the features.

      From clusterA:

      ```
      RESOURCE                 TOTAL       RESERVED       LOCATION
      hspice                   36.0        0.0            host1
      ```

      From clusterB in siteB:

      ```
      RESOURCE                 TOTAL       RESERVED       LOCATION
      hspice                   76.0        0.0            host2
      ```

#### Example configuration: two sites and four service domains

Some of your service domains may have geographical restrictions when the domains are serving licenses. In this example, two clusters in one location can run **hspice** jobs. and four service domains are defined for the **hspice** feature:

- SD1 is a local license file for clusterA with 25 **hspice** licenses
- SD2 is a local license file for clusterB with 65 **hspice** licenses
- SD3 is a WANable license with 15 **hspice** licenses
- SD4 is a globally WANable license with seven **hspice** licenses

The geographical license checkout restrictions are:

- Jobs in clusterA can check out licenses from SD1 SD3 and SD4 but not SD2
- Jobs in clusterB can check out licenses from SD2 SD3 and SD4 but not SD1

```
Begin Feature
NAME = hspice
DISTRIBUTION = SD1 (Lp1 1 Lp2 1)
LOCAL_TO = clusterA
End Feature

Begin Feature
NAME = hspice
DISTRIBUTION = SD2 (Lp1 1 Lp2 1)
LOCAL_TO = clusterB
End Feature

Begin Feature
NAME = hspice
DISTRIBUTION = SD3 (Lp1 1 Lp2 1) SD4 (Lp1 1 Lp2 1)
End Feature
```

Or use the hierarchical group configuration (GROUP_DISTRIBUTION):

```
Begin Feature
NAME = hspice
GROUP_DISTRIBUTION = group1
SERVICE_DOMAINS = SD1
LOCAL_TO = clusterA
End Feature

Begin Feature
NAME = hspice
GROUP_DISTRIBUTION = group1
SERVICE_DOMAINS = SD2
LOCAL_TO = clusterB
End Feature

Begin Feature
NAME = hspice
GROUP_DISTRIBUTION = group1
SERVICE_DOMAINS = SD3 SD4
End Feature
```

### Submit jobs that use locality

#### Before you begin

**LOCAL_TO** is configured in lsf.licensescheduler.

#### About this task

Job submission is simplified when locality is configured.

#### Procedure

Specify the resource usage string with the same resource name you see in **bhosts -s**.

No OR rusage string is needed.

For example:

bsub -Lp Lp1 -R "rusage[hspice=1]" myjob

### How locality works with other settings

The following table shows various combinations of **LOCAL_TO** and other feature section parameters:

------

|      | **NAME** | **LM_LICENSE_NAME** |
| :--- | :------- | :------------------ |
| 1    | AppX     | -                   |
| 2    | AppZ201  | 201-AppZ            |
| 3    | AppB_v1  | AppB                |

------

1. You can define different License Scheduler tokens for the same FlexNet feature. The service domain names (in either the **DISTRIBUTION** line or the **SERVICE_DOMAINS** for group configurations) of the same FlexNet feature in different feature sections must be exclusive. They cannot overlap.
2. When **LOCAL_TO** is configured for a feature, you can define different License Scheduler tokens for the same FlexNet feature with different localities. The constraints are:
   - For the same FlexNet feature, service domains must be exclusive.
   - The location name of **LOCAL_TO** defines the locality of that feature, so the name must be unique for all tokens with same FlexNet feature.
   - Use same location name for different FlexNet features with the same pattern of locality, but License Scheduler does not check whether the same location name of a different feature contains the same list of clusters.
3. Features must either have a different **NAME** or have **LOCAL_TO** defined. The service domains for each License Scheduler token of same FlexNet feature must be exclusive.

#### How locality works with ALLOCATION and ENABLE_INTERACTIVE

The **LOCAL_TO** parameter simplifies the **ALLOCATION** configuration. Most of the time you are only interested in who can participate to share a particular token. **LOCAL_TO** gives the equal share for all the clusters that are defined in **LOCAL_TO** and applies to all the projects. Use **ALLOCATION** to fine-tune the shares for individual projects between different clusters:

- Except for the keyword interactive, all the cluster names that are defined in **ALLOCATION** must also be defined in the **LOCAL_TO** parameter.
- The global parameter **ENABLE_INTERACTIVE** and **ALLOCATION** with interactive share defined works same as before. If **ALLOCATION** is configured, it ignores the global setting of the **ENABLE_INTERACTIVE** parameter.
- If **ALLOCATION** is not defined, but **LOCAL_TO** is defined, the default value for **ALLOCATION** is equal shares for all the clusters defined in **LOCAL_TO** parameter. This share applies to all license projects defined in **DISTRIBUTION** or **GROUP_DISTRIBUTION**.
- If both **ALLOCATION** and **LOCAL_TO** are defined, **ALLOCATION** parameter can be used to fine-tune the shares between the clusters for different projects.

The following table shows example configurations with two clusters and 12 **hspice** licenses distributed as follows:

```
DISTRIBUTION = LanServer (Lp1 1 Lp2 1) 
```

------

| **ENABLE_INTERACTIVE** | **LOCAL_TO**                | **ALLOCATION**                 |
| :--------------------- | :-------------------------- | :----------------------------- |
| No                     | SiteA(clusterA interactive) | -                              |
| No                     | clusterA                    | Lp1(clusterA 1 clusterB 0)     |
| No                     | clusterA                    | Lp1(clusterA 1)Lp2(clusterA 1) |

------

#### About interactive taskman jobs

The License Scheduler command **taskman** is a job starter for **taskman** jobs to use License Scheduler without **bsub**. **taskman** checks out a license token and manages interactive UNIX applications.

You can use the logical AND operator (:) to combine rusage strings and the logical OR operator (||) to separate rusage string siblings. For example:

```
taskman -Lp P1 -R "rusage[f1=1:f2=1||f1=5:f3=1||f4=1]" myjob
```

If you specify multiple rusage string siblings, LSF License Scheduler checks each of the rusage string siblings from left to right. If at least one of the rusage string sibling requirements are met, the task can start. If none of the rusage string sibling requirements are met, LSF License Scheduler sends the DEMAND of all the unsatisfied rusage string siblings.

If a particular unsatisfied resource is specified in multiple rusage string siblings, only the highest value for DEMAND is sent. For example:

```
taskman -Lp P1 -R "rusage[f1=1:f2=2||f1=3:f2=1]" myjob
```

The f1 resource requirement is 1 for the first rusage string sibling and 3 for the second rusage string sibling. If the f1 resource is not satisfied, the demand of f1 is 3, not 3+1. This task will not start until at least one of the requirements of the rusage string siblings is met.

If **LOCAL_TO** is specified for a feature, **taskman** jobs must specify feature names with locality information similar to submission with **bsub**. You must know which token can be used from the location where task is going to run. For example:

```
taskman -Lp P1 -R "rusage[hspice@siteB=1]" myjob
taskman -Lp P1 -R "rusage[hspice=1]" myjob
taskman -Lp P1 -R "rusage[hspice@clusterA=1]" myjob
```