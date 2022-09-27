# 关于提交作业

提交 LSF 作业时，必须在资源需求使用部分（**bsub -R“ rusage ...”**选项）中保留许可证。

您无法通过运行   **bsub -R "select"** 成功保留许可证。

- 指定许可证令牌名称（与指定共享资源相同）。

- 如果使用项目模式，请使用 bsub -Lp 选项指定许可证项目名称。

   如果您在 lsf.conf 中也有 LSF_LIC_SCHED_STRICT_PROJECT_NAME = y 并且没有为所需功能配置默认项目，则该作业将被拒绝。

  ##### 提示

  使用 **blstat** 命令查看有关默认许可证项目的信息。

- 更新资源需求。

  如果队列或作业启动器脚本请求由 LSF ELIM 管理的许可证，则必须更新作业提交脚本，以请求使用许可证令牌名称的许可证。

示例：

bsub -R "rusage[AppB=1]" -Lp Lp1 myjob

此命令将名为 myjob 的作业提交给许可证项目 Lp1，并请求一个 AppB 许可证

bsub -R "rusage[AppC=1]" myjob

此命令提交名为 myjob 的作业，并请求一个 AppC 许可证。