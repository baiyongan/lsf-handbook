# 查看作业的时间顺序历史

## About this task

By default, the **bhist** command displays information from the job event history file, lsb.events, on a per job basis.

## Procedure

- Use the **-t** option of **bhist** to display the events chronologically instead of grouping all events for each job.
- Use the **-T** option to select only those events within a given time range.

## Example

For example, the following displays all events that occurred between 14:00 and 14:30 on a given day:

```shell
bhist -t -T 14:00,14:30
Wed Oct 22 14:01:25 2009: Job <1574> done successfully;
Wed Oct 22 14:03:09 2009: Job <1575> submitted from host to Queue , CWD , User , Project , Command , 
Requested Resources ;
Wed Oct 22 14:03:18 2009: Job <1575> dispatched to ;
Wed Oct 22 14:03:18 2009: Job <1575> starting (Pid 210);
Wed Oct 22 14:03:18 2009: Job <1575> running with execution home , Execution CWD , Execution Pid <210>;
Wed Oct 22 14:05:06 2009: Job <1577> submitted from host  to Queue, CWD , User , Project , Command , 
Requested Resources ;
Wed Oct 22 14:05:11 2009: Job <1577> dispatched to ;
Wed Oct 22 14:05:11 2009: Job <1577> starting (Pid 429);
Wed Oct 22 14:05:12 2009: Job <1577> running with execution home, Execution CWD , Execution Pid <429>;
Wed Oct 22 14:08:26 2009: Job <1578> submitted from host to Queue, CWD , User , Project , Command;
Wed Oct 22 14:10:55 2009: Job <1577> done successfully;
Wed Oct 22 14:16:55 2009: Job <1578> exited;
Wed Oct 22 14:17:04 2009: Job <1575> done successfully;
```