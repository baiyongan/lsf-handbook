# 资源

Resources are physical and logical entities that are used by applications to run. While resource is a generic term, and can include low-level things such as shared memory segments or semaphores. In LSF, EGO manages CPU slots.

A resource of a particular type has attributes. For example, a compute host has the attributes of memory, CPU utilization, operating system type.

## Resource groups

Resources can be grouped into logical groups to simplify identification, resource allocation, or for administration and monitoring purposes. These resource groups are used to provide a consumer with a like group of hosts to run workload. Any host in a resource group can be able to run the same workload.

The following figure shows two resource groups:

- ManagementHosts
- ComputeHosts

![Resource groups](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_foundations/resource_groups_intro.jpg)

If all of your hosts are identical, these resource groups might suffice. If your application requires a specific type of hosts (for example, with a minimum processor speed), and not all hosts meet this criteria, you likely need to create resource groups to group like hosts together.

For example, a simple way to group resources might be to group your hosts by operating system type.

EGO provides a common grouping mechanism for resources. Resources might come and go from the system, so EGO supports dynamic membership in a resource group. Hosts can be placed explicitly into individual resource groups, or the resource groups can be defined with a dynamic membership based on specific criteria. This criteria includes operating system type, CPU speed, total memory, or swap configuration, or custom attributes.