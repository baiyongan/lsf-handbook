# 将主机添加到集群

使用 LSF 安装脚本 **lsfinstall** 将新主机和主机类型添加到您的集群中。

## 开始之前

确保您具有要添加的主机类型的 LSF distribution 文件。 例如，要向集群添加运行 x86-64 内核 2.6 和 3.x 的 Linux系统，请获取文件 lsf10.1_linux2.6-glibc2.3-x86_64.tar.Z。

可通过 [IBM Passport Advantage](http://www.ibm.com/software/howtobuy/passportadvantage/pao_customers.htm) 下载所有受支持的 LSF 版本的分发软件包。

有关受支持的操作系统的完整列表，请参阅 IBM developerWorks 上的  [LSF System Requirements](http://www.ibm.com/developerworks/community/wikis/home?lang=en#!/wiki/New IBM Platform LSF Wiki/page/Platform LSF system requirements) 。

以下视频提供了有关通过IBM Passport Advantage下载LSF的更多帮助：

- [YouTube](https://www.ibm.com/links?url=http%3A%2F%2Fwww.youtube.com%2Fwatch%3Fv%3DYV1vdpQ3Rwk%26feature%3Dyoutube)
- [IBM Education Assistant](http://publib.boulder.ibm.com/infocenter/ieduasst/v1r1m0/index.jsp?topic=/com.ibm.iea.selfassist/selfassist/1.0/download/HowtoDownloadLSF/HowtoDownloadLSF.html)

## 任务说明

将主机添加到集群，有以下主要步骤：

1. ##### 安装主机类型的LSF二进制文件。
2. ##### 将主机信息添加到 lsf.cluster.cluster_name 文件。
3. ##### 设置新主机。

## 步骤

#### 为新的主机类型安装二进制文件。

使用 **lsfinstall** 命令将新的主机类型添加到您的集群中。 如果您已经具有要添加的主机类型的发布文件，则可以跳过这些步骤。

1. 以 root 用户身份登录到可以访问 LSF 安装脚本目录的任何主机。

2. 转到安装脚本目录。

   ```shell
   # cd /usr/share/lsf/cluster1/10.1/install
   ```

3. 编辑 install.config 文件以指定要用于新主机类型的选项。

   有关 install.config 文件的更多信息，请参见 [IBM Spectrum LSF Configuration Reference](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_welcome/lsf_kc_config_ref.html?view=kc). 有关 **lsfinstall** 命令的信息, 请参阅 [Installing IBM Spectrum LSF on UNIX and Linux](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_welcome/lsf_kc_unix_install.html?view=kc) 以及 [IBM Spectrum LSF Command Reference](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_welcome/lsf_kc_cmd_ref.html?view=kc).

4. 运行 ./lsfinstall -f install.config 命令。

5. 请遵循 [Installing IBM Spectrum LSF on UNIX and Linux](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_welcome/lsf_kc_unix_install.html?view=kc) 中 [After Installing LSF](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_unix_install/lsf_installnewunix_configcluster_tsk.html?view=kc) 中的主机设置步骤。(或在由 **lsfinstall** 脚本生成的 lsf_getting_started.html 文件中) 设置新主机。

#### 将主机信息添加到 lsf.cluster.cluster_name 文件。

1. 以主要 LSF 管理员身份登录到 LSF 主节点。

2. 编辑 LSF_CONFDIR/lsf.cluster.cluster_name 文件，并将新主机的主机信息添加到 “Host” 部分。

   - 添加主机名。

   - 添加型号或类型。

     如果在 “model” 和 “type” 列中输入关键字 ！，主机上的 **lim** 会自动检测到主机模型。

     您可能现在想使用该主机类型的默认值，并在以后有更多经验或更多信息时更改它们。

   - 在服务器列中指定 LSF 服务器或客户端：

     - 1（one）表示 LSF 服务器主机。
     
     - 0  (zero) 指示仅 LSF 客户端主机。      
     
       默认情况下，所有主机都被视为 LSF 服务器主机。
             

```shell
HOSTNAME  model  type      server  r1m  mem  RESOURCES  REXPRI
hosta     !      SUNSOL    1       1.0  4    ()         0
hostb     !      LINUX     0       1.0  4    ()         0
hostc     !      HPPA      1       1.0  4    ()         0
End Host
```

3. 将更改保存到 LSF_CONFDIR/lsf.cluster.cluster_name。
   
4. 重新配置 **lim** 以启用集群中的新主机。
   
      ```shell
   % lsadmin reconfig
   Checking configuration files ...
   No errors found.
   Do you really want to restart LIMs on all hosts? [y/n] y
   Restart LIM on <hosta> ...... done
   Restart LIM on <hostc> ...... done
   Restart LIM on <hostd> ...... done
   ```
   
   **lsadmin reconfig** 命令检查配置错误。 如果未找到无法恢复的错误，将要求您确认要在所有主机上重新启动**lim**，并重新配置 **lim**。 如果发现不可恢复的错误，则重新配置退出。

5. 重新配置 **mbatchd**.

   ```shell
   % badmin reconfig
   Checking configuration files ...
   No errors found.
   Do you want to reconfigure? [y/n] y
   Reconfiguration initiated
   ```

   **badmin reconfig ** 命令检查配置错误。 如果未找到不可恢复的错误，则要求您确认重新配置。 如果发现不可恢复的错误，则重新配置退出。


#### （可选）使用 **hostsetup** 命令设置新主机。

1. 以 root 用户身份登录到可以访问 LSF 安装脚本目录的任何主机。

2. 转到安装脚本目录。

   ```shell
   # cd /usr/share/lsf/cluster1/10.1/install
   ```

3. 运行 **hostsetup** 命令以设置新主机。

   ```shell
   # ./hostsetup --top="/usr/share/lsf/lsf_62" --boot="y"
   ```

   有关 **hostsetup** 命令的信息，请参阅 [Installing IBM Spectrum LSF on UNIX and Linux  以及 [IBM Spectrum LSF Command Reference](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_welcome/lsf_kc_cmd_ref.html?view=kc).

4. 在新主机上启动 LSF。

   运行以下命令：

   ```shell
   # lsadmin limstartup
   # lsadmin resstartup
   # badmin hstartup
   ```

5. 运行 **bhosts** 和 **lshosts** 命令以验证您的更改。

   如果任何主机类型或主机模型是UNKNOWN或DEFAULT，请参阅  [IBM Spectrum LSF Cluster Management and Operations](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_welcome/lsf_kc_cluster_ops.html?view=kc) 中的 [Working with hosts](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_admin/chap_hosts_working_with.html?view=kc) 来解决此问题。

## 结论

- 使用动态主机配置将主机添加到集群，而无需手动更改 LSF 配置。 有关动态添加主机的更多信息，请参阅 [IBM Spectrum LSF Cluster Management and Operations](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_welcome/lsf_kc_cluster_ops.html?view=kc)。
- 如果遇到错误，请参见 [Troubleshooting LSF problems](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_admin/chap_troubleshooting_lsf.html?view=kc#v3523448) ，以获取有关一些常见配置错误的帮助。