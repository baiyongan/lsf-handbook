# 第九章 最佳实践

!!! info    
  查看使用 LSF 的各种最佳实践和技巧。

- ##### 会计文件管理

  **[Accounting file management](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/best_practices/Accounting file management.html?view=kc)**

- ##### 将 CPU 分配为并行作业的块

  **[Allocating CPUs as blocks for parallel jobs](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/best_practices/allocating_cpu_block_parallel_jobs.html?view=kc)**
  并行作业始终要求运行多个CPU。 如果可以将分配的CPU分配为块，则某些作业可以运行得更快。

- ##### 清理并行作业执行问题

  **[Cleaning up parallel job execution problems](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/best_practices/Cleaning up parallel job execution problems.html?view=kc)**

- ##### 将 IBM Aspera 配置为数据传输工具

  **[Configuring IBM Aspera as a data transfer tool](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/dm_using/dm_aspera.html?view=kc)**
  IBM Aspera 是一种数据传输工具，可以在高延迟网络中高效，基于策略地使用网络带宽。

- ##### 自定义作业查询输出格式

  **[Customizing job query output format](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/best_practices/Customizing job query output format.html?view=kc)**

- ##### 定义基于主机的外部资源

  **[Defining external host-based resources](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/best_practices/Defining external host-based resources.html?view=kc)**

- ##### 加强作业内存并与 Linux cgroup 交换

  **[Enforcing job memory and swap with Linux cgroups](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/best_practices/Enforcing job memory and swap with Linux cgroups.html?view=kc)**

- ##### 作业访问控制

  **[Job access control](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/best_practices/Job access control in LSF.html?view=kc)**

- ##### 将IBM Spectrum LSF与Andrew File System（AFS）结合使用

  **[Using IBM Spectrum LSF with Andrew File System (AFS)](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/best_practices/afs_integration.html?view=kc)**
  了解 LSF 如何与 Andrew File System（AFS）集成，以便您可以配置 LSF 以适合您的需求。

- ##### 维持集群性能

  **[Maintaining cluster performance](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/best_practices/Maintaining cluster performance.html?view=kc)**

- ##### 在 LSF 中管理浮动软件许可证

  **[Managing floating software licenses in LSF](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/best_practices/floating_software_licenses.html?view=kc)**
  通常，浮动软件许可证池由 LSF 中的数字资源表示。 每个需要许可证的工作都必须在其 **rusag** 表达式中包括许可证要求，以确保在分发工作时为该工作释放了足够的许可证。

- ##### 在启用 CPU 频率调节器的情况下优化 LSF 作业处理

  **[Optimizing LSF job processing with CPU frequency governors enabled](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/best_practices/Optimizing LSF job processing with CPU frequency governors enabled.html?view=kc)**

- ##### Oracle Solaris 和 IBM AIX 上的操作系统分区和虚拟化

  **[Operating system partitioning and virtualization on Oracle Solaris and IBM AIX](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/best_practices/os_partition_vm_solaris_aix.html?view=kc)**
  本文介绍了 LSF 在 OS 分区和虚拟化环境中的工作方式，重点是 Oracle Solaris 容器和 IBM AIX 分区。

- ##### 基于主机的可用作业位置放置作业

  **[Placing jobs based on available job slots of hosts](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/best_practices/Placing jobs based on available job slots of hosts.html?view=kc)**

- ##### 运行 checksum 以验证安装映像

  **[Running checksum to verify installation images](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/best_practices/Running checksum to verify installation images.html?view=kc)**

- ##### 跟踪作业依赖性

  **[Tracking job dependencies](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/best_practices/Tracking job dependencies in LSF.html?view=kc)**

- ##### 了解 mbatchd 的性能指标

  **[Understanding mbatchd performance metrics](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/best_practices/Understanding mbatchd performance metrics.html?view=kc)**

- ##### 使用计算单元进行拓扑调度

  **[Using compute units for topology scheduling](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/best_practices/Using compute units for topology scheduling.html?view=kc)**

- ##### 使用作业目录

  **[Using job directories](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/best_practices/Using job directories.html?view=kc)**

- ##### 使用 lsmake 加速 Android 构建

  **[Using lsmake to accelerate Android builds](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/best_practices/Using lsmake to accelerate Android builds.html?view=kc)**

- ##### 将 NVIDIA DGX 系统与 LSF 一起使用

  **[Using NVIDIA DGX systems with LSF](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/best_practices/Using NVIDIA DGX systems with IBM Spectrum LSF.html?view=kc)**

- ##### 将 ssh X11 转发与 IBM Spectrum LSF 一起使用

  **[Using ssh X11 forwarding with IBM Spectrum LSF](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/best_practices/ssh_x11_forwarding.html?view=kc)**
  为了使启用 X 的应用程序能够按预期运行，必须通过 **ssh** 来建立 X 连接，这是一种安全的方法。

- ##### 为LSF API 使用 Python wrapper

  ##### **[Using the Python wrapper for LSF API](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/best_practices/Using the Python wrapper for LSF API.html?view=kc)**

