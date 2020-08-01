# 使您的集群可供用户使用

确保所有 LSF 用户在其自己的 .cshrc 或 .profile 文件末尾都包含 cshrc.lsf 或 profile.lsf 文件，或者在使用 LSF 之前运行这两个文件之一。

## 任务说明

要为您的用户设置 LSF 环境，请使用以下两个 Shell 文件：

- LSF_CONFDIR/cshrc.lsf

  将此文件用于 **csh** 或 **tcsh** shell。

- LSF_CONFDIR/profile.lsf

  将此文件用于 **sh**, **ksh**, 或 **bash** shell.

## 步骤

对于 **csh** 或 **tcsh** shell：

- 为所有用户将 cshrc.lsf 文件添加到 .cshrc 文件的末尾：

  - 将 cshrc.lsf 文件的内容复制到 .cshrc 文件中。

  - 在 .cshrc 文件的末尾添加带有 source 命令的行：

     例如，如果集群的 LSF_TOP 目录为 /usr/share/lsf/conf，则将以下行添加到 .cshrc 文件中：

    ```shell
source /usr/share/lsf/conf/cshrc.lsf
    ```

对于 **sh**, **ksh**, 或 **bash** shell:

- 为所有用户将 profile.lsf 文件添加到 .profile 文件的末尾：

  - 将 profile.lsf 文件的内容复制到 .profile 文件中。

  - 例如，如果集群的 LSF_TOP 目录为 /usr/share/lsf/conf，则在 .profile 文件的末尾添加类似于以下内容的行：

    ```shell
. /usr/share/lsf/conf/profile.lsf
    ```