# 第九章 最佳实践

!!! info
    查看使用 LSF 的各种最佳实践和技巧。


## IBM Spectrum LSF 审计文件管理
LSF 使用审计文件跟踪所有已完成作业的资源分配和使用情况。这是 lsb.acct 文件的主要目的。

## 额外的配置设置
本主题描述了其他配置设置，你可以将其作为示例用于你自己的集群。其中的一些参数显式地设置为默认值，但是你可以编辑这些参数以适合你自己的集群。

## 将 CPU 分配为并行作业的块
并行作业总是需要多个 CPU 来运行。如果分配的 CPU 可以作为块分配，一些作业可以运行得更快。

## 清理 IBM Spectrum LSF 并行作业执行问题
LSF 分布式应用程序集成框架 blaunch，提供了对跨多个执行主机运行的并行作业的完全控制。

## 将 IBM Aspera 配置为数据传输工具
IBM Aspera 是一个数据传输工具，可以在高延迟网络中，基于策略，高效地使用网络带宽。

## 为 IBM Spectrum LSF 作业查询定制输出格式并减少网络流量
默认的 bjobs 命令输出信息提供了作业的基本信息。当你需要额外的作业信息时，你可能希望逐行显示作业输出。控制 bjobs 输出的格式，还可以使输出被脚本更方便地解析，也可以通过只将所需的信息从 mbatchd 传输到 bjobs 命令，来减少网络流量。

## 在 IBM Spectrum LSF 中定义基于主机的外部资源
本文描述如何在集群中的主机上，定义特定于站点的外部资源，以实现调度目的。

## 使用 Linux cgroups 来强制启用 IBM Spectrum LSF 作业内存和交换分区
在 LSF 中使用 cgroup ，以实施内存和交换分区。

## 在 IBM Spectrum LSF 中应用作业访问控制保护信息隐私
LSF访问控制级别 (ACL) 特性，在作业信息查询中支持不同级别的访问控制。

## IBM Spectrum LSF 作业目录
LSF 为要在执行期间使用的作业，使用不同类型的目录。

## 使用 IBM Spectrum LSF 和 Andrew 文件系统 (AFS)
了解 LSF 如何与 Andrew 文件系统 (AFS) 集成，以便你可以配置 LSF 以满足你的需求。

## 在高查询负载下维护集群性能
LSF 提供了基本的性能指标 (badmin perfmon)，它对三种主要的查询操作 (bjob、bhosts 和 bqueue) 进行了抽样。LSF 还提供 badmin diagnose -c query 命令选项来跟踪查询源，以便进行进一步的故障排除。

## 在 LSF 中管理浮动软件许可证
通常，浮动软件许可池由 LSF 中的数字资源表示。每个需要许可证的作业必须在其 rusage 表达式中包含许可证要求，以确保在作业被分派时，有足够的许可证可供作业使用。

## 在高查询负载下维护集群性能
!!! bug
    官网这里和上面的一个小标题重复了。
    
当启用 CPU 频率调控器时，作业在 LSF 中运行时间较长，但在机器上直接执行时运行更快时，优化 LSF 的作业处理。

## Oracle Solaris 和 IBM AIX 上的操作系统分区和虚拟化
本文介绍 LSF 在操作系统分区和虚拟化环境中的工作方式，重点关注 Oracle Solaris 容器和 IBM AIX 分区。

## mbatchd 的性能度量
LSF mbatchd 性能指标，帮助管理员在 mbatchd 性能问题发生时，确定其根本原因，以便管理员可以采取适当的纠正措施。当问题的原因与集群环境相关时，这些性能指标特别有用，例如，共享存储或网络连接的性能。

## 根据主机的可用作业槽位放置作业
LSF 内置了基于主机的资源槽，以支持基于可用作业槽的作业分配。了解如何根据打包或扩展策略，根据现有的 LSF 资源需求，来配置和使用作业资源槽。

## 下载 IBM Spectrum LSF 安装程序后，定位sha1校验和
使用 sha1 可执行文件，来验证 LSF 的安装文件。

## 追踪 IBM Spectrum LSF 中的作业依赖关系
使用 LSF 作业依赖项，在作业提交期间指定作业执行流。

## 使用计算单元，以使 IBM Spectrum LSF 在调度时考虑集群拓扑
使用 LSF 计算单元 (compute unit、CU) 特性，可以让 LSF 在调度作业时考虑树状网络拓扑。

## 使用 lsmake 加速构建 Android 源代码
LSF lsmake 工具是一个与 LSF 紧密集成的并行 GNU make 工具。

## 使用 NVIDIA DGX 系统搭配 IBM Spectrum LSF
该指南是如何在 NVIDIA DGX 系统上使用 LSF 与 GPU 资源的示例。

## 使用 ssh X11 转发 IBM Spectrum LSF
为了使 X-enabled 类型的应用程序，能够按需要工作，X connection 必须通过 ssh 进行隧道连接，这是一种安全的方法。

## 使用 IBM Spectrum LSF API 的 Python 封装
IBM Spectrum LSF APIs 的 Python 封装，允许用户通过 Python 调用 LSF 的 API 接口。你可以使用简化包装器和接口生成器(Simplified Wrapper and Interface Generator、SWIG)，来创建 Python 的封装，其中，SWIG 是用于连接 LSF C API 和 Python 的工具。