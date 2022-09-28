# 开启、结束与重配置 LSF

使用LSF管理命令 **lsadmin** 和 **badmin** 启动和停止 LSF 守护程序，并重新配置集群属性。

## 两个 LSF 管理命令（lsadmin 和 badmin）

##### 注意

只有 LSF 管理员或 root 用户可以运行这些命令。

要启动和停止 LSF，以及在更改任何配置文件后，重新配置 LSF，请使用以下命令：

- **lsadmin ** 命令控制 **lim** 和 **res** 守护程序的操作。
- **badmin** 命令控制 **mbatchd** 和 **sbatchd** 守护程序的操作。

## 如果您以 非root 用户身份安装 LSF

默认情况下，只有 root 可以启动 LSF 守护程序。 如果 **lsfinstall** 命令检测到您以 非root 用户身份安装，则选择配置多用户集群还是单用户集群：

#### 多用户配置

只有 root 可以启动 LSF 守护程序。 任何用户都可以将作业提交到您的集群。有关更改 **lsadmin** 和 **badmin**命令的所有权和权限的信息，请参阅 [Troubleshooting LSF problems](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_admin/chap_troubleshooting_lsf.html?view=kc).

要允许 LSF 管理员启动和停止 LSF 守护程序，请按照 [Configure LSF Startup](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_admin_foundations/config_startup.html?view=kc) 中的说明设置 /etc/lsf.sudoers 文件。

#### 单用户

您的用户帐户必须是 LSF 主要管理员。 您可以启动 LSF 守护程序，但是只有您的用户帐户,才能将作业提交到集群。 您的用户帐户必须能够读取系统内核信息，例如 /dev/kmem。

- ##### 使用 cshrc.lsf 和 profile.lsf 设置 LSF 环境

  使用 LSF 之前，必须使用 cshrc.lsf 或 profile.lsf 文件设置 LSF 执行环境。

- ##### 启动集群

  使用 **lsadmin** 和 **badmin** 命令启动 LSF 守护程序。

- ##### 停止集群

  使用 **lsadmin** 和 **badmin** 命令停止 LSF 守护程序。

- ##### 使用 lsadmin 和 badmin 重新配置群集

  更改任何配置文件后，请使用 **lsadmin** 和 **badmin** 命令重新配置 LSF。