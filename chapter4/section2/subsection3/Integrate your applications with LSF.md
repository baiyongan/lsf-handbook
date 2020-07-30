# 将您的应用程序与 LSF 集成

通过将应用程序与 LSF 集成，可以确保用户可以使用正确而完整的作业提交选项，来提交和运行其作业，而无需学习 LSF 命令。

通过三种方式将应用程序与 LSF 集成：

- 包装 shell 脚本
- 包装二进制可执行文件
- 修改现有的应用程序源代码和接口

## 包装 shell 脚本

最简单的集成方法是将 **bsub** 命令放入可执行文件中，例如 Shell 脚本。 包装脚本是用于通过 LSF 启动应用程序的可执行文件。 它为用户提供了一个简单的界面来运行其作业，该界面易于部署和维护。

例如，如果您的应用程序名为 abc，则将 abc 重命名为 abc_real ，并创建一个名为 abc 的包装脚本：

```shell
#! /bin/sh
bsub -R "rusage[abc_license=1:duration=1]" abc_real
```

用户运行 abc 时，实际上是在运行脚本，以使用 1 个名为 abc_license 的共享资源向 LSF 提交作业 abc_real。

有关使用 **bsub** 命令的 -R 选项上的资源需求（使用率）字符串，指定共享资源的更多信息，请参阅 [Manage software licenses and other shared resources](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_admin_foundations/shared_resource.html?view=kc#chared_resource39847).

通过向脚本添加适当的选项，可以增强集成：

- 根据许可证的可用性重新排队
- 在执行主机上的本地目录中，复制输入和输出文件
- 计算和估算资源需求

## 包装二进制程序

包装二进制文件类似于已编译二进制可执行文件形式的包装 shell 脚本。 编译的包装文件通常比 shell 脚本运行得更快，更高效，并且它们还可以访问 LSF API（LSLIB 和 LSBLIB）。 二进制代码也更加安全，因为用户无法在没有源代码和适当的库的情况下对其进行修改，但是开发包装器二进制程序比包装 shell 脚本要花费更多的时间。

## 修改现有的应用程序源代码和接口

LSF 已经与许多常用软件产品紧密集成。 IBM 和其他软件应用程序供应商提供了用于更紧密地集成 LSF 和其他应用程序的设施和服务。 通过修改现有的应用程序用户界面，您可以轻松完成作业提交，许可证最大化，并行执行以及其他高级 LSF 功能。 在某些情况下，您可以直接从应用程序用户界面运行 LSF 作业。

