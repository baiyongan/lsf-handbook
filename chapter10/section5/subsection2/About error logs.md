# About error logs

Error logs maintain important information about License Scheduler operations.

**Tip**Log files grow over time. Occasionally clear or back up these files (manually or using automatic scripts).

Log files are reopened each time that a message is logged, so if you rename or remove a daemon log file, the daemons automatically create a new log file.

The location of log files is specified with the parameter **LSF_LOGDIR** in lsf.conf.

The error log file names for the LSF License Scheduler system daemons are:

- bld.log.host_name
- blcollect.log.host_name

## About blcollect log messages

Messages that are logged by **blcollect** include the following information:

- Time: The message log time.
- **blcollect** name: The service domain name, which is the license server host name, accessed by blcollect as defined in lsf.licensescheduler.
- Status report for feature collection: **blcollect** information that gathered successfully or not.
- Detailed information: The number of tokens, the name of tokens, the license server name for license tokens that are collected by **blcollect**.

**[Manage log files](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/license_scheduler/log_files_manage.html?view=kc)**
**[Temporarily change the log level](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/license_scheduler/log_level_change_temporarily.html?view=kc)**