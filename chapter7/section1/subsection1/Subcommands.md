# Subcommands

LSF data management subcommands and options

File-based cache query:

**bdata cache** [**-w** | **-l**] [**-u all** | **-u** *user_name*] [**-g all** | **-g** *user_group_name*] [**-dmd** *cluster_name*] [*host_name***:**]*abs_file_path*

Job-based cache query:

**bdata cache** [**-dmd** *cluster_name*] [**-w** | **-l**] *job_ID*[**@***cluster_name*]

Job-based cache query:

**bdata cache** [**-dmd** *cluster_name*] [**-w** | **-l**] *job_ID*[**@***cluster_name*]

Change group after stage out:

**bdata chgrp** [**-dmd** *cluster_name*] **-g** *user_group_name* [*host_name***:**]*abs_file_path*

Change group after stage in:

**bdata chgrp** [**-dmd** *cluster_name*] **-g** *user_group_name* **-tag** *tag_name*

Change the file permission mode of a file:

**bdata chmod** [**-dmd** *cluster_name*] **-mode** *octal_mode* **-mode** [*host_name***:**]*abs_file_path*

Tag query:

**bdata tags list** [**-w**] [**-u all** | **-u** *user_name*] [**-dmd** *cluster_name*]

Tag cleanup:

**bdata tags clean** [**-u** *user_name*] [**-dmd** *cluster_name*] *tag_name*

Effective configuration query:

**bdata showconf**

Connections query:

**bdata connections** [**-w**]

Administration - reconfigure and shut down LSF data manager:

**bdata admin reconfig**

**bdata admin shutdown** [*host_name*]

## Common options

- -w

  Wide format. Displays the information in a wide format. Use this option only with the **cache**, **connections**, and **tags list** subcommands.

- -l

  Long format. Displays additional information about LSF data management files. Use this option only with the **cache** subcommand.

- -dmd cluster_name

  Query the LSF data manager corresponding to the specified remote cluster. Use this option only with the **cache**, and **tags** subcommands.

- -u all | -u user_name

  Query files in the cache for the specified user. Use -u all or -u user_name with file-based **bdata cache** and **bdata tags list**. You can use only -u user_name with **bdata tags clean**.

**[cache](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_command_ref/bdata.3cache.1.html?view=kc)**
Queries the LSF data management cache.

**[chgrp](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_command_ref/bdata.3achgrp.1.html?view=kc)**
Changes the user group of a file in the LSF data management cache.

**[chmod](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_command_ref/bdata.3bchmod.1.html?view=kc)**
Changes the file permission mode of a file that is staged in to the LSF data management cache.

**[tags](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_command_ref/bdata.4tags.1.html?view=kc)**
LSF data management tag query and cleanup options

**[showconf](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_command_ref/bdata.5showconf.1.html?view=kc)**
LSF data management effective configuration query option

**[connections](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_command_ref/bdata.6connections.1.html?view=kc)**
Query LSF data management connections. Lists currently connected **mbatchd** daemons, with master LSF data manager host names, their status, and the outgoing and incoming connections for remote LSF data managers.

**[admin](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_command_ref/bdata.7admin.1.html?view=kc)**
Reconfigure and shut down the LSF data manager daemon (**dmd**).