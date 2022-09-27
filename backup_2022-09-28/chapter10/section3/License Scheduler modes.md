# License Scheduler 模式

配置许可证计划程序的安装时，必须选择最适合您使用的每个许可证的项目模式和集群模式。 可以在一个安装中配置项目模式和集群模式，但是，作业所需的所有不同许可证必须属于同一模式。

- ##### 集群模式

  将许可证令牌，分发到由 LSF 计划接管的集群。

  ![img](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/license_scheduler/cluster_mode_ls.jpg)

  集群模式强调许可证令牌的高利用率，而不要考虑所有权等其他因素。 许可证所有权和共享仍然可以配置，但是可以在每个集群中进行配置，而不是跨多个集群进行配置。 作业（和许可证）的抢占也发生在每个集群中，而不是跨集群。作业完成后，许可证令牌将由 LSF 重用，而无需等待 **lmstat** 或 **rlmstat** 确认许可证令牌可用，并且在下一个 **blcollect** 周期中报告。 这将提高短期作业的许可证利用率。许可证调度程序 8.0 中引入了集群模式。

- ##### 项目模式

  将许可证令牌，分发给跨所有集群配置的项目。
  
  ![img](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/license_scheduler/proj_mode_ls.jpg)
  
  项目模式强调跨多个集群的特定项目对许可证令牌的所有权。 当 License Scheduler 在项目模式下运行时，License Scheduler 在项目模式下分配许可证令牌之前，会检查所有 LSF 集群中许可证所有者的需求。 收集和评估所有集群中所有项目的需求的过程，会减慢每个计划周期。 在 **lmstat** 或 **rlmstat** 确认许可证令牌可用性之后，许可证令牌将在下一个调度周期中分发。在 License Scheduler 8.0 之前，只能使用项目模式。

## 集群模式和项目模式之间的区别

下图说明了具有相应 **lmstat** 或 **rlmstat** 报告时间的短作业，在**集群模式**下的许可证利用率：

![img](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/license_scheduler/ls_cluster_mode_alloc.jpg)

在集群模式下，当一个作业完成运行时，下一个作业将立即获得其许可证，而不必等待下一个 **lmstat** 或 **rlmstat** 间隔。 例如，需要许可证 2 的四个作业可以运行，而无需等待 **lmstat** 或 **rlmstat** 报告令牌分配。

下图说明了具有 **lmstat** 或 **rlmstat** 报告时间的短期作业，在**项目模式**下的许可证利用率：

![img](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/license_scheduler/ls_project_mode_alloc.jpg)

在项目模式下，每个作业必须等待 **lmstat** 或 **rlmstat** 报告令牌分配，然后才能获得许可证并开始运行。 在此示例中，需要许可证 2 的三个作业，能够在所示的 **lmstat** 或 **rlmstat** 间隔内启动。

## 何时使用集群模式

在以下情况下，集群模式最适合您的需求：

- 您的主要目标是最大限度地使用许可证。
- 许可证的所有权是次要的考虑因素。
- 相对于 **blcollect** 周期（默认为 60 秒，由 **LM_STAT_INTERVAL** 设置）而言，许多作业时间较短。

## 何时使用项目模式

如果满足以下条件，则项目模式最适合您的需求：

- 您的主要目标是确保小组的所有权。
- 最大化使用许可证是次要考虑因素。
- 大多数作业相对于 **blcollect** 周期较长（默认为 60 秒，由 **LM_STAT_INTERVAL** 设置）。