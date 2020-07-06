# Summary

* [前言](README.md)

## Part I 入门介绍篇
* [Chapter 1 LSF 介绍](chapter1/LSF_introduction.md)
    * [1.1 LSF 功能](chapter1/section1/function.md)
    * [1.2 LSF 架构](chapter1/section2/architect.md)
    * [1.3 LSF 基础概念](chapter1/section3/concept.md)
    * 1.4 LSF 系统要求与兼用型
        * 操作系统支持
        * 主机选择
        * 服务器主机兼容性
        * 附加兼容性
        * API 兼容性
    * 1.5 局限性
    * 1.6 版本更新
    * [1.7 LSF 快速上手](chapter1/section7/LSF_quick_reference.md)

-----
* [Chapter 2 安装、升级与迁移](chapter2/install_upgrade_and_migrate.md)
    * 2.1 在 UNIX 与 Linux 上安装
        * 安装规划
            * LSF 集群中的 EGO
            * 主节点选择
        * 准备系统进行安装
        * 安装新的 LSF 集群
        * 从 IBM Fix Central 中获取修订
        * 配置集群
        * 非 root 用户安装
        * 往集群中添加节点
        * LSF HPC 特性
            * 可选的LSF HPC 功能配置
        * 注册服务端口
        * install.config 文件
        * slave.config 文件
    * 2.2 在 Windows 上安装
        * LSF 集群中的 EGO
        * 准备系统进行安装
            * 主节点选择
            * Entitlement files 文件
        * 安装新的 LSF 集群
        * 安装参数快速参考
    * 2.3 使用IBM Spectrum Cluster Foundation安装LSF
        * 使用IBM Spectrum Cluster Foundation安装LSF Suites 10.1.1
            * to be continued
    * 2.4 升级和迁移
        * 在UNIX和Linux上升级
            * 在 UNIX 和 Linux 上升级 LSF
            * 从IBM Fix Central获取修订
        * 在Windows上迁移
            * 在Windows上迁移LSF

## Part II 基础操作篇
* [Chapter 3 用户操作基础](chapter3/user_fundations.md)
    * [3.1 LSF 概览](chapter3/section1/LSF_overview.md)
        * [集群组件](chapter3/section1/cluster_components.md)
    * [3.2 LSF 细观](chapter3/section2/Inside_an_LSF_cluster.md)
        * [LSF 服务与进程](chapter3/section2/LSF_daemons_and_processes.md)
        * [集群通信方式](chapter3/section2/cluster_communication_paths.md)
        * [容错](chapter3/section2/falut_tolerance.md)
        * [安全](chapter3/section2/security.md)
    * [3.3 作业负载管理](chapter3/section3/inside_workload_management.md)
        * [作业生命周期](chapter3/section3/job_lifecycle.md)
        * [作业提交](chapter3/section3/job_submission.md)
        * [作业调度](chapter3/section3/job_scheduling_and_dispatch.md)
        * [节点选择](chapter3/section3/host_selection.md)
        * [作业运行环境](chapter3/section3/job_execution_environment.md)
    * [3.4 启用 EGO 的 LSF](chapter3/section4/LSF_with_EGO_enabled.md)
        * [EGO 组件概览](chapter3/section4/EGO_component_overview.md)
        * [资源](chapter3/section4/resources.md)
        * [LSF 资源共享](chapter3/section4/LSF_resource_sharing.md)

-----
* [Chapter 4 管理员操作基础](chapter4/administrator_fundations.md)
    * [4.1 集群概览](chapter4/section1/cluster_overview.md)
        * [术语与概念](chapter4/section1/terms_and_concepts.md)
        * [集群特征](chapter4/section1/cluster_characteristics.md)
        * [文件系统、目录和文件](chapter4/section1/filesystems_directories_and_files.md)
        * [重要的文件目录与配置文件](chapter4/section1/important_directories_and_configuration_files.md)
    * [4.2 使用 LSF](chapter4/section2/work_with_LSF.md)
        * [开启、结束与重配置 LSF](chapter4/section2/start_stop_and_reconfigure_LSF.md)
        * [检查 LSF 状态](chapter4/section2/check_LSF_status.md)
        * [运行作业](chapter4/section2/run_jobs.md)
        * [管理用户、节点与队列](chapter4/section2/manage_users_hosts_and_queues.md)
        * [配置 LSF 启动](chapter4/section2/configure_LSF_startup.md)
        * [管理软件许可证及其他共享资源](chapter4/section2/manage_software_licenses_and_other_resources.md)
    * [4.3 LSF 排错](chapter4/section3/troubleshooting_LSF_problems.md)
        * [常见 LSF 问题](chapter4/section3/solving_common_LSF_problems.md)
        * [LSF 错误信息](chapter4/section3/LSF_error_messages.md)

## Part III 作业调度篇
* [Chapter 5 作业调度管理](chapter5/run_jobs.md)
    * [5.1 关于 IBM Spectrum LSF](chapter5/section1/about_IBM_Spectrum_LSF.md)
        * [LSF 集群，作业与队列](chapter5/section1/LSF_clusters_jobs_and_queues.md)
        * [节点](chapter5/section1/hosts.md)
        * [LSF daemons](chapter5/section1/LSF_daemons.md)
        * [Batch jobs and tasks](chapter5/section1/Batch_jobs_and_tasks.md)
        * [Host types and host models](chapter5/section1/Host_types_and_host_models.md)
        * [Users and administrators](chapter5/section1/Users_and_administrators.md)
        * [Resources](chapter5/section1/Resources.md)
        * [Job lifecycle](chapter5/section1/Job_lifecycle.md)
    * [5.2 作业运行](chapter5/section2/working_with_jobs.md)
        * [Submitting jobs (bsub)](chapter5/section2/submitting_jobs_using_bsub.md)
            * About submitting a job to a specific queue
            * View available queues
            * Submit a job to a queue
            * Submit a job associated with a project (bsub -P)
            * Submit a job associated with a user group (bsub -G)
            * Submit a job with a job name (bsub -J)
            * Submit a job to a service class (bsub -sla)
            * Submit a job under a job group (bsub -g)
            * Submit a job with a JSON file (bsub -json)
            * Submit a job with a YAML file (bsub -yaml)
            * Submit a job with a JSDL file (bsub -jsdl)
        * Modify pending jobs (bmod)
        * Modify running jobs
        * About controlling jobs
            * Kill a job (bkill)
            * About suspending and resuming jobs (bstop and bresume)
            * Move a job to the bottom of a queue (bbot)
            * Move a job to the top of a queue (btop)
            * Control jobs in job groups
            * Submit a job to specific hosts
            * Submit a job with specific resources
            * Queues and host preference
            * Specify different levels of host preference
            * Submit a job with resource requirements
            * Submit a job with SSH X11 forwarding
        * Using LSF with non-shared file space
        * About resource reservation
            * View resource information
            * Submit a job with resource requirements
            * Submit a job with start or termination times
            * Submit a job with compute unit resource requirements
        * Set pending time limits
    * [5.3 作业监控](chapter5/section3/monitoring_jobs.md)
        * [View information about jobs](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_users_guide/jobs_view_info.html)
            * [View unfinished jobs](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_users_guide/jobs_view_unfinished.html)
            * [View summary information of unfinished jobs](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_users_guide/jobs_view_summary_unfinished.html)
            * [View all jobs](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_users_guide/jobs_view_all.html)
            * [View running jobs](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_users_guide/jobs_view_running.html)
            * [View pending reasons for jobs](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_users_guide/jobs_view_pend_reasons.html)
            * [View job suspending reasons](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_users_guide/jobs_view_sus_reasons.html)
            * [View detailed job information](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_users_guide/jobs_view_detailed.html)
            * [View job group information](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_users_guide/job_group_info_view.html)
            * [Monitor SLA progress](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_users_guide/sla_monitor_progress.html)
            * [View job output](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_users_guide/job_output_view.html)
            * [View chronological history of jobs](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_users_guide/job_history_view_chron.html)
            * [View history of jobs not listed in active event log](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_users_guide/job_history_view_logfiles.html)
            * [View job history](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_users_guide/job_history_view.html)
            * [View the job submission environment](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_users_guide/job_environment_view.html)
            * [Update interval](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_users_guide/update_interval_about.html)
            * [Job-level information](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_users_guide/information_job_level.html)
        * [Display resource allocation limits](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_users_guide/resource_allocation_displaying_about.html)
            * [View information about resource allocation limits](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_users_guide/limits_res_alloc_view.html)

## Part IV 集群运维篇
* [Chapter 6 LSF 集群维护管理](chapter6/Administer_LSF.md)
    * [6.1 Cluster management essentials](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_welcome/lsf_kc_cluster_ops.html)
    * [6.2 Monitoring cluster operations and health](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_welcome/lsf_kc_cluster_monitor.html)
    * [6.3 Managing job execution](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_welcome/lsf_kc_job_exec.html)
    * [6.4 Configuring and sharing job resources](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_welcome/lsf_kc_rsrc_share.html)
    * [6.5 GPU resources](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_welcome/lsf_kc_gpu_resources.html)
    * [6.6 Configuring containers](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_welcome/lsf_kc_containers.html)
    * [6.7 High throughput workload administration](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_welcome/lsf_kc_short_jobs.html)
    * [6.8 Parallel workload administration](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_welcome/lsf_kc_parallel.html)
    * [6.9 Security in LSF](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_welcome/lsf_kc_security.html)
    * [6.10 Advanced configuration](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_welcome/lsf_kc_adv_config.html)
    * [6.11 Performance tuning](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_welcome/lsf_kc_perf_tune.html)
    * [6.12 Energy aware scheduling](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_welcome/lsf_kc_eas.html)
    * [6.13 LSF multicluster capability](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_welcome/lsf_kc_mc.html)
    * [6.14 LSF Advanced Edition](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_welcome/lsf_kc_lsf_ae.html)

-----
* [Chapter 7 参考文档](chapter7/Reference.md)
    * [7.1 Command reference](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_welcome/lsf_kc_cmd_ref.html)
    * [7.2 Configuration reference](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_welcome/lsf_kc_config_ref.html)
        * [Configuration files](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_config_ref/part_files.html)
        * [Environment variables](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_config_ref/part_env.html)
            * [Environment variables set for job execution](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_config_ref/lsf_envars_job_exec.html)
            * [Environment variables for resize notification command](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_config_ref/lsf_envars_resize_cmd.html)
            * [Environment variables for session scheduler (ssched)](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_config_ref/envars_ssched.html)
            * [Environment variables for data provenance](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_config_ref/lsf_envars_data_prov.html)
            * [Environment variable reference](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_config_ref/lsf_envars_ref.html)
    * [7.3 API reference](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_welcome/lsf_kc_api_reference.html)

## Part V 功能拓展篇
* [ Chapter 8 LSF 拓展](chapter8/Extend_LSF.md)
    * [LSF Session Scheduler](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_welcome/lsf_kc_ss.html)
    * [LSF with Rational ClearCase](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_welcome/lsf_kc_clearcase.html)
    * [LSF on Cray](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_welcome/lsf_kc_cray.html)
    * [LSF with Apache Spark](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_welcome/lsf_kc_spark.html)
    * [LSF with Apache Hadoop](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_welcome/lsf_kc_hadoop.html)
    * [LSF with Cluster Systems Manager](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_welcome/lsf_kc_csm.html)
    * [LSF with IBM Cloud Private](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_welcome/lsf_kc_icp.html)
    * [LSF Job Step Manager](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/jsm/jsm_kickoff.html)
    * [Submitting jobs using JSDL](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_admin/appendix_jsdl_lsf_admin.html)
    * [LSF Simulator](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_welcome/lsf_kc_simulator.html)

-----
* [Chapter 9 最佳实践与建议](chapter9/Best_practices_and_tips.md)
    * [Accounting file management](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/best_practices/Accounting file management.html)
    * [Allocating CPUs as blocks for parallel jobs](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/best_practices/allocating_cpu_block_parallel_jobs.html)
    * [Cleaning up parallel job execution problems](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/best_practices/Cleaning up parallel job execution problems.html)
    * [Configuring IBM Aspera as a data transfer tool](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/dm_using/dm_aspera.html?pos=2)
    * [Customizing job query output format](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/best_practices/Customizing job query output format.html)
    * [Defining external host-based resources](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/best_practices/Defining external host-based resources.html)
    * [Enforcing job memory and swap with Linux cgroups](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/best_practices/Enforcing job memory and swap with Linux cgroups.html)
    * [Job access control](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/best_practices/Job access control in LSF.html)
    * [Integration with AFS](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/best_practices/afs_integration.html)
    * [Maintaining cluster performance](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/best_practices/Maintaining cluster performance.html)
    * [Managing floating software licenses](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/best_practices/floating_software_licenses.html)
    * [Optimizing LSF job processing with CPU frequency governors enabled](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/best_practices/Optimizing LSF job processing with CPU frequency governors enabled.html)
    * [OS partitioning and virtualization on Oracle Solaris and IBM AIX](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/best_practices/os_partition_vm_solaris_aix.html)
    * [Placing jobs based on available job slots of hosts](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/best_practices/Placing jobs based on available job slots of hosts.html)
    * [Running checksum to verify installation images](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/best_practices/Running checksum to verify installation images.html)
    * [Tracking job dependencies](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/best_practices/Tracking job dependencies in LSF.html)
    * [Understanding mbatchd performance metrics](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/best_practices/Understanding mbatchd performance metrics.html)
    * [Using compute units for topology scheduling](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/best_practices/Using compute units for topology scheduling.html)
    * [Using job directories](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/best_practices/Using job directories.html)
    * [Using lsmake to accelerate Android builds](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/best_practices/Using lsmake to accelerate Android builds.html)
    * [Using NVIDIA DGX systems with LSF](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/best_practices/Using NVIDIA DGX systems with IBM Spectrum LSF.html)
    * [Using ssh X11 forwarding](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/best_practices/ssh_x11_forwarding.html)
    * [Using the Python wrapper for LSF API](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/best_practices/Using the Python wrapper for LSF API.html)

## Part VI 经验总结篇
* Chapter10
* Chapter11
* Chapter12

-----
* [后记](NOTE.md)

