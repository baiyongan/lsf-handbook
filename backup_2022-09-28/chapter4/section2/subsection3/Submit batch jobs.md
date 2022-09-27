# 提交批处理作业

**bsub** 命令将作业提交到 LSF 批处理调度队列。

以下命令将 **sleep** 作业提交到默认队列（normal）：

```shell
% bsub sleep 60
Job <3616> is submitted to default queue <normal>.
```

当作业提交给 LSF 时，将为其分配唯一的作业 ID，在这种情况下为 3616。

您可以在 **bsub** 命令上指定各种作业选项。 例如，您可以指定一个队列，作业命令 **sleep 60** 是最后一个选项：

```shell
% bsub -q short sleep 60
Job <3628> is submitted to queue <short>.
```

## LSF 对作业输出的作用

默认情况下，当作业完成时，LSF将电子邮件和作业报告以及所有输出和错误消息发送到提交作业的用户帐户。 您可以选择使用 -o 和 -e 选项将标准输出和标准错误保存到文件中。

以下命令，将作业的标准输出和标准错误附加到 user1 家目录下的 job子目录中的 output.3640 和 errors.3640文件中。

```shell
% bsub -q short -o /home/user1/job/output.%J -e /home/user1/job/errors.%J ls -l
Job <3640> is submitted to queue <short>.
```

创建文件时，**％J** 变量将替换为作业 ID。 使用 ％J 可以帮助您在运行大量作业时找到作业输出。

## 使用 bsub -I 的交互式批处理作业

要通过 LSF 提交交互式作业，请使用 -I 选项：

以下命令提交一个批处理交互式作业，该作业显示 **ls** 命令的输出：

```shell
% bsub -I ls
```

要使用伪终端 (pseudo-terminal) 提交批处理交互式作业，请使用 bsub -Ip 选项。

要提交批处理交互式作业,并创建具有 Shell 模式支持的伪终端，请使用 bsub -Is 选项。