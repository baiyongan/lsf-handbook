# 管理软件许可证及其他共享资源

设置LSF外部LIM（ELIM），以将软件许可证，作为动态共享资源进行监视。

## How LSF uses dynamic shared resources

LSF recognizes two main types of resources:

- Host-based resources are available on all hosts in the cluster, for example, host type and model, or nodelocked software licenses.
- Shared resources are managed as dynamic load indexes available for a group of hosts in the cluster, for example, networked floating software licenses, shared file systems.

Shared resources are shared by a group of LSF hosts. LSF manages shared resources for host selection and batch or interactive job execution. These resources are dynamic resources because the load on the system changes with the availability of the resources.

## Software licenses as shared resources

The most common application of shared resources is to manage software application licenses. You submit jobs that require those licenses and LSF runs the jobs according to their priorities when licenses are available. When licenses are not available, LSF queues the jobs then dispatches them when licenses are free. Configuring application licenses as shared resources ensures optimal use of costly and critical resources.

## Define dynamic shared resources in an ELIM

For LSF to use a shared resource like a software license, you must define the resource in the Resource section of the lsf.shared file. You define the type of resource and how often you want LSF to refresh the value of the resource.

For LSF to track the resources correctly over time, you must define them as external load indexes. LSF updates load indexes periodically with a program called an External Load Information Manager (ELIM).

An ELIM can be a shell script or a compiled binary program, which returns the values of the shared resources you define. The ELIM must be named elim and located in the **LSF_SERVERDIR** directory:

```
/usr/share/lsf/lsf/cluser1/10.1/sparc-sol2/etc/elim
```

You can find examples of sample ELIMs in the misc/examples directory.

## Example of shared licenses

In the lsf.shared file, define two dynamic shared resources for software licenses, named license1 and license2:

```
Begin Resource
RESOURCENAME  TYPE    INTERVAL INCREASING  RELEASE   DESCRIPTION   # Keywords
license1      Numeric 30       N           Y         (license1 resource)
license2      Numeric 30       N           Y         (license2 resource)
End Resource
```

- The

   

  TYPE

   

  parameter for a shared resource can be one of the following types:

  - Numeric
  - Boolean
  - String

  In this case, the resource is Numeric.

- The **INTERVAL** parameter specifies how often you want the value to be refreshed. In this example, the ELIM updates the value of the shared resources license1 and license2 every 30 seconds.

- The N in the **INCREASING** column means that the license resources are decreasing; that is, as more licenses become available, the load becomes lower.

- The Y in the **RELEASE** column means that the license resources are released when a job that uses the license is suspended.

## Map dynamic shared resources to hosts

To make LSF aware of where the defined dynamic shared resources license1 and license2 you defined, map them to the hosts where they are located.

In the LSF_CONFDIR/lsf.cluster.cluster_name file, configure a ResourceMap section to specify the mapping between shared resources license1 and license2 you defined in the LSF_CONFDIR/lsf.shared file, and the hosts you want to map them to:

```
Begin ResourceMap
RESOURCENAME  LOCATION
license1      [all]
license1      [all]
End ResourceMap
```

In this resource map, the [all] attribute under the **LOCATION** parameter means that resources license1 and license2 under the **RESOURCENAME** parameter are available on all hosts in the cluster. Only one ELIM needs to run on the master host because the two resources are the same for all hosts. If the location of the resources is different on different hosts, a different ELIM must run on every host.

## Monitor dynamic shared resources

For LSF to receive external load indexes correctly, the ELIM must send a count of the available resources to standard output in the following format:

```
number_indexes [index_name index_value] ...
```

The fields in this example contain the following information:

```
2 license1 3 license2 2
```

- The total number of external load indexes (2)
- The name of the first external load index (license1)
- The value of the first load index (3)
- The name of the second external load index (license2)
- The value of the second load index (2)

## Write the ELIM program

The ELIM must be an executable program, named elim, located in the **LSF_SERVERDIR** directory.

When the **lim** daemon is started or restarted, it runs the **elim** program on the same host and takes the standard output of the external load indexes that are sent by the **elim** program. In general, you can define any quantifiable resource as an external load index, write an ELIM to report its value, and use it as an LSF resource.

The following example ELIM program uses license1 and license2 and assumes that the FLEXlm license server controls them:

```
#!/bin/sh 
NUMLIC=2           # number of dynamic shared resources
while true
do
TMPLICS='/usr/share/lsf/cluster1/10.1/sparc-sol2/etc/lic -c 
/usr/share/lsf/cluster1/conf/license.dat -f license1, license2'

LICS='echo $TMPLICS | sed -e s/-/_/g'
echo $NUMLIC $LICS # $NUMLIC is number of dynamic shared 
resource
sleep 30           # Resource
done
```

In the script, the **sed** command changes the minus sign (-) to underscore (_) in the license feature names because LSF uses the minus sign for calculation, and it is not allowed in resource names.

The lic utility is available from IBM Support. You can also use the FLEXlm command **lmstat** to make your own ELIM.

## Use the dynamic shared resources

To enable the new shared resources in your cluster, restart LSF with the following commands:

- **lsadmin reconfig**
- **badmin reconfig**

If no errors are found, use the **lsload -l** command to verify the value of your dynamic shared resources:

```
HOST_NAME  status r15s  r1m  r15m  ut   pg   io  ls  it  tmp  swp  mem license1 license2
hosta          ok  0.1  0.3  0.4   8%   0.2  50  73   0  62M  700M 425M       3        0 
hostb          ok  0.1  0.1  0.4   4%   5.7   3   3   0  79M  204M  64M       3        0 
```

## Submit jobs that use shared resources

To submit a batch job that uses one license1 resource, use the command following command:

```
% bsub -R 'rusage[license1=1:duration=1]' myjob
```

In the resource requirement (rusage) string, duration=1 means that license1 is reserved for 1 minute to give LSF time to check it out from FLEXlm.

You can also specify the resource requirement string at queue level, in the **RES_REQ** parameter for the queue. In the LSB_CONFDIR/cluster_name/configdir/lsb.queues file, specify the following resource requirement string:

```
Begin Queue
QUEUE_NAME = license1
RES_REQ=rusage[license1=1:duration=1]
...
End Queue
```

Then, submit a batch job that uses one license1 resource by using the following command:

```
% bsub -q license1 myjob
```

When licenses are available, LSF runs your jobs right away; when all licenses are in use, LSF puts your job in a queue and dispatches them as licenses become available. This way, all of your licenses are used to the best advantage.

## For more information

- For more information about the [lsf.shared](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_config_ref/lsf.shared.5.html?view=kc) and [lsf.cluster.cluster_name](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_config_ref/lsf.cluster.5.html?view=kc) files and the parameters for configuring shared resources, see the [Configuration Reference](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_welcome/lsf_kc_config_ref.html?view=kc).
- For more information about adding external resources to your cluster and configuring an ELIM to customize resources, see [External load indices](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_admin/load_indices_external.html?view=kc) in [Administering IBM Spectrum LSF](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_welcome/lsf_kc_managing.html?view=kc).