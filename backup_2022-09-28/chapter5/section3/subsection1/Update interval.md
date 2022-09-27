# 更新间隔

The job-level resource usage information is updated at a maximum frequency of every SBD_SLEEP_TIME second.

The update is done only if the value for the CPU time, resident memory usage, or virtual memory usage has changed by more than 10 percent from the previous update or if a new process or process group has been created.