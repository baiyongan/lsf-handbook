# License Scheduler 中的服务域

服务域是一组一个或多个许可证服务器。 许可证调度程序管理许可证令牌的调度，但是许可证服务器实际上提供了许可证。 您可以使用为网络提供许可证的许可证服务器名称和端口号来配置服务域。

- LAN: 为单个集群提供许可证的服务域
- WAN: 为多个集群提供许可证的服务域

License Scheduler 假定可以从 License Scheduler 接收令牌的任何用户，都可以使用服务域中的任何许可证。 因此，与分发策略中指定的项目关联的每个用户都必须满足以下要求：

- 用户可以与服务域中的每个许可证服务器主机，建立网络连接。
- 用户环境配置有权限，可以从服务域中的每个许可证服务器主机检出许可证。

您必须为许可证计划程序至少配置一个服务域。 它对为 LSF 作业提供许可证的许可证服务器主机进行分组，并在您定义在项目之间共享软件许可证的策略时使用。

如果许可证服务器不属于 License Scheduler 服务域，则其许可证不由 License Scheduler 管理（您在 LSF 中配置的许可证分发策略不适用于这些许可证，并且这些许可证的使用不会影响 LSF 调度决策）。

## 服务域位置

您可以使用许可证功能的局部性，来将功能从不同的服务域限制到特定的集群，以便许可证计划程序不将令牌授予，许可证中无法合法使用在请求令牌的集群上的许可证作业。 集群模式下使用的 LAN 服务域配置，有单集群本地性。

## 项目模式

在项目模式下，集群可以从多个服务域访问相同的许可证功能。

如果您的许可证服务器，将许可证令牌的服务限制在特定地理位置，请使用 **LOCAL_TO** 指定无法在所有位置之间共享的任何功能的许可证令牌的位置。 此参数避免了为不同的服务域定义不同的分发和分配策略，并允许分层项目组配置。

要在项目模式下使用 License Scheduler 令牌，作业提交必须指定 **-Lp **（许可证项目）选项。 必须在 lsf.licensescheduler 中为请求的功能定义项目。

## 集群模式

在集群模式下，集群中的每个许可证功能最多可以从一个 WAN 和一个 LAN 服务域访问单个许可证功能。

许可证计划程序不控制应用程序检出行为。 如果可以从 LAN 和 WAN 服务域中获得相同的许可证，则许可证计划程序希望作业首先尝试从 LAN 获取许可证。

## 并行作业

当 LSF 调度并行作业时，LSF License Scheduler 尝试检出使用用户名和所有执行主机名构造的并行作业中的 user@host密钥，并在服务域上合并相应的检出信息（如果找到）。

例如，在项目模式下，对于在服务域 sd1 中具有两个项目（P1和P2）且具有十个令牌的功能 F1，使用以下命令将并行作业分派给四个执行主机：

bsub -n 4 -Lp P1 -R "rusage[F1=4]" mycmd

每个执行主机上的作业从 sd1 服务域中签出一个 F1 许可证。 如果四个执行主机分别是 hostA，hostB，hostC 和hostD，则有 user@hostA，user@hostB，user@hostC 和 user@hostD 的签出密钥，并且每个条目都贡献一个签出的令牌。 这些令牌都合并到 F1 功能部件中的 P1 项目的数据中。 因此，运行 **blstat** 会显示 F1 功能的以下信息：

```shell
FEATURE: F1
 SERVICE_DOMAIN: LanServer
 TOTAL_INUSE: 4    TOTAL_RESERVE: 0    TOTAL_FREE: 6    OTHERS: 0
  PROJECT                 SHARE     OWN       INUSE     RESERVE   FREE      DEMAND
  P1                      50.0 %    0         4         0         1         0
  P2                      50.0 %    0         0         0         5         0
```

来自四个执行主机的四个 checkout 键合并到 P1 项目中。

如果定义了 MERGE_BY_SERVICE_DOMAIN=Y，则 LSF License Scheduler 还将合并多个 user@host 数据，以用于跨不同服务域的并行作业。

例如，如果您具有与上一个示例相同的设置，但是具有一个额外的服务域 sd2，其中也包含两个项目（P1和P2）和十个令牌，并且您定义了 MERGE_BY_SERVICE_DOMAIN=Y，则运行 **blstat** 将显示 F1 功能的以下信息：

```shell
blstat
FEATURE: F1
 SERVICE_DOMAIN: sd1
 TOTAL_INUSE: 2    TOTAL_RESERVE: 0    TOTAL_FREE: 8    OTHERS: 0
  PROJECT                 SHARE     OWN       INUSE     RESERVE   FREE      DEMAND
  P1                      50.0 %    0         2         0         3         0
  P2                      50.0 %    0         0         0         5         0
 SERVICE_DOMAIN: sd2
 TOTAL_INUSE: 2    TOTAL_RESERVE: 0    TOTAL_FREE: 8    OTHERS: 0
  PROJECT                 SHARE     OWN       INUSE     RESERVE   FREE      DEMAND
  P1                      50.0 %    0         2         0         3         0
  P2                      50.0 %    0         0         0         5         0
```

两个签出密钥合并到 sd1 域中的 P1 项目中，而两个签出密钥合并到 sd2 域中的 P1 项目中。

如果定义了 CHECKOUT_FROM_FIRST_HOST_ONLY=Y，则 LSF License Scheduler 在合并许可证使用数据时仅考虑并行作业的第一个执行主机的 user@host 信息。 在各个功能部件部分中的设置将覆盖 “Parameter” 部分中的全局设置。

如果某个功能具有多个功能部分（使用 **LOCAL_TO** ），则每个部分的  **CHECKOUT_FROM_FIRST_HOST_ONLY** 必须具有相同的设置。