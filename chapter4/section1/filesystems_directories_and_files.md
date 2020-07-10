# 文件系统、目录和文件

LSF is designed for networks where all hosts have shared file systems, and files have the same names on all hosts.

LSF includes support for copying user data to the execution host before a batch job runs, and for copying results back after the job runs.

In networks where the file systems are not shared, this support can be used to give remote jobs access to local data.

## Supported file systems

- ##### UNIX

  On UNIX systems, LSF supports the following shared file systems:

  - ###### Network File System (NFS)

    NFS file systems can be mounted permanently or on demand by using the **automount** command.

  - ###### Andrew File System (AFS)

    Supported on an on-demand basis under the parameters of the 9.1.2 integration with some published configuration parameters. Supports sequential and parallel user jobs that access AFS, **JOB_SPOOL_DIR** on AFS, and job output and error files on AFS.

  - ###### Distributed File System (DCE/DFS)

    Supported on an on-demand basis.

- ##### Windows

  On Windows, directories that contain LSF files can be shared among hosts from a Windows server machine.

## Non-shared directories and files

LSF is used in networks with shared file space. When shared file space is not available, LSF can copy needed files to the execution host before the job runs, and copy result files back to the submission host after the job completes.

Some networks do not share files between hosts. LSF can still be used on these networks, with reduced fault tolerance.

**[Example directory structures](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_admin/dir_structure_lsf.html?view=kc)**
The following figures show typical directory structures for a new installation on UNIX and Linux or on Microsoft Windows. Depending on which products you installed and platforms you selected, your directory structure might be different.





The following figures show typical directory structures for a new installation on UNIX and Linux or on Microsoft Windows. Depending on which products you installed and platforms you selected, your directory structure might be different.

**[UNIX and Linux](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_admin/dir_structure_unix.html?view=kc)**
The following figure shows a typical directory structure for a new UNIX or Linux installation with the **lsfinstall** command.**[Microsoft Windows directory structure](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_admin/windows_dir_structure.html?view=kc)**
The following figure shows a typical directory structure for a new Windows installation.



The following figure shows a typical directory structure for a new UNIX or Linux installation with the **lsfinstall** command.

![Example LSF directory structure on UNIX and Linux](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_admin/lsf_unix_dirmap.jpg)





The following figure shows a typical directory structure for a new Windows installation.

![Example LSF directory structure on Windows](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_admin/lsf_windows_dirmap.jpg)