# About submitting jobs

When you submit an LSF job, you must reserve the license with the resource requirement usage section (**bsub -R "rusage..."** option).

You cannot successfully reserve a license by running **bsub -R "select"**.

- Specify the license token name (same as specifying a shared resource).

- If you use project mode, specify a license project name with the

   bsub -Lp option.

  If you also have LSF_LIC_SCHED_STRICT_PROJECT_NAME=y in lsf.conf and without configuring a default project for the required feature, the job is rejected.

  ##### **Tip**

  Use the **blstat** command to view information about the default license project.

- Update resource requirements.

  If your queue or job starter scripts request a license that is managed by an LSF ELIM, you must update the job submission scripts to request that license that uses the license token name.

Examples:

bsub -R "rusage[AppB=1]" -Lp Lp1 myjob

This command submits a job named myjob to license project Lp1 and requests one AppB license

bsub -R "rusage[AppC=1]" myjob

This command submits a job named myjob and requests one AppC license.