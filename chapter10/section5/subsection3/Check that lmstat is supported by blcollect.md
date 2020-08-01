# Check that lmstat is supported by blcollect

Some problems are due to the license manager not being supported by the LSF License Scheduler collector.

## Procedure

1. Create shell script to output (for example, echo) target **lmstat** output.
2. Point **LMSTAT_PATH** in lsf.licensescheduler to the shell script.
3. If **LIC_COLLECTOR** is not set, restart the **bld** to restart **blcollect**. If **LIC_COLLECTOR** is set, kill **blcollect** and restart **blcollect** manually.
4. Observe the **blcollect** log to view if there are any errors to determine whether **blcollect** is able to parse **lmstat** output properly.