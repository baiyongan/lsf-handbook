# 目录

## LSF Session Scheduler
- [ ] 关于 LSF Session Scheduler
- [ ] 安装 LSF Session Scheduler
- [ ] LSF Session Scheduler 如何运行任务
- [ ] 运行和监视 LSF Session Scheduler 作业
- [ ] 故障排查

## LSF 与 Rational ClearCase
- [ ] 关于 LSF 和 ClearCase
- [ ] 在 ClearCase 中提交作业
- [ ] 在 ClearCase 中提交交互任务
- [ ] ClearCase 的 LSF 环境变量
    - [ ] CLEARCASE_DRIVE
    - [ ] CLEARCASE_MOUNTDIR
    - [ ] CLEARCASE_ROOT
    - [ ] DAEMON_WRAP_DEBUG
    - [ ] NOCHECKVIEW_POSTEXEC

## 在 Cray 的 LSF
- [ ] 下载和安装
- [ ] 配置集成
- [ ] 集成目录和文件结构
- [ ] 提交并运行作业
- [ ] 假设和限制

## LSF 与 Apache Spark
- [ ] 关于 Apache Spark 的 LSF
- [ ] 配置 Apache Spark 的集成
- [ ] 准备一个 Spark 应用程序在 LSF 上运行
- [ ] 在 LSF 上运行 Spark 应用
- [ ] 在 LSF 上运行 Spark shell


## LSF 与 Apache Hadoop
- [ ] 关于使用 Apache Hadoop 的 LSF
- [ ] 配置 Apache Hadoop 集成
- [ ] 在 LSF 上运行 Hadoop 应用程序

## LSF 与 Cluster Systems Manager
- [ ] 下载和安装
- [ ] LSF 作业与 CSM
    - [ ] 配置
    - [ ] 提交并运行作业
        - [ ] 在简单模式下提交作业
        - [ ] 在专家模式下提交作业
- [ ] 直接数据暂存作业
    - [ ] 配置
    - [ ] 提交并运行作业
- [ ] 参考
    - [ ] bsub
        - [ ] -alloc_flags
        - [ ] -cn_cu
        - [ ] -cn_mem
        - [ ] -core_isolation
        - [ ] -csm
        - [ ] -jsm
        - [ ] -ln_mem
        - [ ] -ln_slots
        - [ ] -nnodes
        - [ ] -smt
        - [ ] -stage
        - [ ] -step_cgroup
    - [ ] lsb.queues
        - [ ] CSM_REQ
    - [ ] lsf.conf
        - [ ] LSB_JSM_DEFAULT
        - [ ] LSF_STAGE_IN_EXEC
        - [ ] LSB_STAGE_MAX_STAGE_IN
        - [ ] LSB_STAGE_OUT_EXEC
        - [ ] LSB_STAGE_STORAGE
        - [ ] LSB_STAGE_TRANSFER_RATE
        - [ ] LSB_STEP_CGROUP_DEFAULT
    - [ ] lsb.params
        - [ ] CSM_VALID_SMT
        - [ ] RESCHED_UPON_CSM_SETUP_ERROR


## LSF 与 IBM Cloud Private
- [ ] 在 Linux 上安装可变使用许可

## LSF 与 IBM Spectrum Scale
- [ ] 配置 ELIM 脚本
- [ ] 配置 LSF 集群

## 使用 JSDL 提交作业
- [ ] 在 LSF 中使用 JSDL 文件
    - [ ] 使用 JSDL 文件提交作业
- [ ] 使用 elime .jsdl 收集资源值
    - [ ] 启用 JSDL 资源收集

## LSF Simulator
- [ ] 发行说明
    - [ ] 有哪些更新
    - [ ] 已知问题
- [ ] 安装
    - [ ] 启用 LSF License Scheduler
    - [ ] 使用安全方式连接外部 Elasticsearch
- [ ] 管理
- [ ] 使用
    - [ ] 实验
    - [ ] 集群配置
        - [ ] 创建集群配置包
    - [ ] 工作负载快照
        - [ ] 修改负载快照
            - [ ] 使用修改脚本
            - [ ] 使用修改插件
- [ ] 更新

## LSF Predictor
- [ ] 发行说明
    - [ ] 有哪些更新
    - [ ] 已知的问题和局限性
- [ ] 安装
    - [ ] 准备
- [ ] 连接
- [ ] 管理
- [ ] 使用
    - [ ] 调优
    - [ ] 部署模型
- [ ] 更新
- [ ] 数据和日志
