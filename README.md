# LSF Handbook

![GitHub commits since tagged version](https://img.shields.io/github/commits-since/baiyongan/lsf-handbook/v1.0.0?color=yellow&logo=github&style=for-the-badge)
![GitHub contributors](https://img.shields.io/github/contributors/baiyongan/lsf-handbook?logo=github&style=for-the-badge)
![GitHub repo size](https://img.shields.io/github/repo-size/baiyongan/lsf-handbook?color=purple&logo=github&style=for-the-badge)
![GitHub Workflow Status](https://img.shields.io/github/workflow/status/baiyongan/lsf-handbook/pages%20build%20and%20deployment?color=blue&logo=github&style=for-the-badge)
![GitHub last commit](https://img.shields.io/github/last-commit/baiyongan/lsf-handbook?logo=github&style=for-the-badge)


<!-- ## 内容简介

主要内容是 IBM 官方 LSF manual 的**文档翻译**，具体内容涉及 LSF 的产品介绍、安装升级、用户操作、作业调度、集群运维、功能开发及拓展等。

其次结合译者的工作需求，会有一些**相关知识点的增补，与实际操作经验的总结**。大致包含 Linux 运行环境的常见服务配置、vim 编辑器操作、系统性能调优、队列日志分析、EDA 作业优化、同类调度器（Slurm/PBS）的功能对比等等。

## 重点章节

依照 **Part > Chapter > Section > Subsection > Article** 的行文结构

- Part I 入门介绍篇
  - chapter1 LSF 介绍
    - 重点： lsf 快速入门章节
  - chapter2 安装、升级与迁移
  
- Part II 基础操作篇
  - chapter3 用户操作基础
    - 重点：文件目录，LSF 守护程序与进程，作业生命周期，调度策略
  - chapter4 管理员操作基础
    - 重点：重要配置文件、服务的启动，资源管理等，日志排错

- Part III 作业调度篇
  - chapter5 作业调度管理
    - 重点：LSF daemons 相关， bsub 命令参数及功能

- Part IV 集群运维篇
  - chapter6 集群维护管理
    - 重点：
  - chapter7 参考文档
      - 重点：
  
- Part V 功能拓展篇
  - chapter8 LSF 拓展
  - chapter9 最佳实践与建议
  - chapter10 LSF licence scheduler 
  
- Part VI 经验总结篇
  - chapter11 Linux 操作进阶
    - 重点：常见服务操作、免密、文件服务器、bash脚本编程规范、vim编辑器等
  - chapter12 实际实施经验
    - 重点：日志分析，高级调度策略实施等
  - chapter13 调度器产品对比、行业领域结合等
    - 重点：slurm，PBS等 -->

## 译作初衷

IBM 旗下的作业调度器 LSF， 作为一款在 HPC 领域内应用广泛的商业调度器，其 Manual 是针对众多行业客户而编写的，文档受众主要是各大中小型企业的集群管理者，其次则为数量更多的集群使用者，与少部分功能开发者。但实际上，因为每个企业/非企业级用户的软硬件基础架构、业务场景等有所不同，所以，作为集群的管理者，除了需要熟悉官网中介绍的功能操作外，也有必要结合实际的工作需求，基于所在行业，进行实际经验的总结与梳理等。

本 LSF Handbook 站点，**是从集群管理及二次开发者的角度出发**，摘选出 LSF Manual 的部分重点章节，并进行一些翻译与增补，鉴于作者水平精力有限，出现错误纰漏之处在所难免，希望读者不吝批评指正。

## 更新方式

- 基础性的概念、文章等内容，需要完全掌握理解，尽量做到——全文准确翻译；
- 章节目录，简介说明等内容，用于快速了解都实现了哪些功能，涉及到哪些工具，同样会进行翻译，并保留原英文目录，作为对照；
- 功能解释，特性说明等内容，一般在真正用到时，再翻阅查询即可，且阅读原文更能准确把握其真实含义，因此，不会翻译，而是根据使用经验给出阅读建议，即划重点；
- 经验总结、资源分享等内容，会根据个人实际经验及兴趣，有选择地介绍某些工具，如 k8s，API 等，或分享整理一些搜集到的，不错的资源。

## 章节列表

| 序号 | 章节     | 原文                                                         |
| ---- | -------- | :----------------------------------------------------------- |
| 一   | **快速入门** | [Getting started](https://www.ibm.com/docs/en/spectrum-lsf/10.1.0?topic=getting-started) |
| 二   | LSF 基础 | [LSF foundations](https://www.ibm.com/docs/en/spectrum-lsf/10.1.0?topic=lsf-foundations) |
| 三   | **安装部署** | [Install, upgrade, and migrate](https://www.ibm.com/docs/en/spectrum-lsf/10.1.0?topic=install-upgrade-migrate) |
| 四   | **运行作业** | [Run jobs](https://www.ibm.com/docs/en/spectrum-lsf/10.1.0?topic=run-jobs) |
| 五   | **管理 LSF** | [Administer LSF](https://www.ibm.com/docs/en/spectrum-lsf/10.1.0?topic=administer-lsf) |
| 六   | **参考文档** | [Reference](https://www.ibm.com/docs/en/spectrum-lsf/10.1.0?topic=reference) |
| 七   | **关联工具** | [LSF on Windows](https://www.ibm.com/docs/en/spectrum-lsf/10.1.0?topic=lsf-windows)、 [LSF License Scheduler](https://www.ibm.com/docs/en/spectrum-lsf/10.1.0?topic=lsf-license-scheduler)、[LSF Data Manager](https://www.ibm.com/docs/en/spectrum-lsf/10.1.0?topic=lsf-data-manager)、[LSF resource connnector](https://www.ibm.com/docs/en/spectrum-lsf/10.1.0?topic=lsf-resource-connnector)、[LSF Connector for Kubernetes](https://www.ibm.com/docs/en/spectrum-lsf/10.1.0?topic=lsf-connector-kubernetes)、 |
| 八   | **LSF 扩展** | [Extend LSF](https://www.ibm.com/docs/en/spectrum-lsf/10.1.0?topic=extend-lsf) |
| 九   | **最佳实践** | [Best practices and tips](https://www.ibm.com/docs/en/spectrum-lsf/10.1.0?topic=best-practices-tips) |
| 十   | **经验建议** |                                                             |
| 十一 | **拓展延伸** |                                                             |
| 十二 | **资源分享** |                                                             |



## 意见与参与

如果有任何意见或建议，请发 [issues](https://github.com/baiyongan/lsf-handbook/issues) 联系。

如果想共同参与项目更新，或有独到的使用经验或资源等希望分享，欢迎 [fork](https://github.com/baiyongan/lsf-handbook) 与[PRs](https://github.com/baiyongan/lsf-handbook/pulls)，共同践行开源理念，谢谢！

## 参考资料

基于  [**IBM Spectrum LSF 10.1.0**](https://www.ibm.com/docs/en/spectrum-lsf/10.1.0) 官方文档。

## License

[CC 4.0](docs/LICENSE.md)








