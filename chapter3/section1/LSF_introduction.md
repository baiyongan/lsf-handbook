# LSF 介绍

The IBM Spectrum LSF ("LSF", short for load sharing facility) software is industry-leading enterprise-class software. LSF distributes work across existing heterogeneous IT resources to create a shared, scalable, and fault-tolerant infrastructure, that delivers faster, more reliable workload performance and reduces cost. LSF balances load and allocates resources, and provides access to those resources.

LSF provides a resource management framework that takes your job requirements, finds the best resources to run the job, and monitors its progress. Jobs always run according to host load and site policies.

![A typical LSF Cluster](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_foundations/lsf_cluster_overview.jpg)



## Cluster

A group of computers (hosts) running LSF that work together as a single unit, combining computing power, workload, and resources. A cluster provides a single-system image for a network of computing resources.

Hosts can be grouped into a cluster in a number of ways. A cluster can contain:

- All the hosts in a single administrative group
- All the hosts on a subnetwork

### Hosts

Hosts in your cluster perform different functions.

- Master host

  LSF server host that acts as the overall coordinator for the cluster, doing all job scheduling and dispatch.

- Server host

  A host that submits and runs jobs.

- Client host

  A host that only submits jobs and tasks.

- Execution host

  A host that runs jobs and tasks.

- Submission host

  A host from which jobs and tasks are submitted.

## Job

A unit of work that is running in the LSF system. A job is a command that is submitted to LSF for execution. LSF schedules, controls, and tracks the job according to configured policies.

Jobs can be complex problems, simulation scenarios, extensive calculations, or anything that needs compute power.

## Job slot

A job slot is a bucket into which a single unit of work is assigned in the LSF system.

Hosts can be configured with multiple job slots and you can dispatch jobs from queues until all the job slots are filled. You can correlate job slots with the total number of CPUs in the cluster.

## Queue

A cluster-wide container for jobs. All jobs wait in queues until they are scheduled and dispatched to hosts.

Queues do not correspond to individual hosts; each queue can use all server hosts in the cluster, or a configured subset of the server hosts.

When you submit a job to a queue, you do not need to specify an execution host. LSF dispatches the job to the best available execution host in the cluster to run that job.

Queues implement different job scheduling and control policies.

## Resources

Resources are the objects in your cluster that are available to run work. For example, resources include but are not limited to hosts, CPU slots, and licenses.