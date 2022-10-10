# 第二章 LSF 基础

    
同时针对用户和管理员，关于 IBM Spectrum LSF 的工作负载管理概念及操作的概述。

## IBM Spectrum LSF 用户基础 

获取 IBM Spectrum LSF 工作负载管理概念和操作的概述。

### IBM Spectrum LSF 概述

了解 LSF 如何满足你的作业要求，并找到运行作业的最佳资源。

#### IBM Spectrum LSF 简介
IBM Spectrum LSF (“LSF”，是 load sharing facility 的缩写) 软件是业界领先的企业级软件。
LSF 跨现有的异构 IT 资源分配工作，以创建共享的、可伸缩的和容错的基础设施，从而提供更快、更可靠的工作负载性能并降低成本。LSF 平衡负载并分配资源，并提供对这些资源的访问。

#### LSF 集群组件
LSF 集群管理资源、接受和调度工作负载并监视所有事件。用户和管理员可以通过命令行界面、API 或通过 IBM Spectrum LSF 应用程序中心（IBM Spectrum LSF Application Center）访问 LSF。

### 深入 LSF 集群
了解在 LSF 主机上运行的各种守护进程、LSF 集群通信路径，以及 LSF 如何容忍集群中的主机故障。

### 深入工作负载管理
理解 LSF 作业生命周期。使用 bsub 向队列提交作业，并指定作业提交选项以修改默认作业行为。提交的作业在队列中等待，直到它们被调度并分派到主机上执行。在作业分派时，LSF 会检查哪些主机有资格运行作业。

### 启用 EGO 的 LSF
使用 LSF 启用企业网格协调器(enterprise grid orchestrator，EGO)，以提供控制和管理集群资源的系统基础设施。资源是应用程序使用的物理和逻辑实体。LSF 资源按照 EGO 资源分配计划中的定义进行共享。

## IBM Spectrum LSF 管理员基础
获取 IBM Spectrum LSF 如何管理各种类型的工作负载和集群操作的管理员概述。

### LSF 集群概述
获取集群，以及重要的 LSF 目录和配置文件位置的概述。

### 使用 LSF
启动和停止 LSF 守护进程，并重新配置集群属性。检查 LSF 状态，提交 LSF 作业。

### 排查 LSF 问题
排除常见的 LSF 问题并理解 LSF 错误消息。如果在这里找不到问题的解决方案，请联系 IBM Support。
