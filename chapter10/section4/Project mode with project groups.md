# Project mode with project groups

Project groups use a ProjectGroup section to build a hierarchical project structure, which you can use to set limits on projects that span multiple clusters.

Depending on your license usage, you can configure different project groups for different license features, or reuse the same hierarchical structure.

Each license feature in project mode can either use projects or project groups. Changing from projects to project groups involves adding a ProjectGroup section and changing the license token distribution that is configured in the Feature section. Other configuration remains the same.

**Parent topic:**

[Configuring License Scheduler](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/license_scheduler/chap_config_ls.html?view=kc)

## Configuring project groups

### About this task

ProjectGroup sections use configured projects (each with a Projects section in the lsf.licensescheduler file) to form a hierarchical structure for each feature.

**Note**

The Feature section **GROUP** parameter is used to group projects together, simplifying configuration, and is not the same as a ProjectGroup section.

### Procedure

1. Add a ProjectGroup section to the lsf.licensescheduler file:

   ```
   Begin ProjectGroup
   GROUP     SHARES    OWNERSHIP   LIMITS     NON_SHARED
   End Projectgroup
   ```

   If LS_FEATURE_PERCENTAGE=Y or LS_ACTIVE_PERCENTAGE=Y in lsf.licensescheduler, values for **OWNERSHIP**, **LIMITS**, and **NON_SHARED** are expressed as a percentage of the total licenses, not as an absolute number.

2. For each branch in the hierarchy, add a line to the ProjectGroup section.

   1. Under the heading **GROUP**, indicate the project that branches, and direct descendants in the hierarchy (group(member ...)).
   2. Under the heading **SHARES**, set the integer share for each member project.
   3. Under the heading **OWNERSHIP**, set the integer ownership for each bottom-level group member (leaf node), with a dash (-) representing no ownership. The OWNERSHIP value must be greater than or equal to the NON_SHARED value.
   4. Under the heading **LIMITS** set the integer license limit for each member project, with a dash (-) representing unlimited. The LIMITS value must be greater than or equal to the OWNERSHIP value.
   5. Under the heading **NON_SHARED**, set the integer number of non-shared licenses each bottom-level group member (leaf node) uses exclusively, with ’-’ representing none.
   6. Optionally, under the heading **DESCRIPTION**, add a description up to 64 characters long, using a backslash (\) to extend to multiple lines.

   For example, the branch g4 splits into three members:

   ```
   GROUP                 SHARES    OWNERSHIP   LIMITS     NON_SHARED 
   (g4 (p4 p5 p6))       (1 1 1)   (1 1 1)     ()         (- 3 -) 
   ```

3. In the Feature section, set parameter **GROUP_DISTRIBUTION** to the top level of the ProjectGroup section hierarchy.

   The **DISTRIBUTION** parameter that is used for projects is no longer used.

4. In the Feature section, list service domains in the **SERVICE_DOMAINS** parameter.

   Unlike for projects, service domains are not included in the distribution for project groups.

### Project group examples

![img](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/license_scheduler/licgrp1.jpg)

This hierarchy is implemented by the project group configuration:

```
Begin ProjectGroup 
GROUP                 SHARES    OWNERSHIP   LIMITS     NON_SHARED 
(topgrp (g1 g2))      (1 1)     ()          (10 10)    ()
(g1 (g3 g4))          (1 1)     ()          (10 10)    ()
(g2 (g5 g6))          (1 1)     ()          (- 5)      ()
(g3 (p1 p2 p3))       (1 1 2)   ()          (3 4 5)    ()
(g4 (p4 p5 p6))       (1 1 1)   (1 3 1)     ()         (0 3 0) 
(g5 (p7 p8 p9))       (1 1 1)   (2 0 2)     ()         (1 0 1) 
(g6 (p10 p11 p12))    (1 1 1)   (2 2 2)     (4 4 4)    (1 0 1) 
End ProjectGroup 
```

License feature configuration that uses this project group:

```
Begin Feature 
NAME = AppZ 
GROUP_DISTRIBUTION = topgrp 
SERVICE_DOMAINS = LanServer WanServer 
End Feature
```

Use the **LIMITS** column to limit token use, so tokens are sometimes not distributed even if they are available. By default, License Scheduler distributes all available tokens if possible. For example, if total of six licenses are available:

```
Begin ProjectGroup
GROUP       SHARES OWNERSHIP LIMITS NON_SHARED 
(Root(A B)) (1 1)   ()        ()     () 
(A (c d))   (1 1)   ()        (1 1)  () 
(B (e f))   (1 1)   ()        ()     () 
End ProjectGroup
```

When there is no demand for license tokens, License Scheduler allocates only five tokens according to the distribution. License Scheduler gives three tokens to group A and three tokens to group B, but project c and project d are limited to one token each, so one token is not allocated within group A. As more demand comes in for project e and project f, the tokens that are not allocated are distributed to group B.

### Configuring preemption priority within project groups

#### About this task

The optional **PRIORITY** parameter in the ProjectGroup section, if defined, is used for preemption instead of basing preemption on the accumulated inuse for each project.

#### Procedure

Under the heading **PRIORITY**, set the integer priority for each group member, with ’0’ being the lowest priority.

**PRIORITY** can be set for all members in the project group hierarchy.

#### Example

For example:

```
Begin ProjectGroup
GROUP             SHARES   OWNERSHIP  LIMITS  NON_SHARED PRIORITY
(root(A B C))     (1 1 1)  ()         ()         ()      (3 2 -)
(A (P1 D))        (1 1)    ()         ()         ()      (3 5)
(B (P4 P5))       (1 1)    ()         ()         ()      ()
(C (P6 P7 P8))    (1 1 1)  ()         ()         ()      (8 3 -)
(D (P2 P3))       (1 1)    ()         ()         ()      (2 1)
End ProjectGroup
```

By default, priority is evaluated from top to bottom. The priority of any specific node is first decided by the priorities of its parent nodes. The values are only comparable between siblings.

The following figure illustrates the example configuration:

![img](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/license_scheduler/priority_tree.jpg)

The priority of each node is shown beside the node name. If priority is not defined, by default is set to 0 (nodes P4 and P5 under node B).

To find the highest priority leaf node in the tree, License Scheduler traverses the tree from root to node A to node D to project P2.

To find the lowest priority leaf node in the tree, License Scheduler traverses the tree from root to node C to project P8.

When two nodes have the same priority, for example, projects P4 and P5, priority is determined by accumulated inuse usage at the time the priorities are evaluated.

When a leaf node in branch A wants to preempt a token from branch B or C, branch C is picked because it has a lower priority than branch B.

### Viewing hierarchical configuration

#### Procedure

Use **blinfo -G** to view the hierarchical configuration:

For the previous example:

```
blinfo -G 
GROUP                 SHARES    OWNERSHIP   LIMITS     NON_SHARED  DESCRIPTION
(topgrp (g1 g2))      (1 1)     ()          (10 10)    ()          ()
(g1 (g3 g4))          (1 1)     ()          (10 10)    ()          ()
(g2 (g5 g6))          (1 1)     ()          (- 5)      ()          ()
(g3 (p1 p2 p3))       (1 1 2)   ()          (3 4 5)    ()          ()
(g4 (p4 p5 p6))       (1 1 1)   (1 3 1)     ()         (0 3 0)     ()
(g5 (p7 p8 p9))       (1 1 1)   (2 0 2)     ()         (1 0 1)     ()
(g6 (p10 p11 p12))    (1 1 1)   (2 2 2)     (4 4 4)    (1 0 1)     ()
```

### Viewing information about project groups

#### Procedure

Use **blstat -G** to view the hierarchical dynamic license information.

```
blstat -G
FEATURE: p1_f1 
SERVICE_DOMAINS: 
TOTAL_INUSE: 0    TOTAL_RESERVE: 0    TOTAL_FREE: 4    OTHERS: 0   
SHARE_INFO_FOR:  /topgrp  
GROUP/PROJECT           SHARE   OWN  INUSE RESERVE FREE   DEMAND    
g2                      100.0 % 0    0     0       4      0         
SHARE_INFO_FOR:  /topgrp/g2  
GROUP/PROJECT           SHARE   OWN  INUSE RESERVE FREE   DEMAND
p3                      50.0 %  0    0     0       2      0   
p4                      50.0 %  0    0     0       2      0 
FEATURE: p1_f2 
SERVICE_DOMAINS: 
TOTAL_INUSE: 0    TOTAL_RESERVE: 0    TOTAL_FREE: 4     OTHERS: 0   
SHARE_INFO_FOR:  /topgrp  
GROUP/PROJECT          SHARE   OWN  INUSE RESERVE FREE   DEMAND       
g2                     100.0 % 0    0     0       4      0    
SHARE_INFO_FOR:  /topgrp/g2  
GROUP/PROJECT          SHARE   OWN  INUSE RESERVE FREE   DEMAND       
p3                     50.0 %  0    0     0       2      0  
p4                     50.0 %  0    0     0       2      0
```