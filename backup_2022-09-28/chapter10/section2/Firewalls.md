# 防火墙

LSF，许可证调度程序和 **taskman** 互操作性的配置。

## 设置防火墙通信

### 任务说明

**mbatchd** 和 **bld** 侦听端口（入站连接）必须在防火墙的任一侧打开。

- **mbatchd**: 由 lsf.conf 中的 **LSB_MBD_PORT** 设置
- **bld**: 由 lsf.licensescheduler 中的 **PORT** 设置

### 步骤

- 如果防火墙位于**mbatchd** 主机和 **bld** 主机之间，则两个侦听端口都必须打开。
- 如果防火墙位于 **bld** 和 **blcollect** 主机之间（例如，**blcollect** 被配置为在许可证服务器上本地运行，而 **bld** 位于 LSF 主节点上）， **bld** 侦听端口必须打开。
- 如果防火墙位于 **taskman** 和 **bld** 之间（其中作业使用 **taskman** 与 License Scheduler 进行接口），则必须打开 **bld** 侦听端口。