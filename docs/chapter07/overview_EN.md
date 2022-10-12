# Chapter07 LSF related tools

## Using IBM Spectrum LSF on Windows

!!! info
    Install, configure and use LSF on Microsoft Windows.

### Test your LSF installation
### LSF default user mapping
### Environment
### Charting resources with Windows Performance Monitor
### Dynamic IP addressing for LSF hosts
### Displaying a GUI in LSF with Microsoft Terminal Services
### Installing LSF in a mixed cluster


## IBM Spectrum LSF License Scheduler

!!! info
    Install, configure, and use IBM Spectrum LSF License Scheduler (LSF License Scheduler). 
    
    Learn to make policies that control how your software application licenses are shared among different users or projects in your organization.

### Introduction
### Installing and starting License Scheduler
### LSF License Scheduler concepts
### Configuring License Scheduler
### Viewing information and troubleshooting
### Reference


## IBM Spectrum LSF Data Manager

!!! info
    Configure, manage, and use LSF Data Manager to enable your applications to access the data they require to complete computations unhindered by the location of the data in relation to the application. 
    
    LSF Data Manager solves the problem of data locality by staging required data files as closely as possible to your applications. 
    
    You can stage input data from an external source repository to the cluster execution hosts, and stage output data asynchronously to an external destination repository after job completion.

### About IBM Spectrum LSF Data Manager
When large amounts of data are required to complete computations, it is desirable that your applications access required data unhindered by the location of the data in relation to the application execution environment. LSF Data Manager solves the problem of data locality by staging the required data as closely as possible to the site of the application.

### Plan and install IBM Spectrum LSF Data Manager
Plan and install IBM Spectrum LSF Data Manager in a simple single cluster with a single LSF data manager.

### Use IBM Spectrum LSF Data Manager
Submit, control and monitor jobs with data requirements to IBM Spectrum LSF Data Manager.

### Administering IBM Spectrum LSF Data Manager
The administrator of IBM Spectrum LSF Data Manager is an LSF administrator who performs tasks that are specific to LSF Data Manager.

### Command reference for IBM Spectrum LSF Data Manager
Use the bsub command to submit a job with data requirements to LSF. Use the bdata command to query and manage IBM Spectrum LSF Data Manager. The bjobs command displays and filters information about LSF jobs. Use the bstage command to stage data files for jobs with data requirements.

### Configuration Reference for IBM Spectrum LSF Data Manager
Configure LSF data manager in the lsb.queues, lsf.conf, and lsf.datamanager configuration files.


## Using the IBM Spectrum LSF Resource Connector

!!! info
    Configure and use IBM Spectrum LSF resource connector.

### IBM Spectrum LSF resource connector overview
The resource connector for IBM Spectrum LSF feature (previously referred to as host factory) enables LSF clusters to borrow resources from supported resource providers.
### Configuring resource providers for LSF resource connector
Modify resource connector configuration files after installation to enable resource providers.

### Updating LSF configuration for resource connector
Configure LSF to enable the resource connector.

### View information on the LSF resource connector
View information on the LSF resource connector by checking the status of the ebrokerd daemon, running the badmin rc subcommand, or by viewing the log files.

### LSF resource connector configuration reference
Reference for configuring LSF resource connector.


## Using the LSF Connector for Kubernetes

!!! info
    Configure and use LSF Connector for Kubernetes.

### Overview of LSF Connector for Kubernetes
IBM Spectrum LSF Connector for Kubernetes (LSF Connector for Kubernetes) uses the core IBM Spectrum LSF (LSF) scheduling technology and is integrated into Kubernetes.

### Limitations with LSF Connector for Kubernetes
Certain LSF features, commands, and command options are not supported with Kubernetes jobs.

### Installing LSF Connector for Kubernetes
Verify the prerequisites, install LSF Connector for Kubernetes and deploy the jobs.

### Configuring IBM Spectrum LSF Connector for Kubernetes
Configure LSF Connector for Kubernetes by creating the kubernetes.config file and applying that file to the LSF cluster.

### Verifying the LSF Connector for Kubernetes deployment
Verify that LSF Connector for Kubernetes is working correctly.

### Deploying Kubernetes jobs in LSF Connector for Kubernetes
LSF Connector for Kubernetes enables new options for jobs that are run through Kubernetes. These options are needed for running High Performance Computing (HPC) applications and large AI jobs.

### Submitting Kubernetes jobs
The LSF Connector for Kubernetes allows workload to be run in a Kubernetes pod. You either submit the work to LSF or to Kubernetes and LSF schedules the work based on configured LSF policies.


