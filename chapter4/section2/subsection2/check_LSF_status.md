# 检查 LSF 状态

使用 LSF 管理命令检查集群配置，查看集群状态，以及 LSF 批处理作业负载系统配置和状态。

## 命令输出示例

本节中显示的 LSF 命令显示了典型输出的示例。 您看到的输出，可能会根据您的配置而有所不同。

这些命令都是简要描述，以便您可以轻松地使用它们，来验证您的 LSF 安装。 有关完整的用法和命令选项，请参见 [LSF Command Reference](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_welcome/lsf_kc_cmd_ref.html?view=kc) 或 LSF 手册页。 您可以在任何 LSF 主机上使用这些命令。

如果您从这些命令获得正确的输出，则可以使用集群了。 如果您的输出有错误，请参阅 [Troubleshooting LSF problems](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_admin/chap_troubleshooting_lsf.html?view=kc#v3523448) 来获得帮助。

- ##### 使用 lsadmin 命令检查集群配置

  **lsadmin** 命令控制 LSF 集群的操作，并管理 LSF 守护程序 **lim** 和 **res**。

- ##### 使用 lsid 和 lsload 命令检查集群状态

  **lsid** 命令告诉您是否正确设置了 LSF 环境。 **lsload** 命令显示集群的当前负载级别。

- ##### 使用 **badmin** 检查 LSF 批处理系统配置 

  **badmin** 命令控制和监视 LSF 批处理作业负载系统的操作。

- ##### 使用 **bhosts** 和 **bqueues** 查找批处理系统状态

  使用 **bhosts** 命令查看 LSF 批处理作业负载系统是否正常运行。 **bqueues** 命令显示可用队列的状态及其配置参数。

