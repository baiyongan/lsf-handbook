# I LSF Data Manager


!!! abstract 
    概述
    

## About IBM Spectrum LSF Data Manager
- [ ] Concepts and terminology
- [ ] How LSF Data Manager works
    - [ ] Single cluster implementation
    - [ ] LSF multicluster capability implementation

## Plan and install IBM Spectrum LSF Data Manager
- [ ] Planning to install
- [ ] Install LSF Data Manager
    - [ ] Installing LSF
    - [ ] Installing LSF Data Manager
    - [ ] Configuring LSF data manager parameters
    - [ ] Verifying the installation

## Use LSF Data Manager
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

## Administering LSF Data Manager
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

## Command reference
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

## Configuration reference
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
