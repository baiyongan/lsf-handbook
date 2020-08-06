# 自定义动态许可证信息输出

默认情况下，**blstat** 命令显示一组预定义的动态许可证信息。虽然您可以使用各种 **blstat** 选项显示特定的动态许可证信息，但也可以使用 -f 选项来自定义 **blstat** 显示的特定字段。使用 -f 选项可创建特定的 **blstat** 输出格式，从而使您可以通过使用自定义脚本，轻松解析所需的信息或以预定义的格式显示信息。

blstat ... -f "field_name[:[-][output_width]] ... [delimiter='character']"

- 指定要显示的 **blstat** 字段（或别名，而不是完整的字段名称），显示的顺序和宽度。
- 仅指定 **blstat** 字段名称或别名，以将其输出设置为无限宽度和左对齐。
- 指定不带宽度的冒号（:)，以将输出宽度设置为该字段的建议宽度。
- 用宽度指定冒号（:)，以设置该字段显示的最大字符数。 当值超过此宽度时，**blstat** 将截断输出。
- 当 **blstat** 显示特定字段的输出时，请指定连字符（-）以设置右对齐。 如果未指定，则默认设置为设置左对齐。
- 使用 delimiter= 设置定界字符以在不同的标题和字段之间显示。 该定界符必须是单个字符。 默认情况下，定界符为空格。

输出自定义仅适用于不带任何选项的 **blstat** 命令，并适用于带有以下选项的 **blstat** 的输出：-Lp，-D，-t。 -f 选项不能与任何其他 **blstat** 选项一起使用。

以下是用于指定要显示的 **blstat** 字段的字段名称，建议的宽度，可以用来代替字段名称的别名，适用的 LSF License Scheduler 模式以及该字段的简要说明：

| Field 名称               | 宽度 | 别名             | 模式                             | 描述                       |
| :----------------------- | :--- | :--------------- | :------------------------------- | :------------------------- |
| service_domain_name      | 19   | sd_name          | 所有                             | 服务域名称                 |
| service_domain_others    | 9    | sd_others        | 服务域中 “others” 令牌的总数     |                            |
| service_domain_lsf_total | 12   | sd_lsf_total     | LSF 可以从服务域使用的令牌总数   |                            |
| service_domain_alloc     | 8    | sd_alloc         | 集群模式                         | 服务域分配的令牌总数       |
| service_domain_use       | 7    | sd_use           | 服务域中已使用令牌的总数         |                            |
| service_domain_inuse     | 8    | sd_inuse         | 项目和快速调度模式               | 服务域中正在使用的令牌总数 |
| service_domain_reserve   | 7    | sd_rsv           | 服务域中保留令牌的总数           |                            |
| service_domain_free      | 7    | sd_free          | 来自服务域的免费令牌总数         |                            |
| project_name             | 15   | proj_name        | 项目名称                         |                            |
| project_share            | 7    | proj_share       | 项目份额数                       |                            |
| project_own              | 7    | proj_own         | 项目拥有的令牌数量               |                            |
| project_inuse            | 7    | proj_inuse       | 项目正在使用的令牌数量           |                            |
| project_reserve          | 7    | proj_rsv         | 项目保留的令牌数量               |                            |
| project_free             | 7    | proj_free        | 项目的免费令牌数量               |                            |
| project_demand           | 8    | proj_demand      | 项目所需的令牌数量               |                            |
| project_limit            | 7    | proj_limit       | 项目限额                         |                            |
| project_non_share        | 11   | proj_non_share   | 项目的非共享令牌数               |                            |
| cluster_name             | 15   | cl_name          | 所有                             | 集群名称                   |
| cluster_share            | 7    | cl_share         | 集群模式                         | 集群中的份额数             |
| cluster_alloc            | 7    | cl_alloc         | 集群和快速调度模式               | 分配给集群的令牌数量       |
| cluster_target           | 8    | cl_target        | 集群的目标令牌数                 |                            |
| cluster_inuse            | 7    | cl_inuse         | 所有                             | 集群中正在使用的令牌数     |
| cluster_reserve          | 7    | cl_rsv           | 集群中保留的令牌数               |                            |
| cluster_free             | 7    | cl_free          | 集群中的免费令牌数量             |                            |
| cluster_over             | 7    | cl_over          | 集群和快速调度模式               | 集群中过度使用的令牌数     |
| cluster_demand           | 8    | cl_demand        | 所有                             | 集群需求                   |
| cluster_peak             | 7    | cl_peak          | 集群模式                         | 集群中已使用令牌的峰值数量 |
| cluster_buffer           | 8    | cl_buff          | 在集群中分配缓冲区               |                            |
| cluster_acum_use         | 10   | cl_acum_use      | 项目模式                         | 集群中已使用令牌的累计数量 |
| cluster_scaled_acum      | 13   | cl_scaled_acum   | 集群中已累积使用令牌的缩放数量   |                            |
| cluster_avail            | 7    | cl_avail         | 集群中可用令牌的数量             |                            |
| feature_name             | 18   | feat_name        | 所有                             | 功能名称                   |
| feature_mode             | 20   | feat_mode        | 特征模式                         |                            |
| feature_lm_license_name  | 17   | feat_lm_lic_name | FlexNet 服务器中许可证功能的名称 |                            |

##### 提示

字段名称和别名不区分大小写。 输出宽度的有效值为任何正整数 1-4096。