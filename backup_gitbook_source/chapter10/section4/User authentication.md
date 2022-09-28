# 用户认证

当用户声称某作业属于某个项目时， LSF License Scheduler  会检查该用户是否属于该项目，因为项目会分配公平份额优先级，而抢占则基于所有权。 当用户向不属于他们的许可项目提交作业时，请求将被拒绝，或者将作业放入共享数量很少，或根本没有共享的默认存储桶中。

管理员可以控制谁可以运行什么项目。 默认情况下，未启用这种身份验证以与 LSF License Scheduler 的早期版本兼容。 启用后，用户身份验证具有以下行为：

- 如果用户属于项目，则 LSF License Scheduler 允许许可请求。
- 如果用户不属于该项目，或者该项目与配置中的任何项目都不匹配，则 LSF License Scheduler 拒绝该请求。
- 如果在 LSF License Scheduler 用户验证配置文件 ls.users 中配置了默认项目，则 LSF License Scheduler 会将项目更改为 default，并允许许可证请求。
- 如果项目是默认项目，则无需身份验证，并且 LSF License Scheduler 允许该请求。



## 启用用户身份验证

### 步骤

1. 要为 LSF 作业启用用户身份验证，请将 LSF 配置为使用身份验证 esub（**esub.ls_auth**）。

   在 lsf.conf 中定义 LSB_ESUB_METHOD=lsauth。

2. 要为 **taskman** 作业启用用户身份验证，请在 lsf.licensescheduler 中定义 AUTH = Y。

3. 在 LSF_CONFDIR/ls.users 文件中配置用户及其相关项目。

    该文件使用以下格式每行定义一个项目：

   ```shell
   project_name:::[user_name][,user_name2 ...]
   ```

   例如：

   ```shell
   Project1:::user1,user2
   default:::
   ```

   ##### 提示

   确保 ls.users 中的项目（包括默认项目）符合 lsf.licensescheduler 配置。