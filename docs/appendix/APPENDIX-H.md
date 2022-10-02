# H LSF License Scheduler


!!! abstract 
    概述
    
## Introduction
- [ ] Overview
- [ ] Differences between LSF License Scheduler editions
- [ ] Glossary
- [ ] Architecture

## Installing and starting License Scheduler
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

## LSF License Scheduler concepts
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

## Configuring License Scheduler
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

## Viewing information and troubleshooting
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

## Reference
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
