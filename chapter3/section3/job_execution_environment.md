# 作业运行环境

When LSF runs your jobs, it copies the environment from the submission host to the execution host.

The execution environment includes the following information:

- Environment variables that are needed by the job
- Working directory where the job begins running
- Other system-dependent environment settings, such as resource usage limits

## Shared user directories

To provide transparent remote execution, LSF commands determine the user’s current working directory and use that directory on the remote host.

## Executable files and the PATH environment variable

Search paths for executable files (the PATH environment variable) are passed to the remote execution host unchanged.

**Note** 

In mixed clusters, LSF works best when the user binary directories have the same path names on different host types. Using the same paths names makes the PATH variable valid on all hosts.

For easy administration, LSF configuration files are stored in a shared directory.