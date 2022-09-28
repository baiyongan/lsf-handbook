# 7.1 命令参考

IBM Spectrum LSF 命令的参考。

- ##### **[bacct](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_command_ref/bacct.1.html?view=kc)**
  
  Displays accounting statistics about finished jobs.
- ##### **[badmin](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_command_ref/badmin.8.html?view=kc)**
  
  The **badmin** command is the administrative tool for LSF.
- **[bapp](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_command_ref/bapp.1.html?view=kc)**
  Displays information about application profile configuration.
- **[battach](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_command_ref/battach.1.html?view=kc)**
  Runs a shell process to connect to an existing job execution host or container.
- **[battr](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_command_ref/battr.1.html?view=kc)**
  Provides a set of subcommands to manage LSF host attributes for attribute affinity scheduling.
- **[bbot](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_command_ref/bbot.1.html?view=kc)**
  Moves a pending job to the bottom of the queue relative to the last job in the queue.
- **[bchkpnt](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_command_ref/bchkpnt.1.html?view=kc)**
  Checkpoints one or more checkpointable jobs
- **[bclusters](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_command_ref/bclusters.1.html?view=kc)**
  Displays information about IBM Spectrum LSF multicluster capability
- **[bconf](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_command_ref/bconf.8.html?view=kc)**
  Submits live reconfiguration requests, updating configuration settings in active memory without restarting daemons.
- **[bdata](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_command_ref/bdata.1.html?view=kc)**
  Provides a set of subcommands to query and manage IBM Spectrum LSF Data Manager. If no subcommands are supplied, **bdata** displays the command usage.
- **[bentags](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_command_ref/bentags.1.html?view=kc)**
  Queries or removes information about the energy policy tag from the **mbatchd** daemon, which is saved in the energy-aware scheduling database. Used with energy policy, or energy aware scheduling feature.
- **[bgadd](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_command_ref/bgadd.1.html?view=kc)**
  Creates job groups
- **[bgdel](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_command_ref/bgdel.1.html?view=kc)**
  Deletes job groups
- **[bgmod](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_command_ref/bgmod.1.html?view=kc)**
  Modifies job groups
- **[bgpinfo](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_command_ref/bgpinfo.1.html?view=kc)**
  Displays information about global fairshare.
- **[bhist](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_command_ref/bhist.1.html?view=kc)**
  Displays historical information about jobs
- **[bhosts](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_command_ref/bhosts.1.html?view=kc)**
  Displays hosts and their static and dynamic resources
- **[bhpart](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_command_ref/bhpart.1.html?view=kc)**
  Displays information about host partitions
- **[bimages](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_command_ref/bimages.1.html?view=kc)**
  Displays information on Docker container images
- **[bjdepinfo](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_command_ref/bjdepinfo.1.html?view=kc)**
  Displays job dependencies.
- **[bjgroup](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_command_ref/bjgroup.1.html?view=kc)**
  Displays information about job groups
- **[bjobs](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_command_ref/bjobs.man_top.1.html?view=kc)**
  Displays and filters information about LSF jobs. Specify one or more job IDs (and, optionally, an array index list) to display information about specific jobs (and job arrays).
- **[bkill](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_command_ref/bkill.1.html?view=kc)**
  Sends signals to kill, suspend, or resume unfinished jobs
- **[bladmin](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_command_ref/bladmin.8.html?view=kc)**
  Administrative tool for IBM Spectrum LSF License Scheduler.
- **[blaunch](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_command_ref/blaunch.8.html?view=kc)**
  Launches parallel tasks on a set of hosts.
- **[blcollect](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_command_ref/blcollect.1.html?view=kc)**
  License information collection daemon for LSF License Scheduler. The **blcollect** daemon collects license usage information.
- **[blcstat](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_command_ref/blcstat.1.html?view=kc)**
  Displays dynamic update information from the **blcollect** daemon for LSF License Scheduler.
- **[blhosts](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_command_ref/blhosts.1.html?view=kc)**
  Displays the names of all the hosts that are running the LSF License Scheduler daemon (bld).
- **[blimits](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_command_ref/blimits.1.html?view=kc)**
  Displays information about resource allocation limits of running jobs.
- **[blinfo](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_command_ref/blinfo.1.html?view=kc)**
  Displays static LSF License Scheduler configuration information
- **[blkill](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_command_ref/blkill.1.html?view=kc)**
  Terminates an interactive (**taskman**) LSF License Scheduler task.
- **[blparams](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_command_ref/blparams.1.html?view=kc)**
  Displays information about configurable LSF License Scheduler parameters that are defined in the files lsf.licensescheduler and lsf.conf
- **[blstat](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_command_ref/blstat.1.html?view=kc)**
  Displays dynamic license information.
- **[bltasks](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_command_ref/bltasks.1.html?view=kc)**
  Displays LSF License Scheduler interactive task information.
- **[blusers](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_command_ref/blusers.1.html?view=kc)**
  Displays license usage information for LSF License Scheduler.
- **[bmgroup](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_command_ref/bmgroup.1.html?view=kc)**
  Displays information about host groups and compute units.
- **[bmig](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_command_ref/bmig.1.html?view=kc)**
  Migrates checkpointable or rerunnable jobs.
- **[bmod](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_command_ref/bmod.1.html?view=kc)**
  Modifies job submission options of a job.
- **[bparams](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_command_ref/bparams.1.html?view=kc)**
  Displays information about configurable system parameters in the lsb.params file.
- **[bpeek](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_command_ref/bpeek.1.html?view=kc)**
  Displays the stdout and stderr output of an unfinished job.
- **[bpost](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_command_ref/bpost.1.html?view=kc)**
  Sends external status messages and attaches data files to a job.
- **[bqueues](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_command_ref/bqueues.1.html?view=kc)**
  Displays information about queues.
- **[bread](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_command_ref/bread.1.html?view=kc)**
  Reads messages and attached data files from a job.
- **[brequeue](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_command_ref/brequeue.1.html?view=kc)**
  Kills and requeues a job.
- **[bresize](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_command_ref/bresize.1.html?view=kc)**
  Decreases or increases tasks that are allocated to a running resizable job, or cancels pending job resize allocation requests.
- **[bresources](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_command_ref/bresources.1.html?view=kc)**
  Displays information about resource reservation, resource limits, and guaranteed resource policies.
- **[brestart](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_command_ref/brestart.1.html?view=kc)**
  Restarts checkpointed jobs.
- **[bresume](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_command_ref/bresume.1.html?view=kc)**
  Resumes one or more suspended jobs.
- **[brlainfo](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_command_ref/brlainfo.1.html?view=kc)**
  Displays host topology information.
- **[brsvadd](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_command_ref/brsvadd.8.html?view=kc)**
  Adds an advance reservation.
- **[brsvdel](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_command_ref/brsvdel.8.html?view=kc)**
  Deletes an advance reservation.
- **[brsvjob](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_command_ref/brsvjob.1.html?view=kc)**
  Shows information about jobs submitted with the **brsvsub** command to a specific advance reservation.
- **[brsvmod](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_command_ref/brsvmod.8.html?view=kc)**
  Modifies an advance reservation.
- **[brsvs](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_command_ref/brsvs.1.html?view=kc)**
  Displays advance reservations.
- **[brsvsub](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_command_ref/brsvsub.1.html?view=kc)**
  Creates a dynamically scheduled reservation and submits a job to fill the advance reservation when the resources required by the job are available.
- **[brun](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_command_ref/brun.8.html?view=kc)**
  Forces a job to run immediately.
- **[bsla](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_command_ref/bsla.1.html?view=kc)**
  Displays information about service classes. Service classes are used in guaranteed resource policies and service-level agreement (SLA) scheduling.
- **[bslots](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_command_ref/bslots.1.html?view=kc)**
  Displays slots available and backfill windows available for backfill jobs.
- **[bstage](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_command_ref/bstage.1.html?view=kc)**
  Stages data files for jobs with data requirements by copying files or creating symbolic links for them between the local staging cache and the job execution environment. You must run **bstage** only within the context of an LSF job (like **blaunch**). To access a file with the **bstage** command, you must have permission to read it.
- **[bstatus](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_command_ref/bstatus.1.html?view=kc)**
  Gets current external job status or sets new job status.
- **[bstop](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_command_ref/bstop.1.html?view=kc)**
  Suspends unfinished jobs.
- **[bsub](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_command_ref/bsub.man_top.1.html?view=kc)**
  Submits a job to LSF by running the specified command and its arguments.
- **[bswitch](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_command_ref/bswitch.1.html?view=kc)**
  Switches unfinished jobs from one queue to another.
- **[btop](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_command_ref/btop.1.html?view=kc)**
  Moves a pending job relative to the first job in the queue.
- **[bugroup](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_command_ref/bugroup.1.html?view=kc)**
  Displays information about user groups.
- **[busers](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_command_ref/busers.1.html?view=kc)**
  Displays information about users and user groups.
- **[bwait](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_command_ref/bwait.1.html?view=kc)**
  Pauses and waits for the job query condition to be satisfied.
- **[ch](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_command_ref/ch.1.html?view=kc)**
  Changes the host where subsequent commands run.
- **[gpolicyd](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_command_ref/gpolicyd.8.html?view=kc)**
  Displays LSF global policy daemon information.
- **[lim](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_command_ref/lim.8.html?view=kc)**
  Load information manager (LIM) daemon or service, monitoring host load.
- **[lsacct](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_command_ref/lsacct.1.html?view=kc)**
  Displays accounting statistics on finished RES tasks in the LSF system.
- **[lsacctmrg](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_command_ref/lsacctmrg.1.html?view=kc)**
  Merges LSF RES task log files.
- **[lsadmin](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_command_ref/lsadmin.8.html?view=kc)**
  Administrative tool to control LIM and RES daemon operations in LSF.
- **[lsclusters](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_command_ref/lsclusters.1.html?view=kc)**
  Displays configuration information about LSF clusters.
- **[lseligible](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_command_ref/lseligible.1.html?view=kc)**
  Displays whether a task is eligible for remote execution.
- **[lsfinstall](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_command_ref/lsfinstall.8.html?view=kc)**
  The LSF installation and configuration script.
- **[lsfmon](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_command_ref/lsfmon.1.html?view=kc)**
  Install or uninstall LSF Monitor in an existing cluster.
- **[lsfrestart](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_command_ref/lsfrestart.8.html?view=kc)**
  Restarts the LIM, RES, **sbatchd**, and **mbatchd** daemons on all hosts in the cluster
- **[lsfshutdown](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_command_ref/lsfshutdown.8.html?view=kc)**
  Shuts down the LIM, RES, **sbatchd**, and **mbatchd** daemons on all hosts in the cluster.
- **[lsfstartup](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_command_ref/lsfstartup.8.html?view=kc)**
  Starts the LIM, RES, and **sbatchd** daemons on all hosts in the cluster.
- **[lsgrun](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_command_ref/lsgrun.1.html?view=kc)**
  Runs a task on a group of hosts.
- **[lshosts](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_command_ref/lshosts.1.html?view=kc)**
  Displays hosts and their static resource information.
- **[lsid](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_command_ref/lsid.1.html?view=kc)**
  Displays the LSF version number, the cluster name, and the master host name.
- **[lsinfo](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_command_ref/lsinfo.1.html?view=kc)**
  Displays LSF configuration information.
- **[lsload](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_command_ref/lsload.1.html?view=kc)**
  Displays load information for hosts.
- **[lsloadadj](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_command_ref/lsloadadj.1.html?view=kc)**
  Adjusts load indices on hosts.
- **[lslogin](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_command_ref/lslogin.1.html?view=kc)**
  Remotely logs in to a lightly loaded host.
- **[lsltasks](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_command_ref/lsltasks.1.html?view=kc)**
  Displays or updates a local task list.
- **[lsmake](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_command_ref/lsmake.1.html?view=kc)**
  Runs LSF **make** tasks in parallel.
- **[lsmon](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_command_ref/lsmon.1.html?view=kc)**
  Displays load information for LSF hosts and periodically updates the display.
- **[lspasswd](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_command_ref/lspasswd.1.html?view=kc)**
  Registers Windows user passwords in LSF. Passwords must be 3 - 23 characters long.
- **[lsplace](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_command_ref/lsplace.1.html?view=kc)**
  Displays hosts available to run tasks.
- **[lsportcheck](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_command_ref/lsportcheck.1.html?view=kc)**
  Displays ports that LSF is currently using or the LSF ports that will be used before starting LSF.
- **[lsrcp](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_command_ref/lsrcp.1.html?view=kc)**
  Remotely copies files through LSF.
- **[lsreghost (UNIX)](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_command_ref/lsreghost.1.html?view=kc)**
  UNIX version of the **lsreghost** command registers UNIX LSF host names and IP addresses with LSF servers so that LSF servers can internally resolve these hosts without requiring a DNS server.
- **[lsreghost (Windows)](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_command_ref/lsreghost_win.1.html?view=kc)**
  Windows version of the **lsreghost** command registers Windows LSF host names and IP addresses with LSF servers so that LSF servers can internally resolve these hosts without requiring a DNS server.
- **[lsrtasks](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_command_ref/lsrtasks.1.html?view=kc)**
  Displays or updates a remote task list.
- **[lsrun](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_command_ref/lsrun.1.html?view=kc)**
  Runs an interactive task through LSF.
- **[lstcsh](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_command_ref/lstcsh.1.html?view=kc)**
  Load sharing tcsh for LSF
- **[pam](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_command_ref/pam.1.html?view=kc)**
  Parallel Application Manager – job starter for MPI applications
- **[patchinstall](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_command_ref/patchinstall.8.html?view=kc)**
  UNIX only. Manage patches in LSF cluster.
- **[pversions (UNIX)](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_command_ref/pversions.8.html?view=kc)**
  UNIX version of the command. Displays the version information for IBM Spectrum LSF installed on UNIX hosts.
- **[pversions (Windows)](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_command_ref/pversions_win.8.html?view=kc)**
  Windows version of the command. Displays the version information for IBM Spectrum LSF installed on a Windows host.
- **[ssacct](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_command_ref/ssacct.1.html?view=kc)**
  Displays accounting statistics about finished LSF session scheduler jobs.
- **[ssched](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_command_ref/ssched.1.html?view=kc)**
  Submit tasks through LSF session scheduler.
- **[taskman](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_command_ref/taskman.1.html?view=kc)**
  Checks out a license token and manages interactive UNIX applications.
- **[tspeek](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_command_ref/tspeek.1.html?view=kc)**
  Displays the stdout and stderr output of an unfinished Terminal Services job.
- **[tssub](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_command_ref/tssub.1.html?view=kc)**
  Submits a Terminal Services job to LSF.
- **[wgpasswd](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_command_ref/wgpasswd.1.html?view=kc)**
  Changes a user’s password for a Microsoft Windows workgroup.
- **[wguser](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_command_ref/wguser.8.html?view=kc)**
  Modifies user accounts for a Microsoft Windows workgroup

