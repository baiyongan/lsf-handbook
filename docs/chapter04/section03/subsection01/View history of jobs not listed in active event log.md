# 查看未在活动事件日志中列出的作业历史

## About this task

LSF periodically backs up and prunes the job history log. By default, **bhist** only displays job history from the current event log file. You can display the history for jobs that completed some time ago and are no longer listed in the active event log.

The -n num_logfiles option tells the **bhist** command to search through the specified number of log files instead of only searching the current log file.

Log files are searched in reverse time order. For example, the command bhist -n 3 searches the current event log file and then the two most recent backup files.

## Procedure

Run **bhist -n** num_logfiles.

## Example

------

| `bhist -n 1 ![复制代码](https://www.ibm.com/support/knowledgecenter/images/icons/copy.png)` | Searches the current event log file lsb.events  |
| ------------------------------------------------------------ | ----------------------------------------------- |
| `bhist -n 2 ![复制代码](https://www.ibm.com/support/knowledgecenter/images/icons/copy.png)` | Searches lsb.events and lsb.events.1            |
| `bhist -n 3 ![复制代码](https://www.ibm.com/support/knowledgecenter/images/icons/copy.png)` | Searches lsb.events, lsb.events.1, lsb.events.2 |
| `bhist -n 0 ![复制代码](https://www.ibm.com/support/knowledgecenter/images/icons/copy.png)` | Searches all event log files in LSB_SHAREDIR    |