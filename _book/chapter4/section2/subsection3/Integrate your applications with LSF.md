# Integrate your applications with LSF

By integrating your applications with LSF, you can make sure that your users can submit and run their jobs with correct and complete job submission options without making them learn LSF commands.

Integrate applications with LSF three ways:

- Wrapper shell scripts
- Wrapper binary executables
- Modifying existing application source code and interfaces

## Wrapper shell scripts

The easiest integration method is to put the **bsub** command into an executable file like a shell script. A wrapper script is an executable file for launching your application through LSF. It gives users a simple interface to run their jobs that is easy to deploy and maintain.

For example, if your application is called abc, rename abc to abc_real and create a wrapper script that is called abc:

```
#! /bin/sh
bsub -R "rusage[abc_license=1:duration=1]" abc_real
```

When users run abc, they are actually running a script to submit a job abc_real to LSF that uses 1 shared resource named abc_license.

For more information about specifying shared resources by using the resource requirement (rusage) string on the -R option of the **bsub** command, see [Manage software licenses and other shared resources](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_admin_foundations/shared_resource.html?view=kc#chared_resource39847).

By adding appropriate options to the script, you can enhance your integration:

- Requeue jobs based on license availability
- Copy input and output files to and from the local directory on the execution host
- Calculate and estimate resource requirements

## Wrapper binary programs

A wrapper binary is similar to a wrapper shell script in the form of a compiled binary executable. Compiled wrapper files usually run faster and more efficiently than shell scripts, and they also have access to the LSF API (LSLIB and LSBLIB). Binary code is also more secure because users cannot modify it without the source code and appropriate libraries, but it is more time consuming to develop wrapper binary programs than wrapper shell scripts.

## Modifying existing application source code and interfaces

LSF is already integrated closely with many commonly used software products. IBM and other software application vendors provide facilities and services for closer integration of LSF and other applications. By modifying existing application user interfaces, you can enable easy job submission, license maximization, parallel execution, and other advanced LSF features. In some cases, you are able to run an LSF job directly from the application user interface.

## Where to go next

Learn more about administering your cluster, described in [Manage users, hosts, and queues](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_admin_foundations/manage_users_hosts_queues.html?view=kc).