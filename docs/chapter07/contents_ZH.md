# 目录

## 在 Windows 上使用 LSF
- [ ] 测试你的 LSF 安装
- [ ] LSF 默认用户映射
- [ ] 环境
- [ ] 使用 Windows 性能监视器绘制资源图表
- [ ] LSF 主机动态 IP 寻址
- [ ] 使用微软终端服务在 LSF 中显示 GUI
- [ ] 混合集群中安装 LSF

## LSF License Scheduler
   
### 介绍
- [ ] 概述
- [ ] LSF License Scheduler 版本之间的差异
- [ ] 词汇表
- [ ] 架构

### 安装和启动许可证调度程序
- [ ] 安装许可证调度程序
    - [ ] 安装前
    - [ ] License Scheduler 的设置脚本做些什么
    - [ ] 安装许可证调度程序与 LSF (UNIX) 
    - [ ] 在 Windows 上安装许可证调度程序
        - [ ] 安装许可证调度程序与 LSF (Windows)
    - [ ] 排查故障
    - [ ] 配置 LSF License Scheduler 基本版
- [ ] 启动License Scheduler
- [ ] License Scheduler 中的 LSF 参数
- [ ] 关于提交作业
- [ ] 配置变更后
- [ ] 添加集群到 License Scheduler
- [ ] 配置多个管理员
- [ ] 升级许可证调度程序
- [ ] 防火墙

### LSF License Scheduler 概念
- [ ] License Scheduler 模式
- [ ] 项目组
- [ ] License Scheduler 中的服务域
- [ ] 分发策略
- [ ] 项目模式抢占
    - [ ] 抢占限制
    - [ ] LSF 抢占与 License Scheduler 抢占
- [ ] FlexNet 和 Reprise License Manager 的 License 使用
    - [ ] 已知许可证要求
    - [ ] 未知的许可证要求
    - [ ] 项目模式
    - [ ] 集群模式
    - [ ] 保留 FlexNet Manager 许可证

### 配置 License Scheduler
- [ ] 配置集群模式
- [ ] 配置有保证的集群模式
- [ ] 项目的项目模式
- [ ] 项目组的项目模式
- [ ] 项目模式可选设置
    - [ ] 主动所有权
    - [ ] 默认项目
    - [ ] 项目组
        - [ ] 配置组 license 的所有权
    - [ ] 互动 (taskman) 作业
    - [ ] 集群和交互分配
    - [ ] 特性组
        - [ ] 查看 license 特征组信息
    - [ ] License 特性的位置
        - [ ] 提交使用本地的作业
        - [ ] 本地如何与其他设置一起工作
    - [ ] 分层的项目组路径
    - [ ] 需求限制
    - [ ] 配置 lmremove 或 rlmremove 抢占
    - [ ] 重启执行配置更改
- [ ] 快速调度项目模式
    - [ ] 配置 lmremove 或 rlmremove 抢占
- [ ] 自动时间配置
    - [ ] 故障转移
    - [ ] LANs 的故障切换配置
    - [ ] WANs 的故障切换配置
        - [ ] 在 WAN 中配置并启动 License Scheduler
        - [ ] WAN 示例
        - [ ] 主机和网络级别的服务发放
    - [ ] 设置 fod
- [ ] 用户认证

### 查看信息和排查故障
- [ ] 关于查看可用 license
    - [ ] 查看传递给作业的 license server 和 license feature 信息
    - [ ] 自定义动态 license 信息输出
- [ ] 关于错误日志
    - [ ] 管理日志文件
    - [ ] 临时修改日志级别
- [ ] 故障排除
    - [ ] 文件位置
    - [ ] 检查 blcollect 是否支持 lmstat
    - [ ] 除非定义了 LSF 许可调度程序 elim，否则不删除 lsb.tokens

### Ref参考erence
- [ ] lsf.licensescheduler
    - [ ] bladmin
    - [ ] blcollect
    - [ ] blcstat
    - [ ] blhosts
    - [ ] blinfo
    - [ ] blkill
    - [ ] blparams
    - [ ] blstat
    - [ ] bltasks
    - [ ] blusers
    - [ ] fod.conf
    - [ ] fodadmin
    - [ ] fodapps
    - [ ] fodhosts
    - [ ] fodid
    - [ ] taskman


## LSF Data Manager
   
### 关于 IBM Spectrum LSF Data Manager
- [ ] 概念和术语
- [ ] LSF 数据管理器如何工作
    - [ ] 单集群实现
    - [ ] LSF 多集群能力实现

### 计划并安装 IBM Spectrum LSF Data Manager
- [ ] 计划安装
- [ ] 安装 LSF Data Manager
    - [ ] 安装 LSF
    - [ ] 安装 LSF Data Manager
    - [ ] 配置 LSF data manager 参数
    - [ ] 安装验证

### 使用 LSF Data Manager
- [ ] 提交和管理有数据需求的作业
    - [ ] 指定任务的数据需求
    - [ ] 创建数据规格文件
    - [ ] 分段数据
        - [ ] Staging data in
        - [ ] Staging data out
    - [ ] 数据需求工作流的数据标签
        - [ ] 数据标签的指定规则
        - [ ] 创建和使用数据标签
        - [ ] 数据标签示例
        - [ ] 监控数据标签
        - [ ] 清理数据标签
    - [ ] 修改数据作业
    - [ ] 传输数据需求文件
        - [ ] 环境变量
    - [ ] 指定用户组
    - [ ] 允许其他用户访问您的文件
- [ ] 查询有数据需求的作业
    - [ ] 查询数据缓存
        - [ ] 示例数据需求查询
    - [ ] 查询数据标签
    - [ ] 查询数据作业
    - [ ] 查看数据作业的历史信息

### 管理 LSF Data Manager
- [ ] 管理 dmd
    - [ ] 显示 LSF 数据管理器配置
    - [ ] 重新配置 LSF 数据管理器
    - [ ] 关闭 LSF 数据管理器
    - [ ] 配置故障切换
- [ ] 管理暂存区(缓存)
    - [ ] 配置数据暂存区
    - [ ] 分段区域文件结构
    - [ ] 远程文件访问
    - [ ] 允许用户控制对其文件的访问
- [ ] 管理数据传输
    - [ ] 数据传输任务
        - [ ] 监控数据传输任务
    - [ ] 传输队列概述
        - [ ] 配置数据传输队列
        - [ ] 管理数据传输队列
    - [ ] 管理数据传输节点
    - [ ] 处理数据传输任务失败的故障排查
    - [ ] 数据传输任务的脚本接口
    - [ ] 配置 IBM Aspera 作为数据传输工具
    - [ ] 使用 bsub -f 启用数据需求文件传输
        - [ ] esub.datamanager 脚本
        - [ ] lsrcp.wrapper.datamanager 脚本
- [ ] 数据规范文件
    - [ ] 数据规范文件格式
- [ ] 配置 LSF Data Manager 使用 LSF 多集群能力
    - [ ] 在 LSF 数据管理器中建立 IBM Spectrum LSF 多集群能力作业转发
    - [ ] 显示 LSF 数据管理器连接
    - [ ] 对有数据需求的远程作业选择集群
    - [ ] 跨多个集群的中间数据标签
    - [ ] 查询远程 LSF 数据管理器信息
    - [ ] 优化本地 stage in
    - [ ] 多个集群的单一数据管理器

### 命令参考
- [ ] bsub
    - [ ] 选项
        - [ ] -data
        - [ ] -datagrp
        - [ ] -stage
- [ ] bdata
    - [ ] 概述
    - [ ] 子命令
        - [ ] cache
        - [ ] chgrp
        - [ ] chmod
        - [ ] tags
        - [ ] showconf
        - [ ] connections
        - [ ] admin
    - [ ] 帮助和版本显示
    - [ ] 另请参阅
- [ ] bjobs
    - [ ] 选项
        - [ ] -data
- [ ] bstage
    - [ ] bstage in
    - [ ] bstage out
    - [ ] 帮助和版本显示
    - [ ] 另请参阅

### 配置参考
- [ ] lsb.queues
    - [ ] DATA_TRANSFER
- [ ] lsf.conf
    - [ ] LSB_TIME_DMD
    - [ ] LSF_DATA_HOSTS
    - [ ] LSF_DATA_PORT
    - [ ] LSF_DATA_SKIP_GROUP_CHECK
    - [ ] LSF_STAGE_IN_EXEC
    - [ ] LSB_STAGE_OUT_EXEC
    - [ ] LSB_STAGE_STORAGE
    - [ ] LSB_STAGE_TRANSFER_RATE
- [ ] lsf.datamanager
    - [ ] lsf.datamanager Parameters section
    - [ ] RemoteDataManagers section

## LSF resource connnector

### LSF resource connector 概述

### 配置 resource providers
- [ ] 设置初始配置
- [ ] 配置多个资源提供程序
- [ ] 配置不同的模板创建实例
- [ ] 为模板分配独占资源
- [ ] 配置 IBM Spectrum Conductor with Spark 与 LSF 资源连接器
    - [ ] 管理资源共享和分配
    - [ ] 在计算主机上安装 LSF
    - [ ] 为使用 Spark 的 IBM Spectrum Conductor 配置资源连接器
    - [ ] 向 EGO 提交工作
        - [ ] LSF 如何将主机返回给 EGO
- [ ] 配置 IBM Bluemix 与 LSF 资源连接器
    - [ ] 配置 IBM Bluemix 的 LSF 资源连接器
    - [ ] 向 IBM Bluemix 提交作业
- [ ] 配置 OpenStack 与 LSF 资源连接器
    - [ ] 配置 OpenStack 的 DNS 服务器
    - [ ] 为 OpenStack 配置资源连接器
    - [ ] 向 OpenStack 提交作业
        - [ ] LSF 如何将主机返回给 OpenStack
- [ ] 配置 Microsoft Azure 与 LSF 资源连接器
    - [ ] 配置 Microsoft Azure 的 LSF 资源连接器
    - [ ] 更新 Microsoft Azure 的 LSF 配置
    - [ ] 向 Microsoft Azure 提交作业
    - [ ] 添加多个 Azure providers
- [ ] 配置 Microsoft Azure CycleCloud 与 LSF 资源连接器
    - [ ] 配置 Microsoft Azure CycleCloud 的 LSF 资源连接器
    - [ ] 更新 Microsoft Azure CycleCloud 的 LSF 配置
    - [ ] 向 Microsoft Azure CycleCloud 提交作业
- [ ] 配置 Google Cloud Platform 与 LSF resource connector
    - [ ] 配置 Google Cloud Platform 的 LSF 资源连接器
    - [ ] 向 Google Cloud Platform 提交作业 
- [ ] 配置 Amazon Web Services 与 LSF resource connector
    - [ ] 准备配置 AWS
    - [ ] 构建云映像
        - [ ] 准备 Amazon Web Services 组件
        - [ ] 启动 Amazon Web Services EC2 实例
        - [ ] 在 AWS EC2 实例上安装 LSF 服务器主机
    - [ ] 启用 Amazon Web Services (AWS) 的 LSF 资源连接器
        - [ ] aws_enable.sh 脚本
        - [ ] 选择账号鉴权方式
        - [ ] 为 LSF 执行 AWS 启用脚本
        - [ ] 完成对 AWS 资源连接器的启用
            - [ ] 配置用户脚本注册 AWS 主机
    - [ ] 配置 Bursting 行为
        - [ ] 配置阈值
        - [ ] 提供具体的策略配置
        - [ ] 控制回收行为
    - [ ] 为模板分配独占资源
    - [ ] 使用 federated accounts 配置 AWS 访问
    - [ ] 配置 AWS 启动模板
    - [ ] 附加 EFA 网络接口
    - [ ] 使用 AWS 现场实例
        - [ ] 配置 AWS Spot 实例
    - [ ] 向 AWS 提交作业
        - [ ] LSF 如何将主机返回给 AWS
- [ ] 配置 OpenShift 与 LSF 资源连接器
    - [ ] 启用 OpenShift 的 LSF 资源连接器
    - [ ] 向 OpenShift 提交作业
- [ ] 配置 IBM Cloud Gen 2 与 LSF 资源连接器
    - [ ] 为 LSF 资源连接器准备 IBM Cloud Gen 2
    - [ ] 配置 IBM Cloud Gen 2 的 LSF 资源连接器
    - [ ] 向 IBM Cloud Gen 2 提交作业

### 更新资源连接器的 LSF 配置
- [ ] 预置和后预置
- [ ] 定义资源发放策略
- [ ] 使用 LSF 补丁安装程序更新资源连接器

### 查看关于 LSF 资源连接器的信息
- [ ] 检查 LSF 资源连接器状态
- [ ] 使用 badmin 查看 LSF 资源连接器信息
- [ ] 日志和故障排查

### 配置参考
- [ ] lsb.applications
    - [ ] RC_ACCOUNT
    - [ ] RC_RECLAIM_ACTION
- [ ] lsb.queues
    - [ ] RC_ACCOUNT
    - [ ] RC_DEMAND_POLICY
    - [ ] RC_HOSTS
- [ ] lsf.conf
    - [ ] LSB_RC_DEFAULT_HOST_TYPE
    - [ ] LSB_RC_EXTERNAL_HOST_FLAG
    - [ ] LSB_RC_EXTERNAL_HOST_IDLE_TIME
    - [ ] LSB_RC_EXTERNAL_HOST_MAX_TTL
    - [ ] LSB_RC_MQTT_ERROR_LIMIT
    - [ ] LSF_MQ_BROKER_HOSTS
    - [ ] LSB_RC_QUERY_INTERVAL
    - [ ] LSB_RC_REQUEUE_BUFFER
    - [ ] LSB_RC_TEMPLATE_REQUEST_DELAY
    - [ ] LSB_RC_UPDATE_INTERVAL
    - [ ] MQTT_BROKER_HOST
    - [ ] MQTT_BROKER_PORT
    - [ ] EBROKERD_HOST_CLEAN_DELAY
- [ ] egoprov_config.json
- [ ] egoprov_ego.conf
- [ ] egoprov_templates.json
- [ ] hostProviders.json
- [ ] osprov_config.json
- [ ] osprov_templates.json
- [ ] policy_config.json
- [ ] awsprov_config.json
- [ ] awsprov_templates.json
- [ ] azureprov_config.json
- [ ] azureprov_templates.json
- [ ] cyclecloudprov_config.json
- [ ] cyclecloudprov_templates.json
- [ ] softlayerprov_config.json
- [ ] softlayer_templates.json
- [ ] googleprov_config.json
- [ ] googleprov_templates.json
- [ ] openshiftprov_config.json
- [ ] openshiftprov_templates.json
- [ ] ibmcloudgen2_config.json
- [ ] ibmcloudgen2_templates.json


## LSF Connector 与 Kubernetes  

### 概述
### 局限
### 安装
### 配置
### 验证
### 部署作业
### 提交作业
- [ ] 示例: 提交 sleep 作业