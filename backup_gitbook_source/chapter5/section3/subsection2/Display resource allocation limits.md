# 显示资源分配限制

Use the **blimits** command to display resource allocation limits.

The  

- Configured policy name and information for limits that are being applied to running jobs.
- Configured policy name and information for all limits, even if they are not being applied to running jobs (**-a** option).
- Users (**-u** option)
- Queues (**-q** option)
- Hosts (**-m** option)
- Project names (**-P** option)
- All resource configurations in lsb.resources (**-c** option). This option is the same as **bresources** with no options.

Resources that have no configured limits or no limit usage are indicated by a dash (-). Limits are displayed in a USED/LIMIT format. For example, if a limit of 10 slots is configured and 3 slots are in use, then **blimits** displays the limit for SLOTS as 3/10.

If limits MEM, SWP, or TMP are configured as percentages, both the limit and the amount that is used are displayed in MB. For example, **lshosts** displays maximum memory (maxmem) of 249 MB, and MEM is limited to 10% of available memory. If 10 MB out of are used, **blimits** displays the limit for MEM as 10/25 (10 MB USED from a 25 MB LIMIT).

Configured limits and resource usage for built-in resources (slots, mem, tmp, and swp load indices) are displayed as INTERNAL RESOURCE LIMITS separately from custom external resources, which are shown as EXTERNAL RESOURCE LIMITS.

Limits are displayed for both the vertical tabular format and the horizontal format for Limit sections. If a vertical format Limit section has no name, **blimits** displays NONAMEnnn under the NAME column for these limits, where the unnamed limits are numbered in the order the vertical-format Limit sections appear in the lsb.resources file.

If a resource consumer is configured as all, the limit usage for that consumer is indicated by a dash (-).

PER_HOST slot limits are not displayed. The **bhosts** command displays these limits as MXJ limits.

In MultiCluster, **blimits** returns the information about all limits in the local cluster.

**View information about resource allocation limits**