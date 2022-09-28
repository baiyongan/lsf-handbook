# 查看作业输出

## Before you begin

You must be logged on as the job owner.

## About this task

The output from a job is normally not available until the job is finished. However, LSF provides the **bpeek** command for you to look at the output the job has produced so far.

By default, **bpeek** shows the output from the most recently submitted job. You can also select the job by queue or execution host, or specify the job ID or job name on the command line.

To save time, you can use this command to check whether your job is behaving as you expected and kill the job if it is running away or producing unusable results.



## Procedure

Run **bpeek** job_id.

## Example

For example:

```shell
bpeek 1234
<< output from stdout >>
Starting phase 1
Phase 1 done
Calculating new parameters
...
```