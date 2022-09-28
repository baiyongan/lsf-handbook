# 保证配置集群模式

集群模式在 LSF 集群之间分配许可证。 要为集群中的项目保证许可证资源，并在不使用许可证资源时借用许可证资源，请使用 LSF 保证类型的 SLA。 集群模式下的保证和借贷，类似于项目模式下的非共享许可证和所有权。

保证为属于集合使用者的作业提供了特定的资源（例如主机）。 作业在可能的情况下以保证的资源运行。 使用保证资源时，将按照配置的其他任何调度功能，在保证范围之外运行作业。 保证条件，在保证资源池中配置。

确保在 LSF 中配置了 SLA。 有关更多信息，请参阅《Administering IBM Spectrum LSF》和《IBM Spectrum LSF Configuration Reference》。



## 配置服务类别

### 任务说明

服务类允许访问有保证的资源。 为集群中的每个许可证项目配置服务类。

### 步骤

在 lsb.serviceclasses 文件中配置每个 ServiceClass 部分。 以 Begin ServiceClass 行开始，以 End ServiceClass 行结束。 对于每个服务类，必须指定：

1. NAME：服务类的名称。
2. GOALS = [GUARANTEE]
3. ServiceClass 部分的可选参数是 ACCESS_CONTROL，AUTO_ATTACH 和 DESCRIPTION。

您可以根据需要配置任意多个服务类部分。

##### 重要

用于服务类的名称不能与现有主机分区或用户组名称相同。

```shell
Begin ServiceClass
NAME = sla1
GOALS = [GUARANTEE]
ACCESS_CONTROL=LIC_PROJECTS[ proj1 ]
DESCRIPTION = A guarantee SLA with access restricted to the license project proj1.
End ServiceClass
```

### 自动将作业附加到服务类别

#### 任务说明

设置可选参数 **AUTO_ATTACH** 时，作业将自动附加到服务类。

如果未设置自动附件，则可以通过运行 bsub -sla serviceclass_name 将作业提交到服务类。

如果作业可以访问多个具有自动附件集的 SLA，则该作业将按照配置文件的顺序，附加到第一个有效的 SLA。

#### 步骤

在 lsb.serviceclasses 文件的 ServiceClass 部分中设置 AUTO_ATTACH=Y。

```shell
Begin ServiceClass
NAME = sla1
GOALS = [GUARANTEE]
ACCESS_CONTROL=LIC_PROJECTS[ proj1 ]
AUTO_ATTACH=Y
DESCRIPTION = A guarantee SLA with access restricted to the license project proj1.
Jobs submitted to proj1 are attached to the SLA automatically and run on guaranteed
resources if possible.
End ServiceClass
```

## 配置许可证令牌的资源池

### 任务说明

有保证的资源池为消费者提供了最低的资源保证，并且可以有选择地借出未使用的有保证的资源。

保证的资源池在 lsb.resources 中定义，并由 lsb.serviceclasses 的 ServiceClass 部分中定义的使用者使用。

### 步骤

在 lsb.resources 中配置 GuaranteedResourcePool 部分。从 Begin GuaranteedResourcePool 行开始，到 End GuaranteedResourcePool 行结尾。 指定以下参数：

1. NAME: 保证资源池的名称。
2. TYPE: 担保类型。 对于许可证，请使用资源类型，并包括许可证功能的名称。
3. DISTRIBUTION: 使用资源池共享所有服务类的分配。 可以是百分比或绝对数字。
4. 资源的 GuaranteedResourcePool 部分的可选参数是 LOAN_POLICIES 和 DESCRIPTION。

您可以根据需要配置任意数量的资源池。 一个资源池可由多个 SLA 使用，一个 SLA 可以访问多个资源池。

```shell
Begin GuaranteedResourcePool
NAME = hspice_guarantees
TYPE = resource[hspice]
DISTRIBUTION = ([proj1_sc,50%][proj2_sc,50%])
DESCRIPTION = A resource pool of hspice licenses controlled by License Scheduler
and used by proj1_sc and proj2_sc.
End GuaranteedResourcePool
```

## 配置借贷

### 任务说明

使用集群模式时，建议使用未使用的担保借贷。 禁用借贷后，请使用静态许可证分配策略。

配置后，未使用的许可证资源将根据借用策略借出。 借用策略允许特定队列访问保证资源池中未使用的资源。

### 步骤

1. 在 lsb.resources 中使用所需的 **NAME**，**TYPE** 和 **DISTRIBUTION** 参数配置保证的资源池。

2. 将借贷策略添加到保证的资源池中。

   使用 **LOAN_POLICIES=QUEUES [queue_name]** 指定哪些队列可以访问借出的资源。 使用关键字 **all** 可以从任何队列中借用到作业。

   例如，以下策略允许从队列 my_queue 借给作业：

   ```shell
   Begin GuaranteedResourcePool
   ...
   LOAN_POLICIES = QUEUES[my_queue]
   ...
   End GuaranteedResourcePool
   ```

### 配置短作业的借贷

#### 任务说明

可以根据作业运行时间或估计的运行时间来限制借贷。

#### 步骤

将策略 DURATION [minutes] 添加到 lsb.resources 中保证的资源池配置中，其中 minutes 是整数。

使用 DURATION 设置作业借用资源的最大作业运行时限制（或估计的运行时间，以较短者为准）。 完全省略 **DURATION**，以允许具有任何运行时间的作业从担保中借用。

例如，以下策略允许从运行时间在 10 分钟或更短时间内的任何队列中的作业借出资源：

```shell
Begin GuaranteedResourcePool
...
LOAN_POLICIES = QUEUES[all] DURATION[10]
...
End GuaranteedResourcePool
```

### 配置借贷以在作业等待有保证的资源时停止

#### 任务说明

可以限制借贷，以便仅当拥有未使用保证资源的使用者，没有待处理的负载时，作业才能访问借出的资源。

在运行需要多个许可证的作业时，限制借贷非常有用。 启用受限借贷后，借出单个许可证，不会延迟等待许可证资源累积的作业。

#### 步骤

将策略 CLOSE_ON_DEMAND 添加到 lsb.resources 中的保证资源池配置中。

```shell
Begin GuaranteedResourcePool
...
LOAN_POLICIES = QUEUES[queue1] CLOSE_ON_DEMAND
...
End GuaranteedResourcePool
```

## 配置有权访问所有保证资源的队列

### 任务说明

可以配置具有高优先级的队列（例如管理员测试队列）以访问所有保证的资源，而不管 SLA 的需求如何。

### 步骤

使用 **SLA_GUARANTEES_IGNORE = Y** 参数在 lsb.queues 文件中配置队列。

##### 提示

使用 **SLA_GUARANTEES_IGNORE = Y** 不能达到保证资源的目的。 请仅对低流量队列使用此参数。

## 重新启动以使更改生效

### 任务说明

必须启用集群模式，并且必须重新启动 LSF 集群才能使 LSF 配置更改生效。

### 步骤

1. 在 lsf.licensescheduler 的 Parameters 部分中，确认启用了集群模式（CLUSTER_MODE = Y）。
2. 运行 badmin mbdrestart 重新启动每个 LSF 集群。
3. 运行 bladmin reconfig 重新启动 bld。

## 查看保证的资源池

### 任务说明

保证的资源池配置包括资源类型，以及在相应服务类中定义的使用者之间的分配。

### 步骤

运行 **bresources -g -l -m** 以查看保证的资源池配置的详细信息，包括资源池中当前主机的列表。