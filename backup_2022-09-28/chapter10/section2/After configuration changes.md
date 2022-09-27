# 更改配置后

## 任务说明

如果对 License Scheduler 进行了配置更改，则必须重新配置 License Scheduler 以应用更改。 如果对 LSF 进行配置更改，则还必须重新配置 LSF。

## 步骤

1. 运行 bld -C 以测试配置错误。

2. 运行 bladmin reconfig all。

3. 如果更改了 lsf.conf 或其他 LSF 配置文件，请运行 badmin mbdrestart 和 lsadmin reconfig。

   ##### 备注

   某些 License Scheduler 配置更改后，必须运行 **badmin mbdrestart** 才能使更改生效。 以下配置更改要求您运行 **badmin mbdrestart**：

   - 项目更改，添加或删除
   - 功能更改，添加或删除，包括模式更改
   - 集群位置更改

   您还必须运行 **lsadmin reconfig** 才能使对 LIM 的任何更改生效（例如，如果您更改了 LSF_LIC_SCHED_HOSTS）。

