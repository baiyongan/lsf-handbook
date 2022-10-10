# Chapter02 LSF foundations

Get an overview of IBM Spectrum LSF workload management concepts and operations for both users and administrators.

## IBM Spectrum LSF user foundations
Get an overview of IBM Spectrum LSF workload management concepts and operations.

### IBM Spectrum LSF overview
Learn how LSF takes your job requirements and finds the best resources to run the job.

#### Introduction to IBM Spectrum LSF
The IBM Spectrum LSF ("LSF", short for load sharing facility) software is industry-leading enterprise-class software. LSF distributes work across existing heterogeneous IT resources to create a shared, scalable, and fault-tolerant infrastructure, that delivers faster, more reliable workload performance and reduces cost. LSF balances load and allocates resources, and provides access to those resources.

#### LSF cluster components
An LSF cluster manages resources, accepts and schedules workload, and monitors all events. LSF can be accessed by users and administrators by a command-line interface, an API, or through the IBM Spectrum LSF Application Center

### Inside an LSF cluster
Learn about the various daemon processes that run on LSF hosts, LSF cluster communications paths, and how LSF tolerates host failure in the cluster.

### Inside workload management
Understand the LSF job lifecycle. Use the bsub to submit jobs to a queue and specify job submission options to modify the default job behavior. Submitted jobs wait in queues until they are scheduled and dispatched to a host for execution. At job dispatch, LSF checks to see which hosts are eligible to run the job.

### LSF with EGO enabled
Enable the enterprise grid orchestrator (EGO) with LSF to provide a system infrastructure to control and manage cluster resources. Resources are physical and logical entities that are used by applications. LSF resources are shared as defined in the EGO resource distribution plan.

## IBM Spectrum LSF administrator foundations
Get an administrator overview of IBM Spectrum LSF how to manage various types of workload and cluster operations.

### LSF cluster overview
Get an overview of your cluster and the location of important LSF directories and configuration files.

### Work with LSF
Start and stop LSF daemons, and reconfigure cluster properties. Check LSF status and submit LSF jobs.

### Troubleshooting LSF problems
Troubleshoot common LSF problems and understand LSF error messages. If you cannot find a solution to your problem here, contact IBM Support.