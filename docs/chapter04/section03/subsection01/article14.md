# 查看作业提交环境

Use the **bjobs -env** command option to view a job's environment variables or the **bjobs -script** command option to view the job script file.

## About this task

You cannot specify the     options with the-envor-scriptoptions.

## Procedure

- To view the environment variables for a specified job, run the **bjobs -env** command option.

  ```
  bjobs -env job_id
  ```

  You must specify a single job ID or job array element when using the -env command option. Multiple job IDs are not supported.

- To view the specified job's job script file, run the **bjobs -script** command option.

  ```
  bjobs -script job_id
  ```

  You must specify a single job ID or job array element when using the -script command option. Job arrays and multiple job IDs are not supported.