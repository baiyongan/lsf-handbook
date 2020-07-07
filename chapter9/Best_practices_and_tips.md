# Chapter 9 经验与建议总结

See various best practices and tips for using LSF.

**[Accounting file management](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/best_practices/Accounting file management.html?view=kc)**
**[Allocating CPUs as blocks for parallel jobs](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/best_practices/allocating_cpu_block_parallel_jobs.html?view=kc)**
Parallel jobs always ask for more than one CPU to run. Some jobs can run faster if the assigned CPUs can be allocated as blocks.**[Cleaning up parallel job execution problems](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/best_practices/Cleaning up parallel job execution problems.html?view=kc)**
**[Configuring IBM Aspera as a data transfer tool](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/dm_using/dm_aspera.html?view=kc)**
IBM Aspera is a data transfer tool that makes efficient, policy-based use of network bandwidth in high latency networks.**[Customizing job query output format](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/best_practices/Customizing job query output format.html?view=kc)**
**[Defining external host-based resources](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/best_practices/Defining external host-based resources.html?view=kc)**
**[Enforcing job memory and swap with Linux cgroups](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/best_practices/Enforcing job memory and swap with Linux cgroups.html?view=kc)**
**[Job access control](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/best_practices/Job access control in LSF.html?view=kc)**
**[Using IBM Spectrum LSF with Andrew File System (AFS)](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/best_practices/afs_integration.html?view=kc)**
Learn how LSF integrates with Andrew File System (AFS) so you can configure LSF to suit your needs.**[Maintaining cluster performance](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/best_practices/Maintaining cluster performance.html?view=kc)**
**[Managing floating software licenses in LSF](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/best_practices/floating_software_licenses.html?view=kc)**
Typically, a pool of floating software licenses is represented by numeric resources in LSF. Every job that requires licenses must include the license requirement in its **rusage** expression to ensure that enough licenses are free for the job at the time that the job is dispatched.**[Optimizing LSF job processing with CPU frequency governors enabled](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/best_practices/Optimizing LSF job processing with CPU frequency governors enabled.html?view=kc)**
**[Operating system partitioning and virtualization on Oracle Solaris and IBM AIX](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/best_practices/os_partition_vm_solaris_aix.html?view=kc)**
This describes how LSF works in an OS partitioning and virtualization environment, focusing on Oracle Solaris containers and IBM AIX partitions.**[Placing jobs based on available job slots of hosts](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/best_practices/Placing jobs based on available job slots of hosts.html?view=kc)**
**[Running checksum to verify installation images](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/best_practices/Running checksum to verify installation images.html?view=kc)**
**[Tracking job dependencies](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/best_practices/Tracking job dependencies in LSF.html?view=kc)**
**[Understanding mbatchd performance metrics](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/best_practices/Understanding mbatchd performance metrics.html?view=kc)**
**[Using compute units for topology scheduling](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/best_practices/Using compute units for topology scheduling.html?view=kc)**
**[Using job directories](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/best_practices/Using job directories.html?view=kc)**
**[Using lsmake to accelerate Android builds](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/best_practices/Using lsmake to accelerate Android builds.html?view=kc)**
**[Using NVIDIA DGX systems with LSF](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/best_practices/Using NVIDIA DGX systems with IBM Spectrum LSF.html?view=kc)**
**[Using ssh X11 forwarding with IBM Spectrum LSF](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/best_practices/ssh_x11_forwarding.html?view=kc)**
For X-enabled applications to function as desired, the X connection must be tunneled over **ssh**, which is the secure method.**[Using the Python wrapper for LSF API](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/best_practices/Using the Python wrapper for LSF API.html?view=kc)**