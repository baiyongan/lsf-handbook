# Temporarily change the log level

## Before you begin

You must submit the commands from the host on which the daemon is running (only applicable to the **bld**).

## About this task

You can temporarily change the class or message log level for the **bld** and **blcollect** daemons without changing lsf.licensescheduler.

The message log level that you set is in effect from the time you set it until you turn it off or the daemon stops running, whichever is sooner. If the daemon is restarted, its message log level is reset back to the value of **LS_LOG_MASK** and the log file is stored in the directory that is specified by **LSF_LOGDIR**.

## Procedure

1. Set the log level for the **bld**.

   bladmin blddebug [-l debug_level] [-c class_name]

   For example:

   ```
   bladmin blddebug -l 1 -c "LC_TRACE LC_FLEX"
   ```

   Logs messages for **bld** running on the local host and sets the log message level to LOG_DEBUG1. The log class is LC_TRACE LC_FLEX.

2. Set the log level for **blcollect**.

   bladmin blcdebug [-l debug_level] collector_name ... | all

   For example:

   bladmin blcdebug -l 3 all

   The log mask of all collectors is changed to LOG_DEBUG3.

3. Return the debug settings to their configured values (set with **LS_LOG_MASK** in lsf.licensescheduler).

   bladmin blddebug -o

   bladmin blcdebug -o

## Example

For a detailed description of these commands and their options, see the IBM Spectrum LSF Command Reference.