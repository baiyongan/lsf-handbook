# Configure multiple administrators

## Before you begin

The primary License Scheduler admin account must have write permissions in the LSF working directory of the primary LSF admin account.

## About this task

The administrator account uses a list of users that you specified when you installed License Scheduler. Edit this parameter if you want to add or change administrators. The first user name in the list is the primary License Scheduler administrator. By default, all the working files and directories that are created by License Scheduler are owned by the primary License Scheduler account.

## Procedure

1. Log on as the primary License Scheduler administrator.

2. In lsf.licensescheduler, edit the ADMIN parameter if you want to change the License Scheduler administrator. You can specify multiple administrators that are separated by spaces.

   For example:

   `ADMIN = lsfadmin user1 user2 root`

3. Run **bld -C** to test for configuration errors.

4. Run **bladmin reconfig all** to apply your changes.