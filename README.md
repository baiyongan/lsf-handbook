<!-- # Title

![banner]()

![badge]()
![badge]()
[![license](https://img.shields.io/github/license/:user/:repo.svg)](LICENSE)
[![standard-readme compliant](https://img.shields.io/badge/readme%20style-standard-brightgreen.svg?style=flat-square)](https://github.com/RichardLitt/standard-readme)

This is an example file with maximal choices selected.

This is a long description.

## Table of Contents

- [Title](#title)
  - [Table of Contents](#table-of-contents)
  - [Background](#background)
    - [Any optional sections](#any-optional-sections)
  - [Install](#install)
    - [Any optional sections](#any-optional-sections-1)
  - [Usage](#usage)
    - [Any optional sections](#any-optional-sections-2)
  - [Contributing](#contributing)
    - [Any optional sections](#any-optional-sections-3)
- [LSF handbook](#lsf-handbook)
  - [内容简介](#内容简介)
  - [重点章节](#重点章节)
  - [译作初衷](#译作初衷)
  - [版本](#版本)
  - [贡献者](#贡献者)
  - [License](#license)


## Background

### Any optional sections

## Install

This module depends upon a knowledge of [Markdown]().

```
```

### Any optional sections

## Usage

```
```

Note: The `license` badge image link at the top of this file should be updated with the correct `:user` and `:repo`.

### Any optional sections

## Contributing

See [the contributing file](CONTRIBUTING.md)!

PRs accepted.

Small note: If editing the Readme, please conform to the [standard-readme](https://github.com/RichardLitt/standard-readme) specification.

### Any optional sections
 -->


# LSF Handbook

## 内容简介

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
    - 重点：slurm，PBS等

## 译作初衷

IBM 旗下的作业调度系统 LSF， 作为一款在 HPC 领域内应用广泛的商业调度器，其 manual 是针对多种商业客户而编写的，文档受众主要是各大中小型企业的集群管理者，其次则为数量更多的集群使用者，与少部分功能开发者。但实际上，因为每个企业 / 非企业级用户的软硬件基础架构，与业务场景会有不同，所以，作为集群的管理者，除了需要熟悉官网中介绍的功能操作外，也有必要结合实际的工作需求，基于所在行业，进行实际经验的总结与梳理等。

故而，本 LSF 中文手册是**从集群管理及二次开发者的角度出发**，基于 LSF manual，进行的一些翻译与增补，鉴于译者水平精力有限，出现错误纰漏之处在所难免，希望读者不吝批评指正。

## 版本

基于 版本为 LSF 10.1.0 的 [**LSF manual**](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_welcome/lsf_welcome.html)。

## 贡献者


## License

[CC 4.0](docs/LICENSE.md)








