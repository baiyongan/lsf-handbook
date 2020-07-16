# Submit batch jobs

The **bsub** command submits jobs to LSF batch scheduling queues.

The following command submits a **sleep** job to the default queue (normal):

```
% bsub sleep 60
Job <3616> is submitted to default queue <normal>.
```

When a job is submitted to LSF, it is assigned a unique job ID, in this case 3616.

You can specify a wide range of job options on the **bsub** command. For example, you can specify a queue, and the job command **sleep 60** is the last option:

```
% bsub -q short sleep 60
Job <3628> is submitted to queue <short>.
```

## What LSF does with job output

By default, when the job is finished, LSF sends email with a job report and any output and error messages to the user account from which the job was submitted. You can optionally save standard output and standard error to files with the -o and -e options.

The following command appends the standard output and standard error of the job to the files output.3640 and errors.3640 in the jobs subdirectory of the home directory of user1.

```
% bsub -q short -o /home/user1/job/output.%J -e /home/user1/job/errors.%J ls -l
Job <3640> is submitted to queue <short>.
```

The %J variable is replaced by the job ID when the files are created. Using %J helps you find job output when you run a lot of jobs.

## Interactive batch jobs with bsub -I

To submit an interactive job through LSF, use the -I option:

The following command submits a batch interactive job that displays the output of the **ls** command:

```
% bsub -I ls
```

To submit a batch interactive job by using a pseudo-terminal, use the bsub -Ip option.

To submit a batch interactive job and create a pseudo-terminal with shell mode support, use the bsub -Is option.