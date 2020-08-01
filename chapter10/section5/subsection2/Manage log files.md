# Manage log files

## About this task

License Scheduler logs error messages at different levels so that you can choose to log all messages or only log messages that are deemed critical.

## Procedure

1. Set **LS_LOG_MASK** in lsf.licensescheduler to the wanted logging level.

   **Note**

   If LS_LOG_MASK is not defined, the value of LSF_LOG_MASK in lsf.conf is used. If LS_LOG_MASK or LSF_LOG_MASK are not defined, the default is LOG_WARNING.

   Log levels (highest to lowest):

   - LOG_WARNING: Default. Essential error messages only.
   - LOG_DEBUG: Fewest number of debug messages, useful for debugging a problem.
   - LOG_DEBUG1: More debug messages than LOG_DEBUG.
   - LOG_DEBUG2: Most frequently used debug level.
   - LOG_DEBUG3: All debug messages. Use sparingly.

   Messages that are logged at the specified level and higher are recorded, while lower-level messages are discarded.

2. Clean up or back up log files periodically.