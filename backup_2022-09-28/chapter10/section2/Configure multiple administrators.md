# 配置多个管理员

## 开始之前

主要 License Scheduler 管理员帐户，必须在主要 LSF 管理员帐户的 LSF 工作目录中具有写权限。

## 任务说明

管理员帐户使用您在安装许可证计划程序时指定的用户列表。 如果要添加或更改管理员，请编辑此参数。 列表中的第一个用户名是主要的 License Scheduler 管理员。 默认情况下，License Scheduler 创建的所有工作文件和目录均归 Lickaiense Scheduler 主帐户所有。

## 步骤

1. 以主要的 License Scheduler 管理员身份登录。

2. 如果要更改许可证计划程序管理员，请在 lsf.licensescheduler 中编辑 ADMIN 参数。 您可以指定多个由空格分隔的管理员。

   例如：

   `ADMIN = lsfadmin user1 user2 root`

3. 运行 **bld -C** 以测试配置错误。

4. 运行 **bladmin reconfig all** 以应用您的更改。