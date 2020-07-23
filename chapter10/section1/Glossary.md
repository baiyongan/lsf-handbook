# Glossary

## blcollect

The License Scheduler daemon that queries the licensing software for license usage. **blcollect** collects information from the license manager.

You can spread the load of license collection by running the license information collection daemon on multiple UNIX hosts.

Also called the collector.

## bld

The License Scheduler batch daemon.

## cluster mode

License tokens are allocated to clusters by License Scheduler, and job scheduling within each cluster is managed by the local **mbatchd**. Cluster mode is only available for License Scheduler version 8.0 and later.

Each license feature can use either cluster mode or project mode, but not both.

## lmgrd

The main FlexNet licensing daemon. Usually grouped into service domains inside License Scheduler.

## project mode

License tokens are allocated to projects by License Scheduler, and job scheduling for license projects takes place across clusters that follow the license distribution policy that is configured for each project. Corresponds to License Scheduler version 7.0.5 and earlier.

Each license feature can use either cluster mode or project mode, but not both.

## service domain

A group of one or more FlexNet license servers.

You configure the service domain with the license server names and port numbers that serve licenses to a network.

## taskman job

A job that is run by theIBM Spectrum LSF (LSF) Task Manager (**taskman**) tool outside of LSF, but is scheduled by License Scheduler.

## token

One license token represents one actual license, and is used by License Scheduler to track license use and determine which job to dispatch next.

License Scheduler manages license tokens instead of controlling the licenses directly. After they reserve license tokens, jobs are dispatched, then the application that needs the license is started. The number of tokens available from LSF corresponds to the number of licenses available from the license server, so if a token is not available, the job is not dispatched.

**Parent topic:**

[Introduction](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/license_scheduler/chap_introduction.html?view=kc)