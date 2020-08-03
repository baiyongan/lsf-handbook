# 管理软件许可证及其他共享资源

设置LSF外部 LIM（ELIM），以将软件许可证，作为动态共享资源进行监视。

## LSF 如何使用动态共享资源

LSF 识别两种主要类型的资源：

- 基于主机的资源在集群中的所有主机上均可用，例如，主机类型和型号或节点锁定的软件许可证。
- 共享资源作为动态负载索引进行管理，可用于集群中的一组主机，例如，网络浮动软件许可证，共享文件系统。

共享的资源由一组 LSF 主机共享。 LSF 管理用于主机选择，以及批处理或交互式作业执行的共享资源。 这些资源是动态资源，因为系统上的负载随资源的可用性而变化。

## 软件许可作为共享资源

共享资源最常见的应用程序，是管理软件应用程序许可证。 您提交需要这些许可证的作业，并且在许可证可用时，LSF 会根据其优先级运行作业。 如果许可证不可用，则 LSF 将作业排队，然后在许可证免费时将其分派。 将应用程序许可证配置为共享资源，可确保最佳地使用昂贵的关键资源。

## 在 ELIM 中定义动态共享资源

为了使 LSF 使用共享资源（如软件许可证），必须在 lsf.shared 文件的 “Resource” 部分中定义资源。 您可以定义资源的类型，以及 LSF 刷新资源值的频率。

为了使 LSF 能够随着时间正确跟踪资源，必须将它们定义为外部负载索引。 LSF 使用称为外部负载信息管理器（ELIM）的程序定期更新负载索引。

ELIM 可以是 Shell 脚本或编译的二进制程序，它们返回您定义的共享资源的值。 ELIM 必须命名为 elim，并且位于 **LSF_SERVERDIR** 目录中：

```shell
/usr/share/lsf/lsf/cluser1/10.1/sparc-sol2/etc/elim
```

您可以在 misc/examples 目录中找到示例 ELIM 的示例。

## 共享许可证示例

在 lsf.shared 文件中，为软件许可证定义两个动态共享资源，名为 license1 和 license2：

```shell
Begin Resource
RESOURCENAME  TYPE    INTERVAL INCREASING  RELEASE   DESCRIPTION   # Keywords
license1      Numeric 30       N           Y         (license1 resource)
license2      Numeric 30       N           Y         (license2 resource)
End Resource
```

- 共享资源的 TYPE 参数可以是以下类型之一：

  - Numeric
  - Boolean
  
  - String
  
  在这种情况下，资源是(数字型）Numeric.
- **INTERVAL** 参数指定您希望刷新值的频率。 在此示例中，ELIM 每 30 秒更新一次共享资源 license1 和 license2 的值。

- **INCREASING** 列中的 N 表示许可证资源正在减少； 也就是说，随着更多许可证的可用，负载会降低。

-  **RELEASE** 列中的 Y 表示当使用许可证的作业被挂起时，许可证资源被释放。

## 将动态共享资源映射到主机

要使 LSF 知道所定义的动态共享资源 license1 和 license2 的位置，请将它们映射到它们所在的主机。

在 LSF_CONFDIR/lsf.cluster.cluster_name 文件中，配置 ResourceMap 部分以指定您在 LSF_CONFDIR/lsf.shared 文件中定义的共享资源 license1 和 license2 之间的映射，以及您要将它们映射到的主机：

```shell
Begin ResourceMap
RESOURCENAME  LOCATION
license1      [all]
license1      [all]
End ResourceMap
```

在此资源映射中，**LOCATION** 参数下的 [all] 属性意味着 **RESOURCENAME** 参数下的资源 license1 和 license2 在集群中的所有主机上均可用。主节点上仅需要运行一个 ELIM，因为这两个资源对于所有主机而言都是相同的。 如果资源在不同主机上的位置不同，则必须在每个主机上运行不同的 ELIM。

## 监控动态共享资源

为了使 LSF 正确接收外部负载索引，ELIM 必须以以下格式，将可用资源的计数发送到标准输出：

```shell
number_indexes [index_name index_value] ...
```

本示例中的字段包含以下信息：

```shell
2 license1 3 license2 2
```

- 外部负载指数总数 (2)
- 第一个外部负载索引的名称 (license1)
- 第一个负荷指数的值 (3)
- 第二个外部负载索引的名称 (license2)
- 第二个负荷指数 (2)

## 编写 ELIM 程序

ELIM 必须是位于 **LSF_SERVERDIR** 目录中的名为 elim 的可执行程序。

启动或重新启动 lim 守护程序时，它将在同一主机上运行 elim 程序，并获取 elim 程序发送的外部负载索引的标准输出。 通常，您可以将任何可量化资源，定义为外部负载索引，编写 ELIM 报告其值，然后将其用作 LSF 资源。

以下示例 ELIM 程序使用 license1 和 license2，并假定 FLEXlm 许可证服务器控制它们：

```shell
#!/bin/sh 
NUMLIC=2           # number of dynamic shared resources
while true
do
TMPLICS='/usr/share/lsf/cluster1/10.1/sparc-sol2/etc/lic -c 
/usr/share/lsf/cluster1/conf/license.dat -f license1, license2'

LICS='echo $TMPLICS | sed -e s/-/_/g'
echo $NUMLIC $LICS # $NUMLIC is number of dynamic shared 
resource
sleep 30           # Resource
done
```

在脚本中，**sed** 命令将许可证功能名称中的减号（-）更改为下划线（_），因为 LSF 使用减号进行计算，并且资源名称中不允许使用该减号。

lic 实用程序可从 IBM 支持获得。 您也可以使用 FLEXlm 命令 **lmstat** 来制作自己的 ELIM。

## 使用动态共享资源

要在集群中启用新的共享资源，请使用以下命令重新启动 LSF：

- **lsadmin reconfig**
- **badmin reconfig**

如果未发现错误，请使用 **lsload -l** 命令来验证动态共享资源的值：

```shell
HOST_NAME  status r15s  r1m  r15m  ut   pg   io  ls  it  tmp  swp  mem license1 license2
hosta          ok  0.1  0.3  0.4   8%   0.2  50  73   0  62M  700M 425M       3        0 
hostb          ok  0.1  0.1  0.4   4%   5.7   3   3   0  79M  204M  64M       3        0 
```

## 提交使用共享资源的作业

要提交使用一个 license1 资源的批处理作业，请使用以下命令：

```shell
% bsub -R 'rusage[license1=1:duration=1]' myjob
```

在资源需求（使用率）字符串中，duration=1 表示将 license1 保留 1 分钟，以使 LSF 有时间从 FLEXlm 中检出它。

您还可以在队列的 **RES_REQ** 参数中，在队列级别指定资源需求字符串。 在 LSB_CONFDIR/cluster_name/configdir/lsb.queues 文件中，指定以下资源需求字符串：

```shell
Begin Queue
QUEUE_NAME = license1
RES_REQ=rusage[license1=1:duration=1]
...
End Queue
```

然后，使用以下命令提交使用一个 license1 资源的批处理作业：

```shell
% bsub -q license1 myjob
```

当许可证可用时，LSF 会立即运行您的工作；当所有许可证都被使用时，LSF 会将您的作业排入队列，并在许可证可用时将其分派。 这样，您的所有许可证都将得到最大利用。

## 更多信息

- 有关 [lsf.shared](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_config_ref/lsf.shared.5.html?view=kc) 和 [lsf.cluster.cluster_name](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_config_ref/lsf.cluster.5.html?view=kc) 文件以及用于配置共享资源的参数的更多信息, 请看  [Configuration Reference](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_welcome/lsf_kc_config_ref.html?view=kc).
- 有关向集群添加外部资源以及配置 ELIM 以自定义资源的更多信息，请参阅 [Administering IBM Spectrum LSF](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_welcome/lsf_kc_managing.html?view=kc) 中的 [External load indices](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_admin/load_indices_external.html?view=kc) 。