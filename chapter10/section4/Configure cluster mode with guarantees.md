# Configure cluster mode with guarantees

Cluster mode distributes licenses across LSF clusters. To guarantee license resources to projects within a cluster and allow loaning of license resources when not in use, use LSF guarantee-type SLAs. Guarantees and loans in cluster mode are similar to non-shared licenses and ownership in project mode.

A guarantee provides jobs that belong to set consumers with specific resources (such as hosts). Jobs run with guaranteed resources when possible. When the guaranteed resources are used, jobs run outside the guarantee following whatever other scheduling features are configured. Guarantees are configured within a guaranteed resource pool.

Guarantee SLAs are configured in LSF. For more information, see Administering IBM Spectrum LSF and the IBM Spectrum LSF Configuration Reference.

**Parent topic:**

[Configuring License Scheduler](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/license_scheduler/chap_config_ls.html?view=kc)

## Configure service classes

### About this task

Service classes allow access to guaranteed resources. Configure a service class for each license project in the cluster.

### Procedure

Configure each ServiceClass section in the lsb.serviceclasses file. Begin with the line Begin ServiceClass and end with the line End ServiceClass. For each service class, you must specify:

1. NAME: the name of the service class.
2. GOALS = [GUARANTEE]
3. Optional parameters for the ServiceClass section are ACCESS_CONTROL, AUTO_ATTACH, and DESCRIPTION.

You can configure as many service class sections as you need.

**Important**

The name that you use for your service class cannot be the same as an existing host partition or user group name.

```
Begin ServiceClass
NAME = sla1
GOALS = [GUARANTEE]
ACCESS_CONTROL=LIC_PROJECTS[ proj1 ]
DESCRIPTION = A guarantee SLA with access restricted to the license project proj1.
End ServiceClass
```

### Automatically attach jobs to service classes

#### About this task

When the optional parameter **AUTO_ATTACH** is set, jobs are automatically attached to the service class.

When automatic attachment is not set, jobs can be submitted to the service class by running bsub -sla serviceclass_name.

If a job can access more than one SLA with automatic attachment set, it is attached to the first valid SLA in the order of the configuration file.

#### Procedure

Set AUTO_ATTACH=Y in the ServiceClass section in the lsb.serviceclasses file.

```
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

## Configure a resource pool of license tokens

### About this task

Guaranteed resource pools provide a minimum resource guarantee to consumers, and can optionally loan out guaranteed resources not in use.

Guaranteed resource pools are defined in lsb.resources and used by consumers that are defined within ServiceClass sections in lsb.serviceclasses.

### Procedure

Configure a GuaranteedResourcePool section in lsb.resources. Begin with the line Begin GuaranteedResourcePool and end with the line End GuaranteedResourcePool. Specify the following parameters:

1. NAME: the name of the guaranteed resource pool.
2. TYPE: the guarantee type. For licenses, use the type resources and include the name of the license feature.
3. DISTRIBUTION: share assignments for all service classes using the resource pool. Can be percent or absolute numbers.
4. Optional parameters for GuaranteedResourcePool sections of resources are LOAN_POLICIES, and DESCRIPTION.

You can configure as many resource pools as you need. One resource pool can be used by several SLAs, and one SLA can access multiple resource pools.

```
Begin GuaranteedResourcePool
NAME = hspice_guarantees
TYPE = resource[hspice]
DISTRIBUTION = ([proj1_sc,50%][proj2_sc,50%])
DESCRIPTION = A resource pool of hspice licenses controlled by License Scheduler
and used by proj1_sc and proj2_sc.
End GuaranteedResourcePool
```

## Configure loans

### About this task

Loans from unused guarantees are recommended when you are using cluster mode. When loans are disabled, use a static license distribution policy.

When configured, unused license resources are loaned out based on the loan policy. The loan policy allows specific queues to access unused resources from guaranteed resource pools.

### Procedure

1. Configure a guaranteed resource pool in lsb.resources with the required **NAME**, **TYPE**, and **DISTRIBUTION** parameters.

2. Add a loan policy to the guaranteed resource pool.

   Use **LOAN_POLICIES= QUEUES[queue_name]** to specify which queues can access loaned resources. Use the keyword **all** to loan to jobs from any queue.

   For example, the following policy allows loans to jobs from the queue my_queue:

   ```
   Begin GuaranteedResourcePool
   ...
   LOAN_POLICIES = QUEUES[my_queue]
   ...
   End GuaranteedResourcePool
   ```

### Configure loans to short jobs

#### About this task

Loans can be restricted based on job run time, or estimated run time.

#### Procedure

Add the policy DURATION[minutes] to the guaranteed resource pool configuration in lsb.resources, where minutes is an integer.

Use DURATION to set a maximum job runtime limit (or estimated run time, whichever is shorter) for jobs to borrow resources. Omit **DURATION** completely to allow jobs with any run time to borrow from the guarantee.

For example, the following policy allows loans to jobs from any queue with a run time of 10 minutes or less:

```
Begin GuaranteedResourcePool
...
LOAN_POLICIES = QUEUES[all] DURATION[10]
...
End GuaranteedResourcePool
```

### Configure loans to stop when jobs are waiting for guaranteed resources

#### About this task

Loans can be restricted so that jobs have access to the loaned resources only when consumers with unused guaranteed resources do not have pending loads.

Restricting loans is useful when running jobs that require several licenses. With restricted loans enabled, loaning out single licenses does not delay jobs that are waiting for license resources to accumulate.

#### Procedure

Add the policy CLOSE_ON_DEMAND to the guaranteed resource pool configuration in lsb.resources.

```
Begin GuaranteedResourcePool
...
LOAN_POLICIES = QUEUES[queue1] CLOSE_ON_DEMAND
...
End GuaranteedResourcePool
```

## Configure a queue with access to all guaranteed resources

### About this task

Queues with high priority (such as administrator test queues) can be configured with access to all guaranteed resources, regardless of SLA demand.

### Procedure

Configure a queue in the lsb.queues file with the **SLA_GUARANTEES_IGNORE = Y** parameter.

**Note**

Using **SLA_GUARANTEES_IGNORE = Y** defeats the purpose of guaranteeing resources. Use this parameter sparingly for low traffic queues only.

## Restart for changes to take effect

### About this task

Cluster mode must be enabled, and LSF clusters must be restarted for LSF configuration changes to take effect.

### Procedure

1. In the Parameters section of lsf.licensescheduler, confirm cluster mode is enabled (CLUSTER_MODE=Y).
2. Run badmin mbdrestart to restart each LSF cluster.
3. Run bladmin reconfig to restart the bld.

## View guaranteed resource pools

### About this task

Guaranteed resource pool configuration includes the resource type, and distribution among consumers that are defined in the corresponding service classes.

### Procedure

Run **bresources -g -l -m** to see details of the guaranteed resource pool configuration, including a list of hosts currently in the resource pool.