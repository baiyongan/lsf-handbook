# 设置 LSF 环境

使用 LSF 之前，必须使用 cshrc.lsf 或 profile.lsf 文件设置 LSF 执行环境。

## 步骤

登录到 LSF 主机后，使用以下 shell 程序环境文件之一，来设置您的 LSF 环境。

- 在 csh 或 tcsh shell 中，运行 source 命令：

  ```shell
% source <LSF_TOP>/conf/cshrc.lsf
  ```

- 在 sh , ksh, 或 bash shell 中运行以下命令:

  ```shell
$ . <LSF_TOP>/conf/profile.lsf
  ```

文件 cshrc.lsf 和 profile.lsf 是在安装过程中通过 **lsfinstall** 命令创建的，以设置 LSF 操作环境。