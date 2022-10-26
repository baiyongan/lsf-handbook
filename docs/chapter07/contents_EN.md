# Contents

## LSF on Windows
- [ ] Test your LSF installation
- [ ] LSF default user mapping
- [ ] Environment
- [ ] Charting resources with Windows Performance Monitor
- [ ] Dynamic IP addressing for LSF hosts
- [ ] Displaying a GUI in LSF with Microsoft Terminal Services
- [ ] Installing LSF in a mixed cluster

## LSF License Scheduler
   
### Introduction
- [ ] Overview
- [ ] Differences between LSF License Scheduler editions
- [ ] Glossary
- [ ] Architecture

### Installing and starting License Scheduler
- [ ] Install License Scheduler
    - [ ] Before you install
    - [ ] What the License Scheduler setup script does
    - [ ] Install License Scheduler with LSF (UNIX)
    - [ ] Install License Scheduler on Windows
        - [ ] Install License Scheduler with LSF (Windows)
    - [ ] Troubleshoot
    - [ ] Configure LSF License Scheduler Basic Edition
- [ ] Start License Scheduler
- [ ] LSF parameters in License Scheduler
- [ ] About submitting jobs
- [ ] After configuration changes
- [ ] Add a cluster to License Scheduler
- [ ] Configure multiple administrators
- [ ] Upgrade License Scheduler
- [ ] Firewalls

### LSF License Scheduler concepts
- [ ] License Scheduler modes
- [ ] Project groups
- [ ] Service domains in License Scheduler
- [ ] Distribution policies
- [ ] Project mode preemption
    - [ ] Preemption restrictions
    - [ ] LSF preemption with License Scheduler preemption
- [ ] License usage with FlexNet and Reprise License Manager
    - [ ] Known license requirements
    - [ ] Unknown license requirements
    - [ ] Project mode
    - [ ] Cluster mode
    - [ ] Reserved FlexNet Manager licenses

### Configuring License Scheduler
- [ ] Configure cluster mode
- [ ] Configure cluster mode with guarantees
- [ ] Project mode with projects
- [ ] Project mode with project groups
- [ ] Project mode optional settings
    - [ ] Active ownership
    - [ ] Default project
    - [ ] Groups of projects
        - [ ] Configure group license ownership
    - [ ] Interactive (taskman) jobs
    - [ ] Cluster and interactive allocations
    - [ ] Feature groups
        - [ ] View license feature group information
    - [ ] License feature locality
        - [ ] Submit jobs that use locality
        - [ ] How locality works with other settings
    - [ ] Hierarchical project group paths
    - [ ] Demand limits
    - [ ] Configure lmremove or rlmremove preemption
    - [ ] Restart to implement configuration changes
- [ ] Fast dispatch project mode
    - [ ] Configure lmremove or rlmremove preemption
- [ ] Automatic time-based configuration
    - [ ] Failover
    - [ ] Failover provisioning for LANs
    - [ ] Failover provisioning for WANs
        - [ ] Configure and start License Scheduler in a WAN
        - [ ] WAN example
        - [ ] Service provisioning at the host and network levels
    - [ ] Set up fod
- [ ] User authentication

### Viewing information and troubleshooting
- [ ] About viewing available licenses
    - [ ] View license server and license feature information passed to jobs
    - [ ] Customize dynamic license information output
- [ ] About error logs
    - [ ] Manage log files
    - [ ] Temporarily change the log level
- [ ] Troubleshooting
    - [ ] File locations
    - [ ] Check that lmstat is supported by blcollect
    - [ ] Do not delete lsb.tokens unless you defined a LSF License Scheduler elim

### Reference
- [ ] lsf.licensescheduler
    - [ ] bladmin
    - [ ] blcollect
    - [ ] blcstat
    - [ ] blhosts
    - [ ] blinfo
    - [ ] blkill
    - [ ] blparams
    - [ ] blstat
    - [ ] bltasks
    - [ ] blusers
    - [ ] fod.conf
    - [ ] fodadmin
    - [ ] fodapps
    - [ ] fodhosts
    - [ ] fodid
    - [ ] taskman


## LSF Data Manager
   
### About IBM Spectrum LSF Data Manager
- [ ] Concepts and terminology
- [ ] How LSF Data Manager works
    - [ ] Single cluster implementation
    - [ ] LSF multicluster capability implementation

### Plan and install IBM Spectrum LSF Data Manager
- [ ] Planning to install
- [ ] Install LSF Data Manager
    - [ ] Installing LSF
    - [ ] Installing LSF Data Manager
    - [ ] Configuring LSF data manager parameters
    - [ ] Verifying the installation

### Use LSF Data Manager
- [ ] Submitting and managing jobs with data requirements
    - [ ] Specifying data requirements for your job
    - [ ] Creating a data specification file
    - [ ] Staging data
        - [ ] Staging data in
        - [ ] Staging data out
    - [ ] Data tags for a data requirement work flow
        - [ ] Rules for specifying data tags
        - [ ] Creating and using data tags
        - [ ] Data tags example
        - [ ] Monitoring data tags
        - [ ] Cleaning up data tags
    - [ ] Modifying data jobs
    - [ ] Transferring data requirement files
        - [ ] Environment variables
    - [ ] Specifying a user group
    - [ ] Give other users access to your files
- [ ] Querying jobs with data requirements
    - [ ] Querying the data cache
        - [ ] Example data requirements job query
    - [ ] Querying data tags
    - [ ] Querying data jobs
    - [ ] Viewing historical information about data jobs

### Administering LSF Data Manager
- [ ] Managing dmd
    - [ ] Showing LSF data manager configuration
    - [ ] Reconfiguring LSF data manager
    - [ ] Shutting down LSF data manager
    - [ ] Configuring failover
- [ ] Managing the staging area (cache)
    - [ ] Configuring the data staging area
    - [ ] Staging area file structure
    - [ ] Remote file access
    - [ ] Enable users to control access to their files
- [ ] Managing data transfer
    - [ ] Data transfer jobs
        - [ ] Monitoring data transfer jobs
    - [ ] Transfer queue overview
        - [ ] Configuring the data transfer queue
        - [ ] Managing the data transfer queue
    - [ ] Manage data transfer nodes
    - [ ] Troubleshoot data transfer job failure
    - [ ] Script interface for data transfer jobs
    - [ ] Configuring IBM Aspera as a data transfer tool
    - [ ] Enabling data requirement file transfer with bsub -f
        - [ ] esub.datamanager script
        - [ ] lsrcp.wrapper.datamanager script
- [ ] Data specification files
    - [ ] Data specification file format
- [ ] Configuring LSF Data Manager to use the LSF multicluster capability
    - [ ] Setting up IBM Spectrum LSF multicluster capability job forwarding in LSF data manager
    - [ ] Showing LSF data manager connections
    - [ ] Cluster selection for remote jobs with data requirements
    - [ ] Intermediate data tags across multiple clusters
    - [ ] Querying information from remote LSF data managers
    - [ ] Optimized local stage in
    - [ ] Single data manager for multiple clusters

### Command reference
- [ ] bsub
    - [ ] Options
        - [ ] -data
        - [ ] -datagrp
        - [ ] -stage
- [ ] bdata
    - [ ] Synopsis
    - [ ] Subcommands
        - [ ] cache
        - [ ] chgrp
        - [ ] chmod
        - [ ] tags
        - [ ] showconf
        - [ ] connections
        - [ ] admin
    - [ ] Help and version display
    - [ ] See also
- [ ] bjobs
    - [ ] Options
        - [ ] -data
- [ ] bstage
    - [ ] bstage in
    - [ ] bstage out
    - [ ] Help and version display
    - [ ] See also

### Configuration reference
- [ ] lsb.queues
    - [ ] DATA_TRANSFER
- [ ] lsf.conf
    - [ ] LSB_TIME_DMD
    - [ ] LSF_DATA_HOSTS
    - [ ] LSF_DATA_PORT
    - [ ] LSF_DATA_SKIP_GROUP_CHECK
    - [ ] LSF_STAGE_IN_EXEC
    - [ ] LSB_STAGE_OUT_EXEC
    - [ ] LSB_STAGE_STORAGE
    - [ ] LSB_STAGE_TRANSFER_RATE
- [ ] lsf.datamanager
    - [ ] lsf.datamanager Parameters section
    - [ ] RemoteDataManagers section

## LSF resource connnector

### LSF resource connector overview

### Configuring resource providers
- [ ] Setting the initial configuration
- [ ] Configuring multiple resource providers
- [ ] Configuring different templates to create instances
- [ ] Assigning exclusive resources to a template
- [ ] Configuring IBM Spectrum Conductor with Spark for LSF resource connector
    - [ ] Managing resource sharing and distribution
    - [ ] Installing LSF on compute hosts
    - [ ] Configure resource connector for IBM Spectrum Conductor with Spark
    - [ ] Submitting jobs to EGO
        - [ ] How LSF returns hosts to EGO
- [ ] Configuring IBM Bluemix for LSF resource connector
    - [ ] Configuring LSF resource connector for IBM Bluemix
    - [ ] Submitting jobs to IBM Bluemix
- [ ] Configuring OpenStack for LSF resource connector
    - [ ] Configuring the DNS server for OpenStack
    - [ ] Configuring resource connector for OpenStack
    - [ ] Submitting jobs to OpenStack
        - [ ] How LSF returns hosts to OpenStack
- [ ] Configuring Microsoft Azure for LSF resource connector
    - [ ] Configuring LSF resource connector for Microsoft Azure
    - [ ] Update the LSF configuration for Microsoft Azure
    - [ ] Submitting jobs to Microsoft Azure
    - [ ] Adding multiple Azure providers
- [ ] Configuring Microsoft Azure CycleCloud for LSF resource connector
    - [ ] Configuring LSF resource connector for Microsoft Azure CycleCloud
    - [ ] Update the LSF configuration for Microsoft Azure CycleCloud
    - [ ] Submitting jobs to Microsoft Azure CycleCloud
- [ ] Configuring Google Cloud Platform for LSF resource connector
    - [ ] Configuring LSF resource connector for Google Cloud Platform
    - [ ] Submitting jobs to Google Cloud Platform
- [ ] Configuring Amazon Web Services for LSF resource connector
    - [ ] Preparing to configure AWS
    - [ ] Building a cloud image
        - [ ] Preparing Amazon Web Services components
        - [ ] Launching the Amazon Web Services EC2 instance
        - [ ] Installing an LSF server host on the AWS EC2 instance
    - [ ] Enabling LSF resource connector for Amazon Web Services (AWS)
        - [ ] The aws_enable.sh script
        - [ ] Choose account authentication method
        - [ ] Executing AWS enablement script for LSF
        - [ ] Completing the enabling of Resource Connector for AWS
            - [ ] Configuring user scripts to register AWS hosts
    - [ ] Configuring Bursting Behavior
        - [ ] Configuring a threshold
        - [ ] Providing specific policy configurations
        - [ ] Controlling reclaim behavior
    - [ ] Assigning exclusive resources to a template
    - [ ] Configuring AWS access with federated accounts
    - [ ] Configure AWS launch templates
    - [ ] Attach EFA network interfaces
    - [ ] Use AWS spot instances
        - [ ] Configuring AWS Spot instances
    - [ ] Submitting jobs to AWS
        - [ ] How LSF returns hosts to AWS
- [ ] Configuring OpenShift for LSF resource connector
    - [ ] Enabling LSF resource connector for OpenShift
    - [ ] Submitting jobs to OpenShift
- [ ] Configuring IBM Cloud Gen 2 for LSF resource connector
    - [ ] Preparing IBM Cloud Gen 2 for LSF resource connector
    - [ ] Configuring LSF resource connector for IBM Cloud Gen 2
    - [ ] Submitting jobs to IBM Cloud Gen 2

### Updating LSF configuration for resource connector
- [ ] Pre-provisioning and post-provisioning
- [ ] Define resource provisioning policies
- [ ] Use the LSF patch installer to update resource connector

### View information on the LSF resource connector
- [ ] Checking the LSF resource connector status
- [ ] Use badmin to view LSF resource connector information
- [ ] Logging and troubleshooting

### Configuration reference
- [ ] lsb.applications
    - [ ] RC_ACCOUNT
    - [ ] RC_RECLAIM_ACTION
- [ ] lsb.queues
    - [ ] RC_ACCOUNT
    - [ ] RC_DEMAND_POLICY
    - [ ] RC_HOSTS
- [ ] lsf.conf
    - [ ] LSB_RC_DEFAULT_HOST_TYPE
    - [ ] LSB_RC_EXTERNAL_HOST_FLAG
    - [ ] LSB_RC_EXTERNAL_HOST_IDLE_TIME
    - [ ] LSB_RC_EXTERNAL_HOST_MAX_TTL
    - [ ] LSB_RC_MQTT_ERROR_LIMIT
    - [ ] LSF_MQ_BROKER_HOSTS
    - [ ] LSB_RC_QUERY_INTERVAL
    - [ ] LSB_RC_REQUEUE_BUFFER
    - [ ] LSB_RC_TEMPLATE_REQUEST_DELAY
    - [ ] LSB_RC_UPDATE_INTERVAL
    - [ ] MQTT_BROKER_HOST
    - [ ] MQTT_BROKER_PORT
    - [ ] EBROKERD_HOST_CLEAN_DELAY
- [ ] egoprov_config.json
- [ ] egoprov_ego.conf
- [ ] egoprov_templates.json
- [ ] hostProviders.json
- [ ] osprov_config.json
- [ ] osprov_templates.json
- [ ] policy_config.json
- [ ] awsprov_config.json
- [ ] awsprov_templates.json
- [ ] azureprov_config.json
- [ ] azureprov_templates.json
- [ ] cyclecloudprov_config.json
- [ ] cyclecloudprov_templates.json
- [ ] softlayerprov_config.json
- [ ] softlayer_templates.json
- [ ] googleprov_config.json
- [ ] googleprov_templates.json
- [ ] openshiftprov_config.json
- [ ] openshiftprov_templates.json
- [ ] ibmcloudgen2_config.json
- [ ] ibmcloudgen2_templates.json


## LSF Connector for Kubernetes

### Overview
### Limitations
### Installing
### Configuring
### Verifying
### Deploying jobs
### Submitting jobs
- [ ] Example: Submit a sleep job