# Summary

* [前言](README.md)

* [Chapter 1 LSF 入门](chapter1/README.md)
    
    * [1.1 LSF 功能](chapter1/introduction/function.md)
    * [1.2 LSF 架构](chapter1/introduction/architect.md)
    * [1.3 LSF 基础概念](chapter1/introduction/concept.md)
    * LSF  系统要求与兼用型
        * 操作系统支持
        * 主机选择
        * 服务器主机兼容性
        * 附加兼容性
        * API 兼容性
    * 局限性
    * [1.4 LSF 快速上手](chapter1/introduction/quick_reference.md)
    * 1.5 to be continued
    
    
    
* [Chapter 2 LSF 用户基础操作](chapter1/introduction/user_guide.md)

  * 2.1.1 LSF 概览
      * 集群组件
  * 2.1.2 LSF 细览
      * LSF 服务与进程
      * 集群通信方式
      * 容错
      * 安全
  * 2.1.3 作业负载管理
      * 作业生命周期
      * 作业提交
      * 作业调度
      * 节点选择
      * 作业运行环境
  * 2.1.4 启用 EGO 的 LSF
      * EGO 组件概览
      * 资源
      * LSF 资源共享



- Chapter 3 LSF 的安装、升级与迁移
  - 在 UNIX 与 Linux 上安装
    - 安装规划
      - LSF 集群中的 EGO
      - 主节点选择
    - 准备系统进行安装
    - 安装新的 LSF 集群
    - 从 IBM Fix Central 中获取修订
    - 配置集群
    - 非 root 用户安装
    - 往集群中添加节点
    - LSF HPC 特性
      - 可选的LSF HPC 功能配置
    - 注册服务端口
    - install.config 文件
    - slave.config 文件
  - 在 Windows 上安装
    - LSF 集群中的 EGO
    - 准备系统进行安装
      - 主节点选择
      - Entitlement files 文件
    - 安装新的 LSF 集群
    - 安装参数快速参考
  - 使用IBM Spectrum Cluster Foundation安装LSF
    - 使用IBM Spectrum Cluster Foundation安装LSF Suites 10.1.1
      - to be continued
  - 升级和迁移
    - 在UNIX和Linux上升级
      - 在 UNIX 和 Linux 上升级 LSF
      - 从IBM Fix Central获取修订
    - 在Windows上迁移
      - 在Windows上迁移LSF



- [Chapter 4 作业调度管理](chapter2/README.md)
    - 关于IBM Spectrum LSF
        - [LSF clusters, jobs, and queues](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_users_guide/clusters_jobs_about.html)
        - [Hosts](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_users_guide/hosts_about.html)
        - [LSF daemons](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_users_guide/daemons_about.html)
        - [Batch jobs and tasks](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_users_guide/batch_jobs_about.html)
        - [Host types and host models](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_users_guide/host_types_models_about.html)
        - [Users and administrators](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_users_guide/users_lsf_about.html)
        - [Resources](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_users_guide/resources_lsf_about.html)
        - [Job lifecycle](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_users_guide/job_lifecycle_lsf.html)
    - [作业运行](chapter2/use_experience/job_management/submitting.md)
      - [Submitting jobs (bsub)](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_users_guide/bsub_about.html)
        - [About submitting a job to a specific queue](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_users_guide/job_submitspecific_queue_about.html)
        - [View available queues](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_users_guide/queues_view.html)
        - [Submit a job to a queue](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_users_guide/job_submit_to_queue.html)
        - [Submit a job associated with a project (bsub -P)](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_users_guide/bsub_project.html)
        - [Submit a job associated with a user group (bsub -G)](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_users_guide/bsub_usergroup.html)
        - [Submit a job with a job name (bsub -J)](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_users_guide/bsub_jobname.html)
        - [Submit a job to a service class (bsub -sla)](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_users_guide/bsub_serviceclass.html)
        - [Submit a job under a job group (bsub -g)](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_users_guide/bsub_job_group.html)
        - [Submit a job with a JSON file (bsub -json)](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_users_guide/bsub_json_file.html)
        - [Submit a job with a YAML file (bsub -yaml)](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_users_guide/bsub_yaml_file.html)
        - [Submit a job with a JSDL file (bsub -jsdl)](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_users_guide/bsub_jsdl_file.html)
      - [Modify pending jobs (bmod)](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_users_guide/jobs_modify_pending.html)
      - [Modify running jobs](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_users_guide/jobs_running_modifying.html)
      - [About controlling jobs](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_users_guide/jobs_controlling_about.html)
        - [Kill a job (bkill)](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_users_guide/job_kill.html)
        - [About suspending and resuming jobs (bstop and bresume)](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_users_guide/jobs_suspending_resuming_about.html)
        - [Move a job to the bottom of a queue (bbot)](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_users_guide/job_move_bottom.html)
        - [Move a job to the top of a queue (btop)](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_users_guide/job_move_top.html)
        - [Control jobs in job groups](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_users_guide/job_groups_control_jobs.html)
        - [Submit a job to specific hosts](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_users_guide/job_submit_to_host.html)
        - [Submit a job with specific resources](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_users_guide/job_submit_resources_boolean.html)
        - [Queues and host preference](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_users_guide/queue_host_pref_about.html)
        - [Specify different levels of host preference](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_users_guide/host_preference_specify_level.html)
        - [Submit a job with resource requirements](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_users_guide/job_submit_resreq.html)
        - [Submit a job with SSH X11 forwarding](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_users_guide/ssh_x11_forward_job_submit.html)
      - [Using LSF with non-shared file space](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_users_guide/non_shared_about.html)
      - [About resource reservation](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_users_guide/res_rev_about.html)
        - [View resource information](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_users_guide/view_res.html)
        - [Submit a job with resource requirements](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_users_guide/job_submit_with_rusage.html)
        - [Submit a job with start or termination times](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_users_guide/job_submit_with_start_stop.html)
        - [Submit a job with compute unit resource requirements](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_users_guide/job_submit_resreq_cu.html)
      - [Set pending time limits](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_users_guide/job_pending_time_limit.html)
    - [作业监控](chapter2/use_experience/job_management/modifying.md)
      - [View information about jobs](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_users_guide/jobs_view_info.html)
        - [View unfinished jobs](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_users_guide/jobs_view_unfinished.html)
        - [View summary information of unfinished jobs](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_users_guide/jobs_view_summary_unfinished.html)
        - [View all jobs](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_users_guide/jobs_view_all.html)
        - [View running jobs](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_users_guide/jobs_view_running.html)
        - [View pending reasons for jobs](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_users_guide/jobs_view_pend_reasons.html)
        - [View job suspending reasons](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_users_guide/jobs_view_sus_reasons.html)
        - [View detailed job information](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_users_guide/jobs_view_detailed.html)
        - [View job group information](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_users_guide/job_group_info_view.html)
        - [Monitor SLA progress](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_users_guide/sla_monitor_progress.html)
        - [View job output](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_users_guide/job_output_view.html)
        - [View chronological history of jobs](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_users_guide/job_history_view_chron.html)
        - [View history of jobs not listed in active event log](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_users_guide/job_history_view_logfiles.html)
        - [View job history](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_users_guide/job_history_view.html)
        - [View the job submission environment](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_users_guide/job_environment_view.html)
        - [Update interval](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_users_guide/update_interval_about.html)
        - [Job-level information](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_users_guide/information_job_level.html)
      - [Display resource allocation limits](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_users_guide/resource_allocation_displaying_about.html)
        - [View information about resource allocation limits](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_users_guide/limits_res_alloc_view.html)



- Chapter LSF 管理员基础操作
  - 集群概览
    * 术语与概念
    * 集群特征
    * 文件系统、目录和文件
    * 重要的文件目录与配置文件
  - 使用 LSF
    * 开启、结束与重配置 LSF
    * 检查 LSF 状态
    * 运行作业
    * 管理用户、节点与队列
    * 配置 LSF 启动
    * 管理软件许可证及其他共享资源
  - LSF 排错
    * 常见 LSF 问题
    * LSF 错误信息

  

- [Chapter 5 LSF 集群维护](chapter3/README.md)

    - [Cluster management essentials](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_welcome/lsf_kc_cluster_ops.html)
    - [Monitoring cluster operations and health](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_welcome/lsf_kc_cluster_monitor.html)
    - [Managing job execution](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_welcome/lsf_kc_job_exec.html)
    - [Configuring and sharing job resources](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_welcome/lsf_kc_rsrc_share.html)
    - [GPU resources](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_welcome/lsf_kc_gpu_resources.html)
    - [Configuring containers](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_welcome/lsf_kc_containers.html)
    - [High throughput workload administration](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_welcome/lsf_kc_short_jobs.html)
    - [Parallel workload administration](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_welcome/lsf_kc_parallel.html)
    - [Security in LSF](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_welcome/lsf_kc_security.html)
    - [Advanced configuration](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_welcome/lsf_kc_adv_config.html)
    - [Performance tuning](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_welcome/lsf_kc_perf_tune.html)
    - [Energy aware scheduling](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_welcome/lsf_kc_eas.html)
    - [LSF multicluster capability](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_welcome/lsf_kc_mc.html)
    - [LSF Advanced Edition](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_welcome/lsf_kc_lsf_ae.html)



- Chapter 6 参考
  - [Command reference](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_welcome/lsf_kc_cmd_ref.html)
  - [Configuration reference](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_welcome/lsf_kc_config_ref.html)
    - [Configuration files](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_config_ref/part_files.html)
    - [Environment variables](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_config_ref/part_env.html)
      - [Environment variables set for job execution](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_config_ref/lsf_envars_job_exec.html)
      - [Environment variables for resize notification command](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_config_ref/lsf_envars_resize_cmd.html)
      - [Environment variables for session scheduler (ssched)](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_config_ref/envars_ssched.html)
      - [Environment variables for data provenance](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_config_ref/lsf_envars_data_prov.html)
      - [Environment variable reference](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_config_ref/lsf_envars_ref.html)
  - [API reference](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_welcome/lsf_kc_api_reference.html)



- [ Chapter 7 LSF 拓展](chapter4/README.md)
    * [Python API](chapter4/advanced/Python_API.md)
    * [行为分析](chapter4/advanced/Job_analysis.md)



- Chapter 8 [Best practices and tips](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_welcome/lsf_kc_best_practices_tips.html)



- 后记
  - 相关前置知识储备等	
  - 性能瓶颈分析

