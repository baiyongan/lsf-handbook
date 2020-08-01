# Project mode with projects

You can configure license distribution when you are running license projects in project mode. Each distribution policy is applied locally, within service domains.

**Tip**Although license projects are not the same as LSF projects, you can map your license project names to LSF project names for easier monitoring.

**Parent topic:**

[Configuring License Scheduler](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/license_scheduler/chap_config_ls.html?view=kc)

## Configure parameters

### Procedure

1. Project mode can be set globally, or for individual license features. Set individually when you are using project mode for some features and cluster mode for some features.

   1. If you are using project mode for all license features, define CLUSTER_MODE=N in the Parameters section of lsf.licensescheduler.

   2. If you are using project mode for some license features, define CLUSTER_MODE=N for individual license features in the Feature section of lsf.licensescheduler.

      The Feature section setting of **CLUSTER_MODE** overrides the global Parameter section setting.

2. List the License Scheduler hosts.

   By default with an LSF installation, the **HOSTS** parameter is set to the **LSF_MASTER_LIST**.

   - List the hosts in order from most preferred to least preferred. The first host is the master license scheduler host.
   - Specify a fully qualified host name such as hostX.mycompany.com unless all your License Scheduler clients run in the same DNS domain.

   HOSTS=host1 host2

3. Specify the data collection frequency between License Scheduler and the license manager.

   The default is 30 seconds.

   LM_STAT_INTERVAL=seconds

4. Specify the file paths to the commands for the license managers that you are using.

   1. If you are using FlexNet, specify the path to the FlexNet command **lmutil** (or **lmstat**).

      For example, if **lmstat** is in /etc/flexlm/bin:

      ```
      LMSTAT_PATH=/etc/flexlm/bin
      ```

   2. If you are using Reprise License Manager, specify the path to the Reprise License Manager command **rlmutil** (or **rlmstat**).

      For example, if **rlmstat** is in /etc/rlm/bin:

      ```
      RLMSTAT_PATH=/etc/rlm/bin
      ```

## Configure clusters

### About this task

Configure the clusters that are permitted to use License Scheduler in the Clusters section of the lsf.licensescheduler file.

This configuration is only required if you are using more than one cluster.

### Procedure

In the Clusters section, list all clusters that can use License Scheduler.

For example:

```
Begin Clusters 
CLUSTERS 
cluster1 
cluster2
End Clusters
```

## Configure projects

### About this task

Each project that is defined in a Projects section of lsf.licensescheduler can have a distribution policy that is applied in the Feature section, where projects can be associated with license features.

### Procedure

Define the projects with or without priority.

```
Begin Projects 
PROJECTS       PRIORITY 
Lp1             3 
Lp2             1 
Lp3             2 
default         0 
End Projects
```

The higher the number, the higher the priority. When two projects have the same priority number that is configured, the first listed project has a higher priority. Priority is taken into account when license preemption occurs, where lower priority projects are preempted first.

If not explicitly configured, the default project has the priority of 0. A default project is used when no license project is specified during job submission.

### Add project description

#### About this task

Optionally, you can add a project description of up to 64 characters to your projects to help identify them.

#### Procedure

In the Project section of lsf.licensescheduler, find the project and add a description in the DESCRIPTION column.

For example:

```
Begin Projects
PROJECTS PRIORITY DESCRIPTION
p1       10       "Engineering project 123"
p2       9        "QA build project 2C"
P3       8        ""
End Projects
```

#### Results

When you are running **blinfo -Lp** or **blinfo -G**, any existing project descriptions display.

## Project mode service domains

A service domain is a group of one or more license servers. License Scheduler manages the scheduling of the license tokens, but the license server actually supplies the licenses. You must configure at least one service domain for License Scheduler.

In project mode, each cluster can access licenses from multiple WAN and LAN service domains. License Scheduler collects license availability and usage from license server hosts, and merges this information with license demand and usage information from LSF clusters to make distribution and preemption decisions.

**Note**Unless you require multiple service domains for some specific reason, configure both modes with at most one LAN and one WAN for each feature in a cluster. Because License Scheduler does not control license checkout, running with one cluster that is accessing multiple service domains is not optimal.

### Configure service domains

#### About this task

You configure each service domain, with the license server names and port numbers that serve licenses to a network, in the ServiceDomain section of the lsf.licensescheduler file.

#### Procedure

1. Add a ServiceDomain section, and define **NAME** for each service domain.

   For example:

   ```
   Begin ServiceDomain 
   NAME=DesignCenterA 
   End ServiceDomain
   ```

2. Specify the license server hosts for that domain, including the host name and license manager port number.

   For example:

   ```
   Begin ServiceDomain 
   NAME=DesignCenterA 
   LIC_SERVERS=((1700@hostA)) 
   End ServiceDomain
   ```

   For multiple license servers:

   ```
   LIC_SERVERS=((1700@hostA)(1700@hostB))
   ```

   For redundant servers, the parentheses are used to group the three hosts that share license.dat file:

   `LIC_SERVERS=((1700@hostD 1700@hostE 1700@hostF))`

   **Note**If FlexNet uses a port from the default range, you can specify the host name without the port number. See the FlexNet documentation for the values of the default port range.

   `LIC_SERVERS=((@hostA))`

### Configure remote license server hosts

#### Before you begin

If you are using FlexNet as a license manager, the FlexNet license server hosts must have **lmutil** (or **lmstat**) in the **LMSTAT_PATH** directory before configuring these hosts with LSF License Scheduler.

If you are using Reprise License Manager, the Reprise License Manager license server hosts must have **rlmutil** (or **rlmstat**) directory before configuring these hosts with LSF License Scheduler.

#### About this task

The license collector (**blcollect**) is a multi-threaded daemon that queries all license servers under LSF License Scheduler for license usage information.

The license collector calls **lmutil** or **lmstat** (for FlexNet), or **rlmutil** or **rlmstat** (for Reprise License Manager) to collect information from each license server. When there are both local and remote license servers (that is, license servers that are in a different subnet from the host running **blcollect**), the threads that collect information from the remote license servers are slower than the threads that collect information from local license servers.

If there are remote license servers, designate at least one remote license server within each domain as a remote agent host. The license collector connects to the remote agent host and calls **lmutil**, **lmstat**, **rlmutil**, or **rlmstat** on the remote agent host and gets license information from all license servers that the remote agent host serves. The remote agent host and the remote license servers should be in the same domain to improve access.

#### Procedure

1. Select the connection method for the license collector to connect to remote hosts.

   LSF License Scheduler supports the use of **ssh**, **rsh**, and **lsrun** to connect to remote hosts. If using **lsrun** as the connection method, the agent host must be a server host in the LSF cluster and RES must be started on this host. Otherwise, if using **ssh** or **rsh** as the connection method, the agent host does not have to be a server host in the LSF cluster.

   1. In the Parameters section, define the **REMOTE_LMSTAT_PROTOCOL** parameter and specify the connection command (and command options, if required) to connect to remote servers.

      REMOTE_LMSTAT_PROTOCOL=ssh [ssh_command_options] | rsh [rsh_command_options] | lsrun [lsrun_command_options]

      The default connection method is **ssh** with no command options. LSF License Scheduler uses the specified command (and optional command options) to connect to the agent host. LSF License Scheduler automatically appends the name of the agent host to the command, so there is no need to specify the host with the command.

      **Note**LSF License Scheduler does not validate the specified command, so you must ensure that you correctly specify the command. Any connection errors are noted in the **blcollect** log file.

   2. If the connection method is **ssh** or **rsh**, verify that this connection method is configured so the host running the license collector can connect to remote hosts without specifying a password.

2. Define remote license servers and remote agent hosts.

   In the ServiceDomain section, define the **REMOTE_LMSTAT_SERVERS** parameter:

   REMOTE_LMSTAT_SERVERS=host_name[(host_name ...)] [host_name[(host_name ...)] ...]

   Specify a remote agent host, then any license servers that it serves in parentheses. The remote agent host and the license servers that it serves must be in the same subnet. If you specify a remote agent host by itself without any license servers (for example, REMOTE_LMSTAT_SERVERS=hostA), the remote agent host is considered to be a remote license server with itself as the remote agent host. That is, the license collector connects to the remote agent host and only gets license information on the remote agent host. You can specify multiple remote agent hosts to serve multiple subnets, or multiple remote agent hosts to serve specific license servers within the same subnet.

   Any host that you specify here must be a license server defined in **LIC_SERVERS**. Any hosts defined in **REMOTE_LMSTAT_SERVERS** that are not also defined in **LIC_SERVERS** are ignored.

   The following examples assume that the license collector (**blcollect**) is running on LShost1. That is, the following parameter is specified in the Parameters section:

   ```
   Begin Parameters
   ...
   HOSTS=LShost1
   ...
   End Parameters
   ```

   - One local license server (

     hostA

     ) and one remote license server (

     hostB

     ):

     ```
     LIC_SERVERS=((1700@hostA)(1700@hostB))
     REMOTE_LMSTAT_SERVERS=hostB
     ```

     - The license collector runs **lmutil**, **lmstat**, **rlmutil**, or **rlmstat** directly on hostA to get license information on hostA.
     - Because hostB is defined without additional license servers, hostB is a remote agent host that only serves itself. The license collector connects to hostB (using the command specified by the **REMOTE_LMSTAT_PROTOCOL** parameter) and runs **lmutil**, **lmstat**, **rlmutil**, or **rlmstat** to get license information on 1700@hostB.

   - One local license server (

     hostA

     ), one remote agent host (

     hostB

     ) that serves one remote license server (

     hostC

     ), and one remote agent host (

     hostD

     ) that serves two remote license servers (

     hostE

      

     and

      

     hostF

     ):

     ```
     LIC_SERVERS=((1700@hostA)(1700@hostB)(1700@hostC)(1700@hostD)(1700@hostE)(1700@hostF))
     REMOTE_LMSTAT_SERVERS=hostB(hostC) hostD(hostE hostF)
     ```

     - The license collector runs **lmutil**, **lmstat**, **rlmutil**, or **rlmstat** directly to get license information from 1700@hostA, 1700@hostB, and 1700@hostD.

     - The license collector connects to

        

       hostB

        

       (using the command specified by the

        

       REMOTE_LMSTAT_PROTOCOL

        

       parameter) and runs

        

       **lmutil**, **lmstat**, **rlmutil**, or **rlmstat**

        

       to get license information on

        

       1700@hostC

       .

       hostB and hostC should be in the same subnet to improve access.

     - The license collector connects to

        

       hostD

        

       (using the command specified by the

        

       REMOTE_LMSTAT_PROTOCOL

        

       parameter) and runs

        

       **lmutil**, **lmstat**, **rlmutil**, or **rlmstat**

        

       to get license information on

        

       1700@hostE

        

       and

        

       1700@hostF

       .

       hostD, hostE, and hostF should be in the same subnet to improve access.

   - One local license server (

     hostA

     ), one remote license server (

     hostB

     ), and one remote agent host (

     hostC

     ) that serves two remote license servers (

     hostD

      

     and

      

     hostE

     ):

     ```
     LIC_SERVERS=((1700@hostA)(1700@hostB)(1700@hostC)(1700@hostD)(1700@hostE))
     REMOTE_LMSTAT_SERVERS=hostB hostC(hostD hostE)
     ```

     - The license collector runs **lmutil**, **lmstat**, **rlmutil**, or **rlmstat** directly to get license information on 1700@hostA and 1700@hostC.

     - The license collector connects to hostB (using the command specified by the **REMOTE_LMSTAT_PROTOCOL** parameter) and runs **lmutil**, **lmstat**, **rlmutil**, or **rlmstat** to get license information on 1700@hostB.

     - The license collector connects to

        

       hostC

        

       (using the command specified by the

        

       REMOTE_LMSTAT_PROTOCOL

        

       parameter) and runs

        

       **lmutil**, **lmstat**, **rlmutil**, or **rlmstat**

        

       to get license information on

        

       1700@hostD

        

       and

        

       1700@hostE

       .

       hostC, hostD, and hostE should be in the same subnet to improve access.

## Configure license features

### About this task

Each type of license requires a Feature section in the lsf.licensescheduler file.

The Feature section includes the license distribution policy.

### Procedure

1. Define the feature name that is used by the license manager to identify the type of license by using the **NAME** parameter.

   Optionally, define an alias between LSF License Scheduler and the license manager feature names by using the **LM_LICENSE_NAME** parameter to specify the license manager feature name and the **NAME** parameter to define the LSF License Scheduler alias.

   You only need to specify **LM_LICENSE_NAME** if the LSF License Scheduler token name is not identical to the license manager feature name, or for license manager feature names that either start with a number or contain a hyphen character (-), which are not supported in LSF.

   If the license manager feature name is AppZ201 and you intend to use this same name as the LSF License Scheduler token name, define the **NAME** parameter as follows:

   ```
   Begin Feature
   NAME=AppZ201 
   End Feature
   ```

   If the license manager feature name 201-AppZ, this is not supported in LSF because the feature name starts with a number and contains a hyphen. Therefore, define AppZ201 as an alias of the 201-AppZ license manager feature name as follows:

   ```
   Begin Feature
   NAME=AppZ201
   LM_LICENSE_NAME=201-AppZ 
   End Feature
   ```

2. Optionally, combine multiple interchangeable license manager features into one LSF License Scheduler alias by specifying multiple license manager feature names in **LM_LICENSE_NAME** as a space-delimited list.

   In this example, two license manager features named 201-AppZ and 202-AppZ are combined into an alias named AppZ201.

   ```
   Begin Feature
   NAME=AppZ201
   LM_LICENSE_NAME=201-AppZ 202-AppZ
   End Feature
   ```

   AppZ201 is a combined feature that uses both 201-AppZ and 202-AppZ tokens. Submitting a job with AppZ201 in the rusage string (for example, bsub -Lp Lp1 -R "rusage[AppZ201=2]" myjob) means that the job checks out tokens for either 201-AppZ or 202-AppZ.

3. Define a distribution policy.

   A distribution policy defines the license fairshare policy in the format:

   ```
   DISTRIBUTION = ServiceDomain1 (project1 share_ratio project2 share_ratio ...)
   ServiceDomain2 (project3 share_ratio ...)
   ```

   For example, a basic configuration assigns shares:

   ```
   Begin Feature 
   LM_LICENSE_NAME=201-AppZ 
   NAME=AppZ201 
   DISTRIBUTION = DesignCenterA (LpA 2 LpB 1 default 1)
   End Feature
   ```

   LpA has the right to twice as many licenses as LpB. Jobs that are submitted without a license project that is specified can run under the default project.

4. Optionally, add owned licenses to the distribution policy in the format:

   ```
   DISTRIBUTION = ServiceDomain1 (project1 share_ratio/number_owned
   project2 share_ratio/number_owned ...) ServiceDomain2
   (project3 share_ratio ...)
   ```

   If LS_FEATURE_PERCENTAGE=Y or LS_ACTIVE_PERCENTAGE=Y in lsf.licensescheduler, number_owned is expressed as a percentage of the total licenses.

   Example 1:

   ```
   DISTRIBUTION = LanServer(Lp1 1 Lp2 1/10)
   ```

   This example assumes that there are 10 licenses in total, all owned by Lp2.

   The two License Scheduler projects, Lp1 and Lp2, and share the licenses, but grant ownership of the licenses to one of the projects (Lp2).

   When Lp2 has no work to be done, Lp1 can use the licenses. When Lp2 has work to do, Lp1 must return the license immediately to Lp2. The license utilization is always at the maximum, showing that all licenses are in use even while the license distribution policies are being enforced.

   Example 2:

   ```
   DISTRIBUTION=LanServer1(Lp1 1 Lp2 2/6)
   ```

   Lp1 is set to use one third of the available licenses and Lp2 to use two thirds of the licenses. However, Lp2 is always entitled to six licenses and preempts other license project jobs when licenses are needed immediately.

   If the projects are competing for a total of 12 licenses, Lp2 is entitled to eight (six on demand, and two more as soon as they are free).

   If the projects are competing for only six licenses in total, Lp2 is entitled to all of them, and Lp1 can use licenses only when Lp2 does not need them.

## Track partial and unspecified license use

### About this task

When you want to manage licenses not included in job resource requirements or have applications that you know use licenses for only part of the length of each job, use these optional settings.

### Procedure

1. Optionally, specify **DYNAMIC=Y** to consider the license feature as a dynamic resource when it is only used for part of the job.

   Set **DYNAMIC=Y** for applications with known license use that do not use the license for the entire length of the job. Jobs are submitted with **duration** specified, then release the license when not in use.

   ```
   Begin Feature 
   NAME = p1_2 
   DISTRIBUTION= Lan1 (a 1 b 1 c 1 default 1) 
   DYNAMIC=Y 
   End Feature
   ```

   For example, a **taskman** job submission with **duration**:

   taskman -R "rusage[p1_2=1:duration=2]" myjob

2. Optionally, set **ENABLE_DYNAMIC_RUSAGE=Y** in the Feature section of lsf.licensescheduler to track license use of license features not specified at job submission.

   For example:

   ```
   Begin Feature 
   NAME = feat2 
   DISTRIBUTION = LanServer(proj1 1 default 1) 
   ENABLE_DYNAMIC_RUSAGE = y 
   End Feature
   ```

   Submit a job to run the application, specifying the license feature name:

   ```
   bsub -R "rusage[feat1=1]" -Lp proj1 app1 
   ```

   The job runs and license feat1 is checked out:

   ```
   blstat 
   FEATURE: feat1 
    SERVICE_DOMAIN: LanServer
    TOTAL_INUSE: 1    TOTAL_RESERVE: 0    TOTAL_FREE: 4    OTHERS: 0  
     PROJECT                 SHARE   OWN  INUSE RESERVE FREE   DEMAND 
     proj1                   50.0 %  0    1     0       2      0
     default                 50.0 %  0    0     0       2      0
   FEATURE: feat2             
    SERVICE_DOMAIN: LanServer
    TOTAL_INUSE: 0    TOTAL_RESERVE: 0    TOTAL_FREE: 10   OTHERS: 0   
     PROJECT                 SHARE   OWN  INUSE RESERVE FREE   DEMAND 
     proj1                   50.0 %  0    0     0       5      0
     default                 50.0 %  0    0     0       5      0
   ```

   ```
   blusers -l 
   FEATURE  SERVICE_DOMAIN  USER   HOST    NLICS   NTASKS OTHERS  DISPLAYS   PIDS 
   feat1    LanServer       user1  hostA   1       1      0       (/dev/tty) (16326)
   ```

   ```
   blusers -J 
   JOBID   USER     HOST     PROJECT          CLUSTER        START_TIME 
   1896    user1    hostA    proj1            cluster1       Aug  9 10:01:25 
   RESOURCE        RUSAGE        SERVICE_DOMAIN   INUSE  EFFECTIVE_PROJECT
   feat1           1             LanServer        1      proj1
   ```

   Later, app1 checks out feature feat2. Since it was not specified at job submission, feat2 is a class C license checkout. But since it is configured with **ENABLE_DYNAMIC_RUSAGE=Y**, jobs that require feat2 are considered managed workload, and subject to the distribution policies of project proj1:

   ```
   blstat 
   FEATURE: feat1 
   SERVICE_DOMAIN: LanServer 
   TOTAL_INUSE: 1    TOTAL_RESERVE: 0    TOTAL_FREE: 4    OTHERS: 0 
   PROJECT                 SHARE   OWN  INUSE RESERVE FREE   DEMAND 
    proj1                  50.0 %  0    1     0       2      0
    default                50.0 %  0    0     0       2      0
   ```

   ```
   FEATURE: feat2             
   SERVICE_DOMAIN: LanServer 
   TOTAL_INUSE: 1    TOTAL_RESERVE: 0    TOTAL_FREE: 9    OTHERS: 0 
   PROJECT                 SHARE   OWN  INUSE RESERVE FREE   DEMAND 
    proj1                  50.0 %  0    1     0       4      0
    default                50.0 %  0    0     0       5      0
   ```

   ```
   blusers -l 
   FEATURE  SERVICE_DOMAIN  USER   HOST    NLICS  NTASKS  OTHERS  DISPLAYS   PIDS 
   feat1    LanServer       user1  hostA   1      1       0       (/dev/tty) (16326) 
   feat2    LanServer       user1  hostA   1      1       0       (/dev/tty) (16344)
   ```

   ```
   blusers -J 
   JOBID   USER      HOST      PROJECT             CLUSTER        START_TIME 
   1896    user1     hostA     proj1               cluser1        Aug  9 10:01:25 
   RESOURCE        RUSAGE        SERVICE_DOMAIN   INUSE  EFFECTIVE_PROJECT
   feat1           1             LanServer        1      proj1
   feat2           1             LanServer        1      proj1
   ```

## Restart to implement configuration changes

### Procedure

1. Run bladmin reconfig to restart the **bld**.

2. If you deleted any Feature sections, restart **mbatchd**. In this case, a message is written to the log file, prompting the restart.

   If required, run badmin mbdrestart to restart each LSF cluster.

## View projects and descriptions

### Procedure

Run **blinfo -Lp** to view projects and descriptions.

For example:

```
blinfo -Lp
PROJECT PRIORITY DESCRIPTION
p1      10       Engineering project 123
p2      9        QA build project 2C
P3      8        
```

## View license allocation

### Procedure

Run blstat -t token_name to view information for a specific license token (as configured in a Feature section).

**blstat** output differs for cluster mode and project mode.