# 配置集群模式

使用集群模式，可在 LSF 集群之间分配许可证，而让每个 LSF 集群的调度程序调度作业，为集群中的项目分配许可证并抢占作业。

## 配置参数

### 步骤

1. Cluster mode can be set globally, or for individual license features. Set individually when using cluster mode for some features and project mode for some features.

   - If you are using cluster mode for all license features, define CLUSTER_MODE=Y in the Parameters section of lsf.licensescheduler.

   - If you are using cluster mode for some license features, define CLUSTER_MODE=Y for individual license features in the Feature section of lsf.licensescheduler.

      The Feature section setting of **CLUSTER_MODE** overrides the global Parameter section setting.

2. List the License Scheduler hosts.

   By default with an LSF installation, the **HOSTS** parameter is set to the **LSF_MASTER_LIST**.

   - List the hosts in order from most preferred to least preferred. The first host is the master license scheduler host.
   - Specify a fully qualified host name such as hostX.mycompany.com unless all your License Scheduler clients run in the same DNS domain.

   HOSTS=host1 host2

3. Specify the data collection frequency between License Scheduler and the license manager.

   The default is 60 seconds.

   LM_STAT_INTERVAL=seconds

4. Specify the file paths to the commands for the license managers that you are using.

   - If you are using FlexNet, specify the path to the **lmutil** (or **lmstat**) command.

     For example, if **lmstat** is in /etc/flexlm/bin:

   ```shell
   LMSTAT_PATH=/etc/flexlm/bin
   ```

   - If you are using Reprise License Manager, specify the path to the **rlmutil** (or **rlmstat**) command.

     For example, if the commands are in /etc/rlm/bin:

   ```shell
   RLMSTAT_PATH=/etc/rlm/bin
   ```

## 配置集群

### 任务说明

Configure the clusters that are permitted to use License Scheduler in the Clusters section of the lsf.licensescheduler file.

Configuring the clusters is only required if you are using more than one cluster.

### 步骤

In the Clusters section, list all clusters that can use License Scheduler.

For example:

```
Begin Clusters
CLUSTERS
cluster1
cluster2
End Clusters 
```

## 集群模式服务域

A service domain is a group of one or more license servers. License Scheduler manages the scheduling of the license tokens, but the license server actually supplies the licenses.

In cluster mode, each cluster can access licenses from one WAN and one LAN service domain.

![Each cluster has access to one WAN and one LAN service.](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/license_scheduler/cluster_mode_lan_wan.jpg)

License Scheduler does not control application checkout behavior. If the same license is available from both the LAN and WAN service domains, License Scheduler expects jobs to try to obtain the license from the LAN first.

### 配置服务域部分

#### 任务说明

You configure each service domain, with the license server names and port numbers that serve licenses to a network, in the ServiceDomain section of the lsf.licensescheduler file.

Whether the service domain is a WAN or LAN service domain is specified later in the Feature section.

#### 步骤

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

   For redundant servers, the parentheses are used to group the three hosts that share the same license.dat file:

   `LIC_SERVERS=((1700@hostD 1700@hostE 1700@hostF))`

   **Note**If FlexNet uses a port from the default range, you can specify the host name without the port number. See the FlexNet documentation for the values of the default port range.

   `LIC_SERVERS=((@hostA))`

### 配置远程许可证服务器主机

#### 开始之前

If you are using FlexNet as a license manager, the FlexNet license server hosts must have **lmutil** (or **lmstat**) in the **LMSTAT_PATH** directory before configuring these hosts with LSF License Scheduler.

If you are using Reprise License Manager, the Reprise License Manager license server hosts must have **rlmutil** (or **rlmstat**) directory before configuring these hosts with LSF License Scheduler.

#### 任务说明

The license collector (**blcollect**) is a multi-threaded daemon that queries all license servers under LSF License Scheduler for license usage information.

The license collector calls **lmutil** or **lmstat** (for FlexNet), or **rlmutil** or **rlmstat** (for Reprise License Manager) to collect information from each license server. When there are both local and remote license servers (that is, license servers that are in a different subnet from the host running **blcollect**), the threads that collect information from the remote license servers are slower than the threads that collect information from local license servers.

If there are remote license servers, designate at least one remote license server within each domain as a remote agent host. The license collector connects to the remote agent host and calls **lmutil**, **lmstat**, **rlmutil**, or **rlmstat** on the remote agent host and gets license information from all license servers that the remote agent host serves. The remote agent host and the remote license servers should be in the same domain to improve access.

#### 步骤

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

### Configure LAN service domain

#### About this task

You configure LAN service domains in the Feature section of lsf.licensescheduler. Only a single cluster and service domain can be specified in each LAN Feature section. Licenses from the LAN service domain are statically allocated to the cluster.

#### Procedure

In the Feature section, set

```
CLUSTER_DISTRIBUTION=service_domain(cluster_name share)
```

Use the service domain name that is defined in the ServiceDomain section.

For example:

```
Begin Feature
NAME=verilog
CLUSTER_DISTRIBUTION=MyLanServer(tokyo_cluster 1)
End Feature
```

### Configure WAN service domain

#### About this task

WAN configuration includes all clusters that are sharing the WAN service domain. As for a LAN service domain, you set this configuration in the **CLUSTER_DISTRIBUTION** parameter in the Feature section of the lsf.licensescheduler file.

For a WAN service domain, you can optionally configure dynamic license sharing based on past license use across all clusters that are served by the WAN service domain, and if required set minimum and maximum allocations for each cluster.

#### Procedure

1. Set the WAN service domain name in the **CLUSTER_DISTRIBUTION** parameter.

   ```
   CLUSTER_DISTRIBUTION = service_domain(cluster share/min/max...)
   ```

   Use the service domain name that is defined in the ServiceDomain section.

2. Configure each cluster.

   All clusters with access to the WAN service domain licenses must be included.

   1. Set the cluster name.

   2. Set the share for each cluster.

      The share is a non-negative integer representing the share of licenses each cluster receives in a static license allocation, and the starting share in a dynamic license allocation.

3. Optionally, set **ALLOC_BUFFER** in the Feature section of the lsf.licensescheduler file. When set, this parameter enables a dynamic sharing policy.

   ```
   ALLOC_BUFFER = buffer
   ```

   or

   ```
   ALLOC_BUFFER = cluster1 buffer1 cluster2 buffer2...default buffer
   ```

   - When extra license tokens are available, each cluster’s allocation increases to as much as **PEAK**+**BUFFER**.

     The value **BUFFER** is set by **ALLOC_BUFFER** in the Feature section, and the value PEAK is the peak value of dynamic license token use over a time interval that is set by **PEAK_INUSE_PERIOD** in the Parameters or Feature section.

   - When allocated tokens are not being use in a cluster, the cluster’s allocation goes down to **PEAK**+**BUFFER**.

     Since tokens are not being used in the cluster, the peak use value **PEAK** decreases, thus **PEAK**+**BUFFER** also decreases.

   The allocation buffer sets both the rate at which the cluster allocation can grow, and the number of licenses that can go unused, depending on demand.

   Allocation buffers help determine the maximum rate at which tokens can be transferred to a cluster as demand increases in the cluster. The maximum rate of transfer to a cluster is given by the allocation buffer that is divided by **MBD_REFRESH_INTERVAL**. Be careful not to set the allocation buffer too large so that licenses are not wasted because they are allocated to a cluster that cannot use them.

4. Optionally, when dynamic sharing is enabled (**ALLOC_BUFFER** is defined) you can set the minimum and maximum allocation for each cluster.

   The minimum allocation reserves license tokens for exclusive use by the cluster; the maximum allocation limits the total number of license tokens that are received by the cluster.

   Cluster shares take precedence over minimum allocations configured. If the minimum allocation exceeds the cluster's share of the total tokens, a cluster's allocation as given by **bld** may be less than the configured minimum allocation.

#### Results

To allow a cluster to be able to use licenses only when another cluster does not need them, you can set the cluster distribution for the cluster to 0, and specify an allocation buffer for the number of tokens that the cluster can request.

For example:

```
Begin Feature
CLUSTER_DISTRIBUTION=Wan(CL1 0 CL2 1)
ALLOC_BUFFER=5
End Feature
```

When no jobs are running, the token allocation for CL1 is five. If CL2 does not require the tokens, CL1 can get more than five.

#### Examples

Static example (no allocation buffer set):

```
Begin Feature
NAME=verilog
CLUSTER_DISTRIBUTION=MyWanServer(tokyo_cl 1 newyork_cl 1 toronto_cl 2)
End Feature
```

In this example, licenses are statically allocated based solely on the number of shares that are assigned to each cluster. If the number of licenses is not evenly divisible by the number of shares, the additional licenses are distributed round-robin to clusters in the specified order in **CLUSTER_DISTRIBUTION**. Thus if there are 98 licenses in total, tokyo_cl receives 25, newyork_cl receives 25, and toronto_cl receives 48. Each cluster limits the total rusage of running jobs that are based on the allocated license tokens.

Dynamic example (allocation buffer set):

```
Begin Feature
NAME=verilog
CLUSTER_DISTRIBUTION=MyWanServer(tokyo_cl 1 newyork_cl 1 toronto_cl 2/10/50)
ALLOC_BUFFER=tokyo_cl 5 newyork_cl 1 toronto_cl 2
End Feature
```

In this example, licenses are initially distributed according to the assigned shares. Since allocation buffers are set, dynamic sharing that is based on past use is enabled. Based on the allocation buffers, toyko_cl receives license tokens the fastest when there is demand within the cluster. Minimum and maximum allocations of 10 and 50 are set for toronto_cl, which also has the largest share.

LAN and dynamic WAN example:

```
Begin Feature
NAME=verilog
CLUSTER_DISTRIBUTION=MyWan(c1 1/1/25 c2 1/1/30 c3 2/5/100) MyLan(c1 1)
ALLOC_BUFFER=c3 5 default 2
End Feature
```

In this example, the verilog license feature is available from both WAN and LAN service domain, however only cluster c1 receives the license feature from both servers. Licenses from the WAN service domain are initially distributed according to the assigned shares. Since allocation buffers are set, dynamic sharing that is based on past use is enabled. Based on the allocation buffers cluster c3 receives license tokens the fastest when there is demand within the cluster.

## Configure license features

### About this task

Each type of license requires a Feature section in the lsf.licensescheduler file.

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

## Configure taskman jobs in cluster mode

### About this task

Optionally, to run taskman (interactive) jobs in cluster mode, include the dummy cluster interactive in your service domain configuration.

### Procedure

In the Feature section:

1. Include the dummy cluster interactive in the **CLUSTER_DISTRIBUTION** parameter.
2. Set a share for the dummy cluster interactive.
3. Optionally, set an allocation buffer for the dummy cluster interactive to enable dynamic allocation.

### Examples

```
Begin Feature
NAME=licenseA
CLUSTER_DISTRIBUTION=MyLanServer(tokyo_cl 1 interactive 1)
End Feature
 
Begin Feature
NAME=licenseB
CLUSTER_DISTRIBUTION=MyWanServer(tokyo_cl 1 newyork_cl 1 interactive 2)
End Feature
```

## Allocate licenses to non-LSF jobs

### About this task

Applies to WAN service domains only.

### Procedure

Set **WORKLOAD_DISTRIBUTION** in the Feature section to allocate licenses for non-LSF use.

```
WORKLOAD_DISTRIBUTION=service_domain_name(LSF lsf_distribution NON_LSF non_lsf_distribution)
```

If **WORKLOAD_DISTRIBUTION** is set for a LAN service domain in cluster mode, the parameter is ignored.

### Example

For example, to set aside 20% of licenses for use outside of LSF:

```
Begin Feature
NAME=licenseB
CLUSTER_DISTRIBUTION=MyWanServer(tokyo_cl 1 newyork_cl 1)
WORKLOAD_DISTRIBUTION=MyWanServer(LSF 8 NON_LSF 2)
End Feature
```

## Restart to implement configuration changes

### Procedure

1. Run bladmin reconfig to restart the bld.

2. If you deleted any Feature sections, restart mbatchd. In this case, a message is written to the log file, prompting the restart.

   If required, run badmin mbdrestart to restart each LSF cluster.

## View license allocation

### Procedure

Run blstat -t token_name to view information for a specific license token (as configured in a Feature section).

**blstat** output differs for cluster mode and project mode.