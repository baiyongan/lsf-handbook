# Before you install

## About this task

LSF must be installed and running before you install License Scheduler.

## Procedure

Log on to any LSF host as root and use **lsid** to make sure that the cluster is running. If you see the message "Cannot open lsf.conf file", verify that the $LSF_ENVDIR environment variable is set correctly.

To set your LSF environment:

- For **csh** or **tcsh**:

  % source LSF_TOP/conf/cshrc.lsf

- For **sh**, **ksh**, or **bash**:

  $ . LSF_TOP/conf/profile.lsf