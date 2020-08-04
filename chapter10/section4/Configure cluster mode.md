# 配置集群模式

使用集群模式，可在 LSF 集群之间分配许可证，而让每个 LSF 集群的调度程序调度作业，为集群中的项目分配许可证并抢占作业。

## 配置参数

### 步骤

1. 集群模式可以全局设置，也可以针对单个许可证功能设置。 对于某些功能使用集群模式，对于某些功能使用项目模式时，请分别进行设置。

   - 如果将集群模式用于所有许可证功能，请在 lsf.licensescheduler 的 “Parameters” 部分中定义CLUSTER_MODE=Y。

   - 如果您将集群模式用于某些许可证功能，请在 lsf.licensescheduler 的 “Feature” 部分中为单个许可证功能定义 CLUSTER_MODE=Y。

      **CLUSTER_MODE** 的 Feature 区域设置，将覆盖全局 Parameter 区域设置。

2. 列出许可证调度程序主机。

   在 LSF 安装中，默认情况下，**HOSTS** 参数设置为 **LSF_MASTER_LIST**。

   - 按从最倾向使用到最不倾向的顺序列出主机。 第一台主机是主许可证调度程序主机。
   - 除非所有您的 License Scheduler 客户端都在同一 DNS 域中运行，否则请指定标准主机名，例如 hostX.mycompany.com。

   HOSTS=host1 host2

3. 指定许可证调度程序，和许可证管理器之间的数据收集频率。

   默认值为 60 秒。

   LM_STAT_INTERVAL=秒数值

4. 为所使用的许可证管理器，指定命令的文件路径。

   - 如果使用的是 FlexNet，请指定 **lmutil** （或 **lmstat**）命令的路径。

     例如，如果 **lmstat** 位于 /etc/flexlm/bin 中：
   
     ```shell
     LMSTAT_PATH=/etc/flexlm/bin
     ```
   
     

   - 如果使用的是 Reprise License Manager，请指定 **rlmutil**（或 **rlmstat**）命令的路径。

     例如，如果命令在 /etc/rlm/bin 中：
     
     ```shell
     RLMSTAT_PATH=/etc/rlm/bin
     ```
     
     
   

## 配置集群

### 任务说明

在 lsf.licensescheduler 文件的 “Cluster” 部分中，配置允许使用许可调度程序的集群。

仅当您使用多个集群时才需要配置集群。

### 步骤

在 “集群” 部分中，列出可以使用许可证计划程序的所有集群。

例如：

```shell
Begin Clusters
CLUSTERS
cluster1
cluster2
End Clusters 
```

## 集群模式服务域

服务域是一组一个或多个许可证服务器。 License Scheduler 管理许可证令牌的调度，但是许可证服务器实际上提供了许可证。

在集群模式下，每个集群可以从一个 WAN 和一个 LAN 服务域访问许可证。

![Each cluster has access to one WAN and one LAN service.](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/license_scheduler/cluster_mode_lan_wan.jpg)

License Scheduler 不控制应用程序检出行为。 如果可以从 LAN 和 WAN 服务域中获得相同的许可证，则 License Scheduler 希望作业首先尝试从 LAN 获取许可证。

### 配置服务域部分

#### 任务说明

您可以在 lsf.licensescheduler 文件的 ServiceDomain 部分中，使用为网络提供许可证的许可证服务器名称和端口号来配置每个服务域。

稍后在 “ Feature” 部分中指定服务域是 WAN 还是 LAN 服务域。

#### 步骤

1. 添加一个 ServiceDomain 部分，并为每个服务域定义 **NAME**。

   例如：

   ```shell
   Begin ServiceDomain 
   NAME=DesignCenterA 
   End ServiceDomain
   ```

2. 指定该域的许可证服务器主机，包括主机名和许可证管理器端口号。

   例如：

   ```shell
   Begin ServiceDomain 
   NAME=DesignCenterA 
   LIC_SERVERS=((1700@hostA))
   End ServiceDomain
   ```

   对于多个许可证服务器：

   ```shell
   LIC_SERVERS=((1700@hostA)(1700@hostB))
   ```

   对于冗余服务器，括号用于将共享同一 license.dat 文件的三台主机分组：

   `LIC_SERVERS=((1700@hostD 1700@hostE 1700@hostF))`

   ##### 提示

   如果 FlexNet 使用默认范围内的端口，则可以指定不带端口号的主机名。 请参阅 FlexNet 文档以获取默认端口范围的值。
   
   `LIC_SERVERS=((@hostA))`

### 配置远程许可证服务器主机

#### 开始之前

如果将 FlexNet 用作许可证管理器，则在使用 LSF License Scheduler 配置这些主机之前，FlexNet 许可证服务器主机必须在 **LMSTAT_PATH** 目录中具有 **lmutil**（或 **lmstat**）。

如果使用的是 Reprise License Manager，则在使用 LSF License Scheduler 配置这些主机之前，Reprise License Manager 许可证服务器主机必须具有 **rlmutil**（或 **rlmstat**）目录。

#### 任务说明

许可证收集器（**blcollect**）是一个多线程守护程序，可在 LSF License Scheduler 下向所有许可证服务器查询许可证使用信息。

许可证收集器调用 **lmutil** 或 **lmstat**（对于 FlexNet 而言），或 **rlmutil** 或 **rlmstat**（对于 Reprise License Manager 而言），以从每个许可证服务器收集信息。 当同时存在本地和远程许可证服务器（即，与运行 **blcollect** 的主机位于不同子网中的许可证服务器）时，从远程许可证服务器收集信息的线程，比从本地许可证服务器收集信息的线程慢。

如果有远程许可证服务器，请在每个域中至少指定一个远程许可证服务器作为远程代理主机。许可证收集器连接到远程代理主机，并在远程代理主机上调用 **lmutil**，**lmstat** **，rlmutil **或 **rlmstat**，并从所有许可证服务器获取许可证信息。 远程代理主机服务。 远程代理主机和远程许可证服务器应位于同一域中以改善访问。

#### 步骤

1. 选择许可证收集器连接到远程主机的连接方法。

   LSF License Scheduler 支持使用 **ssh** ，**rsh** 和l **lsrun ** 连接到远程主机。 如果使用 **lsrun** 作为连接方法，则代理主机必须是 LSF 集群中的服务器主机，并且 RES 必须在此主机上启动。 否则，如果使用 **ssh** 或 **rsh**作为连接方法，则代理主机不必是 LSF 集群中的服务器主机。

   - 在 “Parameters” 部分中，定义 **REMOTE_LMSTAT_PROTOCOL** 参数，并指定连接命令（和命令选项，如果需要的话）以连接到远程服务器。

     REMOTE_LMSTAT_PROTOCOL=ssh [ssh 命令选项] | rsh [rsh 命令选项] | lsrun [lsrun 命令选项]

     默认连接方法是 **ssh**，没有命令选项。 LSF License Scheduler 使用指定的命令（和可选的命令选项）连接到代理主机。  LSF License Scheduler 会自动将代理主机的名称附加到命令中，因此无需使用命令指定主机。

     ##### 提示

     LSF License Scheduler 无法验证指定的命令，因此必须确保正确指定命令。**blcollect** 日志文件中会记录所有连接错误。

   - 如果连接方法是 **ssh** 或 **rsh**，请验证是否已配置此连接方法，以便运行许可证收集器的主机，可以连接到远程主机而无需指定密码。

2. 定义远程许可证服务器和远程代理主机。

   在 ServiceDomain 部分中，定义 **REMOTE_LMSTAT_SERVERS** 参数：

   REMOTE_LMSTAT_SERVERS=host_name[(host_name ...)] [host_name[(host_name ...)] ...]

   指定一个远程代理主机，然后在括号中指定它服务的所有许可证服务器。 远程代理主机及其服务的许可证服务器，必须位于同一子网中。 如果您自己指定了一个远程代理主机，而没有任何许可证服务器（例如REMOTE_LMSTAT_SERVERS=hostA）, 则该远程代理主机，将被视为是一个以自身为远程代理主机的远程许可证服务器。也就是说，许可证收集器连接到远程代理主机，并且仅在远程代理主机上获取许可证信息。 您可以指定多个远程代理主机来服务多个子网，也可以指定多个远程代理主机来服务同一子网中的特定许可证服务器。

   您在此处指定的任何主机必须是在 **LIC_SERVERS** 中定义的许可证服务器。 **REMOTE_LMSTAT_SERVERS**中定义的所有主机，如果也未在 **LIC_SERVERS** 中定义，则将被忽略。

   以下示例假定许可证收集器（**blcollect**）在 LShost1 上运行。 也就是说，在 “Parameters” 部分中指定了以下参数：

   ```shell
   Begin Parameters
   ...
   HOSTS=LShost1
   ...
   End Parameters
   ```

   - 一台本地许可证服务器（hostA）和一台远程许可证服务器（hostB）：

     ```shell
LIC_SERVERS=((1700@hostA)(1700@hostB))
     REMOTE_LMSTAT_SERVERS=hostB
     ```
     
     - 许可证收集器直接在 hostA 上运行 **lmutil**，**lmstat**，**rlmutil** 或 **rlmstat**，以获取 hostA 上的许可证信息。
     - 因为在没有其他许可证服务器的情况下定义了 hostB，所以 hostB 是仅为其自身提供服务的远程代理主机。  许可证收集器连接到 hostB（使用 **REMOTE_LMSTAT_PROTOCOL** 参数指定的命令）并运行**lmutil** ，**lmstat**，**rlmutil** 或 **rlmstat** 以获取在 1700@hostB 上许可证信息 。

- 一台本地许可证服务器（hostA），一台为一台远程许可证服务器（hostC）服务的远程代理主机（hostB）和一台为两台远程许可证服务器（hostE和hostF）服务的远程代理主机（hostD）：

  ```shell
LIC_SERVERS=((1700@hostA)(1700@hostB)(1700@hostC)(1700@hostD)(1700@hostE)(1700@hostF))
  REMOTE_LMSTAT_SERVERS=hostB(hostC) hostD(hostE hostF)
```
  
- 许可证收集器直接运行 **lmutil**，**lmstat**，**rlmutil** 或 **rlmstat**，以从1700@hostA，1700@hostB 和 1700@hostD 获取许可证信息。
  
- 许可证收集器连接到 hostB（使用 **REMOTE_LMSTAT_PROTOCOL** 参数指定的命令），并运行 **lmutil**，**lmstat**，**rlmutil** 或 **rlmstat** 以获取有关 1700@hostC 的许可证信息。
  
  hostB 和 hostC 应该位于同一子网中以改善访问。
  
- 许可证收集器连接到 hostD（使用 **REMOTE_LMSTAT_PROTOCOL** 参数指定的命令），并运行 **lmutil**，**lmstat**，**rlmutil** 或 **rlmstat** 以获取有关 1700@hostE 和 1700@hostF 的许可证信息。
  
  hostD，hostE 和 hostF 应该位于同一子网中以改善访问。
  
- 一台本地许可证服务器（hostA），一台远程许可证服务器（hostB）和一台为两个远程许可证服务器（hostD和hostE）提供服务的远程代理主机（hostC）：

  ```
LIC_SERVERS=((1700@hostA)(1700@hostB)(1700@hostC)(1700@hostD)(1700@hostE))
  REMOTE_LMSTAT_SERVERS=hostB hostC(hostD hostE)
```
  
- 许可证收集器直接运行 **lmutil**，**lmstat**，**rlmutil** 或 **rlmstat**，以获取有关 1700@hostA 和 1700@hostC 的许可证信息。
  
- 许可证收集器连接到 hostB（使用 **REMOTE_LMSTAT_PROTOCOL** 参数指定的命令）并运行 **lmutil** ，**lmstat**，**rlmutil**  或 **rlmstat ** 以获取在 1700@hostB 上的许可证信息 。
  
- 许可证收集器连接到 hostC（使用 **REMOTE_LMSTAT_PROTOCOL** 参数指定的命令），并运行 **lmutil**，**lmstat**，**rlmutil** 或 **rlmstat** 以获取有关 1700@hostD 和 1700@hostE 的许可证信息。
  
  hostC，hostD 和 hostE 应该位于同一子网中以改善访问。

### 配置局域网服务域（LAN）

#### 任务说明

You configure LAN service domains in the Feature section of lsf.licensescheduler. Only a single cluster and service domain can be specified in each LAN Feature section. Licenses from the LAN service domain are statically allocated to the cluster.

#### 步骤

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

### 配置 WAN 服务域

#### 任务说明

WAN configuration includes all clusters that are sharing the WAN service domain. As for a LAN service domain, you set this configuration in the **CLUSTER_DISTRIBUTION** parameter in the Feature section of the lsf.licensescheduler file.

For a WAN service domain, you can optionally configure dynamic license sharing based on past license use across all clusters that are served by the WAN service domain, and if required set minimum and maximum allocations for each cluster.

#### 步骤

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

#### 结果

To allow a cluster to be able to use licenses only when another cluster does not need them, you can set the cluster distribution for the cluster to 0, and specify an allocation buffer for the number of tokens that the cluster can request.

For example:

```
Begin Feature
CLUSTER_DISTRIBUTION=Wan(CL1 0 CL2 1)
ALLOC_BUFFER=5
End Feature
```

When no jobs are running, the token allocation for CL1 is five. If CL2 does not require the tokens, CL1 can get more than five.

#### 示例

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

## 配置许可证特征

### 任务说明

Each type of license requires a Feature section in the lsf.licensescheduler file.

### 步骤

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

## 在集群模式下配置Taskman作业

### 任务说明

Optionally, to run taskman (interactive) jobs in cluster mode, include the dummy cluster interactive in your service domain configuration.

### 步骤

In the Feature section:

1. Include the dummy cluster interactive in the **CLUSTER_DISTRIBUTION** parameter.
2. Set a share for the dummy cluster interactive.
3. Optionally, set an allocation buffer for the dummy cluster interactive to enable dynamic allocation.

### 示例

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

## 将许可证分配给非 LSF 作业

### 任务说明

Applies to WAN service domains only.

### 步骤

Set **WORKLOAD_DISTRIBUTION** in the Feature section to allocate licenses for non-LSF use.

```
WORKLOAD_DISTRIBUTION=service_domain_name(LSF lsf_distribution NON_LSF non_lsf_distribution)
```

If **WORKLOAD_DISTRIBUTION** is set for a LAN service domain in cluster mode, the parameter is ignored.

### 示例

For example, to set aside 20% of licenses for use outside of LSF:

```
Begin Feature
NAME=licenseB
CLUSTER_DISTRIBUTION=MyWanServer(tokyo_cl 1 newyork_cl 1)
WORKLOAD_DISTRIBUTION=MyWanServer(LSF 8 NON_LSF 2)
End Feature
```

## 重新启动以实施配置更改

### 步骤

1. Run bladmin reconfig to restart the bld.

2. If you deleted any Feature sections, restart mbatchd. In this case, a message is written to the log file, prompting the restart.

   If required, run badmin mbdrestart to restart each LSF cluster.

## 查看许可证分配

### 步骤

Run blstat -t token_name to view information for a specific license token (as configured in a Feature section).

**blstat** output differs for cluster mode and project mode.

