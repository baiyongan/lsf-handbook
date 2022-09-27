# 保留的 FlexNet Manager 许可证

LSF License Scheduler 支持 FlexNet Manager 许可证保留关键字（**RESERVE**），该关键字允许 LSF License Scheduler 包含这些保留的许可证。 FlexNet Manager 保留的许可令牌被视为正在使用（作为 “OTHER” 令牌），而不是免费的（作为 “FREE” 令牌）。 因此，**RESERVE** 值包括在 **blstat** 命令输出的 **OTHERS **值中，而不包括在 **FREE** 值中。

要启用对 FlexNet Manager 许可证保留关键字的支持，请在 lsf.licensescheduler 文件中定义**LM_RESERVATION** 参数。 在 “Parameter” 部分中定义 **LM_RESERVATION=Y** 以启用全局支持，或者在 “Features” 部分中定义**LM_RESERVATION=Y** 以启用对单个功能的支持。

如果在功能中定义了 **WORKLOAD_DISTRIBUTION** 参数，则不能在基于时间的配置中使用此支持，也不能使用此支持。

##### 提示

FlexNet Manager 保留的许可证令牌，必须在 LSF License Scheduler 之外使用。