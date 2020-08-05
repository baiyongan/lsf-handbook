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

  

```shell
LIC_SERVERS=((1700@hostA)(1700@hostB)(1700@hostC)(1700@hostD)(1700@hostE))
REMOTE_LMSTAT_SERVERS=hostB hostC(hostD hostE)
```


- 许可证收集器直接运行 **lmutil**，**lmstat**，**rlmutil** 或 **rlmstat**，以获取有关 1700@hostA 和 1700@hostC 的许可证信息。
  
- 许可证收集器连接到 hostB（使用 **REMOTE_LMSTAT_PROTOCOL** 参数指定的命令）并运行 **lmutil** ，**lmstat**，**rlmutil**  或 **rlmstat ** 以获取在 1700@hostB 上的许可证信息 。
  
- 许可证收集器连接到 hostC（使用 **REMOTE_LMSTAT_PROTOCOL** 参数指定的命令），并运行 **lmutil**，**lmstat**，**rlmutil** 或 **rlmstat** 以获取有关 1700@hostD 和 1700@hostE 的许可证信息。
  
  hostC，hostD 和 hostE 应该位于同一子网中以改善访问。

### 配置局域网服务域（LAN）

#### 任务说明

您可以在 lsf.licensescheduler 的 “Feature” 部分中配置 LAN 服务域。 在每个 “ LAN Feature” 部分中只能指定一个集群和服务域。 来自 LAN 服务域的许可证被静态分配给集群。

#### 步骤

在 Feature 部分，设置

```shell
CLUSTER_DISTRIBUTION=service_domain(cluster_name share)
```
使用在 ServiceDomain 部分中定义的服务域名。

例如：

```shell
Begin Feature
NAME=verilog
CLUSTER_DISTRIBUTION=MyLanServer(tokyo_cluster 1)
End Feature
```
### 配置 WAN 服务域

#### 任务说明

WAN 配置包括共享 WAN 服务域的所有集群。 对于 LAN 服务域，请在 lsf.licensescheduler 文件的 “Feature” 部分的 **CLUSTER_DISTRIBUTION** 参数中设置此配置。

对于 WAN 服务域，您可以选择基于 WAN 服务域所服务的所有集群之间过去的许可证使用情况，来配置动态许可证共享，并在需要时为每个集群设置最小和最大分配。

#### 步骤

1. 在 **CLUSTER_DISTRIBUTION** 参数中设置 WAN 服务域名。

```shell
CLUSTER_DISTRIBUTION = service_domain(cluster share/min/max...)
```

   使用在 ServiceDomain 部分中定义的服务域名。

2. 配置每个集群。

   必须包括有权访问 WAN 服务域许可证的所有集群。

   1. 设置集群名称

   2. 设置每个集群的份额。

      份额是一个非负整数，代表每个集群在静态许可分配中获得的许可份额，以及在动态许可分配中的起始份额。

3. （可选）在 lsf.licensescheduler 文件的 “Feature” 部分中设置  **ALLOC_BUFFER **。 设置后，此参数将启用动态共享策略。

   ```shell
   ALLOC_BUFFER = buffer
   ```

   或者

   ```shell
   ALLOC_BUFFER = cluster1 buffer1 cluster2 buffer2...default buffer
   ```

      - 如果有额外的许可证令牌可用，则每个集群的分配增加到 **PEAK** + **BUFFER**。

        **BUFFER** 值由 “Feature” 部分中的 **ALLOC_BUFFER** 设置，而 PEAK 值是在 Parameters 或 Feature 部分中 **PEAK_INUSE_PERIOD** 设置的时间间隔内，动态许可证令牌使用的峰值。 

      - 如果集群中未使用分配的令牌，则集群的分配将降为 **PEAK** + **BUFFER**。

        由于集群中未使用令牌，因此峰值使用值 **PEAK** 降低，因此 **PEAK** + **BUFFER** 也降低。

   分配缓冲区，根据需要设置集群分配增长的速率，以及可以不使用的许可证数量。

   分配缓冲区可帮助确定随着集群中需求的增加将令牌传输到集群的最大速率。 分配给集群的最大速率由分配缓冲区除以 **MBD_REFRESH_INTERVAL**。注意不要将分配缓冲区设置得太大，以致于因为将许可证分配给了不能使用它们的集群，而浪费许可证。

4. （可选）启用动态共享（定义了 **ALLOC_BUFFER**）后，您可以为每个集群设置最小和最大分配。

   最低分配保留许可证令牌供集群专用； 最大分配限制了集群接收的许可证令牌的总数。

   集群共享优先于配置的最小分配。 如果最小分配超出了集群在总令牌中所占的份额，则 **bld** 给出的集群分配可能小于配置的最小分配。

#### 结果

为了允许一个集群仅在另一个集群不需要许可证时，才可以使用许可证，可以将集群的集群分布设置为 0，并为该集群可以请求的令牌数量指定一个分配缓冲区。

例如：

   ```shell
Begin Feature
CLUSTER_DISTRIBUTION=Wan(CL1 0 CL2 1)
ALLOC_BUFFER=5
End Feature
   ```
当没有作业在运行时，CL1 的令牌分配为 5。 如果 CL2 不需要令牌，则 CL1 可以获得 5 个以上。

#### 示例

##### 静态示例（未设置分配缓冲区）：

```shell
Begin Feature
NAME=verilog
CLUSTER_DISTRIBUTION=MyWanServer(tokyo_cl 1 newyork_cl 1 toronto_cl 2)
End Feature
```

在此示例中，仅基于分配给每个集群的份额数，来静态分配许可证。 如果许可证数量不能被份额数量平均整除，则附加许可证将按指定顺序以 **CLUSTER_DISTRIBUTION** 的形式循环分发给集群。 因此，如果总共有 98 个许可证，则 tokyo_cl 接收 25 个许可证，newyork_cl 接收 25 个许可证，toronto_cl 接收 48 个许可证。每个集群基于分配的许可证令牌，限制正在运行的作业的总使用率。

##### 动态示例（分配缓冲区集）：

```shell
Begin Feature
NAME=verilog
CLUSTER_DISTRIBUTION=MyWanServer(tokyo_cl 1 newyork_cl 1 toronto_cl 2/10/50)
ALLOC_BUFFER=tokyo_cl 5 newyork_cl 1 toronto_cl 2
End Feature
```

在此示例中，最初根据分配的份额分配许可证。 由于设置了分配缓冲区，因此启用了基于过去使用的动态共享。 根据分配缓冲区，当集群内有需求时，toyko_cl 最快会收到许可证令牌。 分配给 toronto_cl 的最小和最大分配为10 和 50，这也占最大份额。

##### 局域网和动态广域网示例：

```shell
Begin Feature
NAME=verilog
CLUSTER_DISTRIBUTION=MyWan(c1 1/1/25 c2 1/1/30 c3 2/5/100) MyLan(c1 1)
ALLOC_BUFFER=c3 5 default 2
End Feature
```

在此示例中，verilog 许可证功能可从 WAN 和 LAN 服务域使用，但是只有集群 c1 从两个服务器都接收许可证功能。 最初根据分配的份额，分配 WAN 服务域中的许可证。 由于设置了分配缓冲区，因此启用了基于过去使用的动态共享。 当集群内有需求时，基于分配缓冲区，集群 c3 最快接收许可证令牌。



## 配置许可证特征

### 任务说明

每种许可证类型都需要 lsf.licensescheduler 文件中的 “Feature” 部分。

### 步骤

1. 使用 **NAME** 参数定义许可证管理器,用来标识许可证类型的功能名称。

   （可选）使用 **LM_LICENSE_NAME** 参数在 LSF License Scheduler 和许可证管理器特征名称之间定义别名。 来指定许可证管理器功能名称和 **NAME** 参数以定义 LSF License Scheduler 别名。

   如果 LSF License Scheduler 令牌名称与许可证管理器特征名称不同，或者对于以数字开头，或包含连字符（-）的许可证管理器特征名称 (这种方式 LSF 不支持)，则只需指定 **LM_LICENSE_NAME**。

   如果许可证管理器特征名称为 AppZ201，并且您打算使用与 LSF License Scheduler 令牌名称相同的名称，则按如下所示定义 **NAME** 参数：
   
   ```shell
   Begin Feature
   NAME=AppZ201 
   End Feature
   ```
   
   如果许可证管理器特征名称为 201-AppZ，则 LSF 不支持此功能，因为这个特征名称以数字开头并包含连字符。 因此，将 AppZ201 定义为 201-AppZ 许可证管理器特征名称的别名，如下所示：
   
   ```shell
   Begin Feature
   NAME=AppZ201
   LM_LICENSE_NAME=201-AppZ 
   End Feature
   ```
   
2. （可选）通过将 **LM_LICENSE_NAME** 中的多个许可证管理器特征名称，指定为以空格分隔的列表，将多个可互换的许可证管理器特征，组合到一个 LSF 许可证调度程序别名中。

   在此示例中，两个名为 201-AppZ 和 202-AppZ 的许可证管理器特征，组合到一个名为 AppZ201 的别名中。

   ```shell
   Begin Feature
   NAME=AppZ201
   LM_LICENSE_NAME=201-AppZ 202-AppZ
   End Feature
   ```

   AppZ201 是同时使用 201-AppZ 和 202-AppZ 令牌的组合功能。 提交带有 rusage 字符串中的 AppZ201 的作业（例如，bsub -Lp Lp1-R “rusage [AppZ201 = 2]” myjob）意味着该作业检查了 201-AppZ 或 202-AppZ 的令牌。

## 在集群模式下配置Taskman作业

### 任务说明

（可选）要在集群模式下运行 Taskman（交互式）作业，请在服务域配置中包括交互式的虚拟集群。

### 步骤

在 Feature 部分中：

1. 在 **CLUSTER_DISTRIBUTION** 参数中包括交互式的虚拟集群。
2. 为虚拟集群交互设置共享。
3. （可选）为虚拟集群交互，设置分配缓冲区以启用动态分配。

### 示例

```shell
Begin Feature
NAME=licenseA
CLUSTER_DISTRIBUTION=MyLanServer(tokyo_cl 1 interactive 1)
End Feature
```

```shell
Begin Feature
NAME=licenseB
CLUSTER_DISTRIBUTION=MyWanServer(tokyo_cl 1 newyork_cl 1 interactive 2)
End Feature
```

## 将许可证分配给非 LSF 作业

### 任务说明

仅适用于 WAN 服务域。

### 步骤

在 “Feature” 部分中设置 **WORKLOAD_DISTRIBUTION**，以分配许可证供非 LSF 使用。

```shell
WORKLOAD_DISTRIBUTION=service_domain_name(LSF lsf_distribution NON_LSF non_lsf_distribution)
```

如果在集群模式下，为 LAN 服务域设置了 **WORKLOAD_DISTRIBUTION**，则将忽略该参数。

### 示例

例如，要预留 20％ 的许可证以在 LSF 之外使用：

```shell
Begin Feature
NAME=licenseB
CLUSTER_DISTRIBUTION=MyWanServer(tokyo_cl 1 newyork_cl 1)
WORKLOAD_DISTRIBUTION=MyWanServer(LSF 8 NON_LSF 2)
End Feature
```

## 重新启动以实施配置更改

### 步骤

1. 运行 bladmin reconfig 以重新启动 bld。

2. 如果删除了任何 Feature 部分，请重新启动 mbatchd。 在这种情况下，会将一条消息写入日志文件，提示重新启动。

   如果需要，请运行 badmin mbdrestart 重新启动每个 LSF 集群。

## 查看许可证分配

### 步骤

运行 blstat -t token_name 以查看特定许可证令牌的信息（在 “Feature” 部分中配置）。

**blstat** 输出对于集群模式和项目模式有所不同。

