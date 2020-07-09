# Making your cluster available to users

Make sure that all LSF users include either the cshrc.lsf or profile.lsf file at the end of their own .cshrc or .profile file, or run one of these two files before you use LSF.

## About this task

To set up the LSF environment for your users, use the following two shell files:

- LSF_CONFDIR/cshrc.lsf

  Use this file for **csh** or **tcsh** shell.

- LSF_CONFDIR/profile.lsf

  Use this file for **sh**, **ksh**, or **bash** shell.

## Procedure

For **csh** or **tcsh** shell:

- Add the cshrc.lsf file to the end of the .cshrc file for all users:

  - Copy the contents of the cshrc.lsf file into the .cshrc file.

  - Add a line with the

     

    source

     

    command to the end of the

     

    .cshrc

     

    file:

    For example, if your the LSF_TOP directory for your cluster is /usr/share/lsf/conf, add the following line to the .cshrc file:

    ```
    source /usr/share/lsf/conf/cshrc.lsf
    ```

For **sh**, **ksh**, or **bash** shell:

- Add the profile.lsf file to the end of the .profile file for all users:

  - Copy the contents of the profile.lsf file into the .profile file.

  - For example, if your the

     

    LSF_TOP

     

    directory for your cluster is

     

    /usr/share/lsf/conf

    , add a line similar to the following to the end of the

     

    .profile

     

    file:

    ```
    . /usr/share/lsf/conf/profile.lsf
    ```