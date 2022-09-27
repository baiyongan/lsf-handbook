# LSF License Scheduler 版本之间的差异

LSF License Scheduler 有两个版本：基本版和标准版。

LSF Standard Scheduler 和 Advanced Edition 随附了 LSF License Scheduler Basic Edition，并不旨在应用有关如何在集群或项目之间共享许可证的策略。 相反，LSF License Scheduler Basic Edition 旨在代替外部负载信息管理器（**elim**），以收集由 FlexNet 或 Reprise License Manager 管理的许可证的外部负载指示。为了替代此限制，LSF License Scheduler Basic Edition 限制了单个集群的作业的许可证使用，以防止许可证的过度使用，并通过将许可证签出与这些作业匹配，来跟踪单个作业的许可证使用。

LSF License Scheduler Standard Edition 不仅提供单个集群的集群模式功能，而且还提供完整的 LSF License Scheduler 功能，包括对所有模式（集群模式，项目模式和快速分发项目模式）的支持，多个集群，功能和特性。 组，每个许可证功能有多个服务域。 LSF License Scheduler Standard Edition 还支持 **taskman** 作业，以及 LSF Advanced Edition（LSF Advanced Edition）中的 LSF/XL 功能。

##### 重要

现在需要 LSF License Scheduler 授权文件（ls.entitlement）才能运行 LSF License Scheduler Standard Edition。 在启动 LSF License Scheduler 作为标准版运行之前，将授权文件（ls.entitlement）复制到 $LSF_ENVDIR 目录。

要安装和运行 LSF License Scheduler Basic Edition，请按照 [Install License Scheduler](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/license_scheduler/install_ls.html) 中的说明，下载并安装LSF License Scheduler 软件包。但请按照安装和配置 LSF License Scheduler Basic Edition（而非 Standard Edition）的所有特定步骤进行操作。

所有 LSF License Scheduler 文档均假定使用 LSF License Scheduler Standard Edition，除非明确指明它用了 LSF License Scheduler Basic Edition。

