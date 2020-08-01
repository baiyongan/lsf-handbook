# Customize dynamic license information output

By default, the **blstat** command displays a predefined set of dynamic license information. While you can use various **blstat** options to display specific dynamic license information, you can also customize the specific fields that **blstat** displays using the -f option. Use the -f option to create a specific **blstat** output format, allowing you to easily parse the information you need by using custom scripts or to display the information in a predefined format.

blstat ... -f "field_name[:[-][output_width]] ... [delimiter='character']"

- Specify which **blstat** fields (or aliases instead of the full field names), in which order, and with what width to display.
- Specify only the **blstat** field name or alias to set its output to unlimited width and left justification.
- Specify the colon (:) without a width to set the output width to the recommended width for that field.
- Specify the colon (:) with a width to set the maximum number of characters to display for the field. When the value exceeds this width, **blstat** truncates the output.
- Specify a hyphen (-) to set right justification when **blstat** displays the output for the specific field. If not specified, the default is to set left justification.
- Use delimiter= to set the delimiting character to display between different headers and fields. This delimiter must be a single character. By default, the delimiter is a space.

Output customization applies only to the **blstat** command with no options, and to output for **blstat** with the following options: -Lp, -D, -t. The -f option does not work with any other **blstat** option.

The following are the field names used to specify the **blstat** fields to display, recommended width, aliases you can use instead of field names, the applicable LSF License Scheduler modes, and a brief description of the field:

| Field name               | Width | Alias            | Mode                                                         | Description                                              |
| :----------------------- | :---- | :--------------- | :----------------------------------------------------------- | :------------------------------------------------------- |
| service_domain_name      | 19    | sd_name          | all                                                          | Name of the service domain                               |
| service_domain_others    | 9     | sd_others        | Total number of "others" tokens in the service domain        |                                                          |
| service_domain_lsf_total | 12    | sd_lsf_total     | Total number of tokens that LSF can use from the service domain |                                                          |
| service_domain_alloc     | 8     | sd_alloc         | cluster mode                                                 | Total number of allocated tokens from the service domain |
| service_domain_use       | 7     | sd_use           | Total number of used tokens from the service domain          |                                                          |
| service_domain_inuse     | 8     | sd_inuse         | project and fast dispatch mode                               | Total number of tokens in use from the service domain    |
| service_domain_reserve   | 7     | sd_rsv           | Total number of reserved tokens from the service domain      |                                                          |
| service_domain_free      | 7     | sd_free          | Total number of free tokens from the service domain          |                                                          |
| project_name             | 15    | proj_name        | Name of the project                                          |                                                          |
| project_share            | 7     | proj_share       | Number of shares for the project                             |                                                          |
| project_own              | 7     | proj_own         | Number of tokens that are owned by the project               |                                                          |
| project_inuse            | 7     | proj_inuse       | Number of tokens that are in use by the project              |                                                          |
| project_reserve          | 7     | proj_rsv         | Number of tokens that are reserved by the project            |                                                          |
| project_free             | 7     | proj_free        | Number of free tokens for the project                        |                                                          |
| project_demand           | 8     | proj_demand      | Number of tokens that are demanded by the project            |                                                          |
| project_limit            | 7     | proj_limit       | The project limit                                            |                                                          |
| project_non_share        | 11    | proj_non_share   | Number of non-shared tokens for the project                  |                                                          |
| cluster_name             | 15    | cl_name          | all                                                          | Name of the cluster                                      |
| cluster_share            | 7     | cl_share         | cluster mode                                                 | Number of shares in the cluster                          |
| cluster_alloc            | 7     | cl_alloc         | cluster and fast dispatch mode                               | Number of tokens that are allocated to the cluster       |
| cluster_target           | 8     | cl_target        | Target number of tokens for the cluster                      |                                                          |
| cluster_inuse            | 7     | cl_inuse         | all                                                          | Number of tokens that are in use in the cluster          |
| cluster_reserve          | 7     | cl_rsv           | Number of tokens that are reserved in the cluster            |                                                          |
| cluster_free             | 7     | cl_free          | Number of free tokens in the cluster                         |                                                          |
| cluster_over             | 7     | cl_over          | cluster and fast dispatch mode                               | Number of overused tokens in the cluster                 |
| cluster_demand           | 8     | cl_demand        | all                                                          | Demand of the cluster                                    |
| cluster_peak             | 7     | cl_peak          | cluster mode                                                 | Peak number of used tokens in the cluster                |
| cluster_buffer           | 8     | cl_buff          | Allocate buffer in the cluster                               |                                                          |
| cluster_acum_use         | 10    | cl_acum_use      | project mode                                                 | Accumulated number of used tokens in the cluster         |
| cluster_scaled_acum      | 13    | cl_scaled_acum   | Scaled number of accumulated used tokens in the cluster      |                                                          |
| cluster_avail            | 7     | cl_avail         | Number of available tokens in the cluster                    |                                                          |
| feature_name             | 18    | feat_name        | all                                                          | Name of the feature                                      |
| feature_mode             | 20    | feat_mode        | Feature mode                                                 |                                                          |
| feature_lm_license_name  | 17    | feat_lm_lic_name | Name of the license feature in the FlexNet server            |                                                          |

**Note**Field names and aliases are not case-sensitive. Valid values for the output width are any positive integer 1 - 4096.