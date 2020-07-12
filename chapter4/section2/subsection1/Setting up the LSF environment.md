# Setting up the LSF environment

Before you use LSF, you must set up the LSF execution environment with the cshrc.lsf or profile.lsf file.

## Procedure

After you log in to an LSF host, use one of the following shell environment files to set your LSF environment.

- In the csh or tcsh shell, run the

  source command:

  ```
% source <LSF_TOP>/conf/cshrc.lsf
  ```

- In the sh , ksh, or bash shell run the following command:

  ```
$ . <LSF_TOP>/conf/profile.lsf
  ```

The files cshrc.lsf and profile.lsf are created during installation by the **lsfinstall** command to set up the LSF operating environment.