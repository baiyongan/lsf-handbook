# Chapter09 Best practices and tips

See various best practices and tips for using LSF.

## IBM Spectrum LSF accounting file management
LSF uses accounting files to track resource allocation and usage for all finished jobs. This is the primary purpose of the lsb.acct file.

## Additional configuration settings
This topic describes additional configuration settings that you can use as an example for your own cluster. Some of the following parameters are explicitly set to the default value, but you can edit these to suit your own cluster.

## Allocating CPUs as blocks for parallel jobs
Parallel jobs always ask for more than one CPU to run. Some jobs can run faster if the assigned CPUs can be allocated as blocks.

## Cleaning up IBM Spectrum LSF parallel job execution problems
The LSF distributed application integration framework blaunch offers full control of parallel jobs running across multiple execution hosts.

## Configuring IBM Aspera as a data transfer tool
IBM Aspera is a data transfer tool that makes efficient, policy-based use of network bandwidth in high latency networks.

## Customizing output format and reducing network traffic for IBM Spectrum LSF job queries
The default bjobs command output provides basic job information. When you need additional job information, you might prefer to have the job output displayed line by line. Controlling the format of bjobs output can also make the output easily parsed by scripts and also reduce network traffic by transferring only the required information from mbatchd to the bjobs command.

## Defining external host-based resources in IBM Spectrum LSF
This article describes how to define site-specific external resources on hosts in the cluster for scheduling purposes.

## Enforcing IBM Spectrum LSF job memory and swap with Linux cgroups
Enable cgroup memory and swap enforcement in LSF.

## Applying job access control in IBM Spectrum LSF to protect information privacy
The LSF access control level (ACL) feature supports different levels of access control in job information queries.

## IBM Spectrum LSF job directories
LSF uses different types of directories for jobs to use during execution.

## Using IBM Spectrum LSF with Andrew File System (AFS)
Learn how LSF integrates with Andrew File System (AFS) so you can configure LSF to suit your needs.

## Maintaining cluster performance under high query load
LSF provides basic performance metrics (badmin perfmon), which samples three major query operations (bjobs, bhosts, and bqueues). LSF also provides the badmin diagnose -c query command option to trace query sources for further troubleshooting.

## Managing floating software licenses in LSF
Typically, a pool of floating software licenses is represented by numeric resources in LSF. Every job that requires licenses must include the license requirement in its rusage expression to ensure that enough licenses are free for the job at the time that the job is dispatched.

## Maintaining cluster performance under high query load
Optimize LSF job processing when jobs have a long run time in LSF when CPU frequency governors are enabled, but run faster when executed directly on the machine.

## Operating system partitioning and virtualization on Oracle Solaris and IBM AIX
This describes how LSF works in an OS partitioning and virtualization environment, focusing on Oracle Solaris containers and IBM AIX partitions.

## Performance metrics for mbatchd
LSF mbatchd performance metrics help administrators to identify the root causes of mbatchd performance issues when they occur, so that administrators can take appropriate corrective actions. These performance metrics are particularly useful when the cause of issue is related to the cluster environment; for example, the performance of shared storage or a network connection.

## Placing jobs based on available job slots of hosts
LSF has built-in host-based resource slots to support the placement of jobs based on available job slots. Learn how to configure and use the slots resource with existing LSF resource requirements according to a packing or spreading policy.

## Locating the sha1 checksum after downloading the IBM Spectrum LSF installers
Use the sha1 executable file to verify the LSF installation files.

## Tracking job dependencies in IBM Spectrum LSF
Use LSF job dependencies to specify the job execution flow during job submission.

## Using compute units to have IBM Spectrum LSF consider cluster topology when scheduling
Use the LSF compute unit (CU) feature to have LSF consider a tree-like network topology when scheduling jobs.

## Using lsmake to accelerate building Android source code
The LSF lsmake tool is a parallel GNU make that is tightly integrated with LSF.

## Using NVIDIA DGX systems with IBM Spectrum LSF
The following guide is an example of how to use LSF with GPU resources on NVIDIA DGX systems.

## Using ssh X11 forwarding with IBM Spectrum LSF
For X-enabled applications to function as desired, the X connection must be tunneled over ssh, which is the secure method.

## Using the IBM Spectrum LSF API Python wrapper
The Python wrapper for IBM Spectrum LSF APIs allows users to call the LSF APIs from Python. You create a Python wrapper using the Simplified Wrapper and Interface Generator (SWIG), which is the tool used for interfacing the LSF C APIs and Python.