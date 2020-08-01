# User authentication

When a user claims a job belongs to a project, LSF License Scheduler checks if this user belongs to this project, since projects assign fairshare priority and preemption is based on ownership. When users submit jobs to license projects they do not belong to, the request is refused or the job gets put in a "default" bucket with a low number of shares or no shares at all.

Administrators can control who can run what project. By default, such authentication is not enabled for compatibility with the previous versions of LSF License Scheduler. When enabled, user authentication has the following behavior:

- If the user belongs to the project, LSF License Scheduler allows the license request.
- If the user does not belong to the project or the project does not match any projects in the configuration, LSF License Scheduler rejects the request.
- If a default project is configured in the LSF License Scheduler user authentication configuration file ls.users, LSF License Scheduler changes the project to default and allows the license request.
- If the project is default, no authentication is needed and LSF License Scheduler allows the request.

**Parent topic:**

[Configuring License Scheduler](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/license_scheduler/chap_config_ls.html?view=kc)

## Enable user authentication

### Procedure

1. To enable user authentication for LSF jobs, configure LSF to use authentication esub (**esub.ls_auth**).

   Define LSB_ESUB_METHOD=lsauth in lsf.conf.

2. To enable user authentication for **taskman** jobs, define AUTH=Y in lsf.licensescheduler.

3. Configure users and their associated projects in the LSF_CONFDIR/ls.users file.

   The file defines one project per line using the following format:

   ```
   project_name:::[user_name][,user_name2 ...]
   ```

   For example,

   ```
   Project1:::user1,user2
   default:::
   ```

   **Note**Ensure that projects in ls.users, including the default project, conform to the lsf.licensescheduler configuration.