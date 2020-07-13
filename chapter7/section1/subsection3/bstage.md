# bstage

Stages data files for jobs with data requirements by copying files or creating symbolic links for them between the local staging cache and the job execution environment. You must run **bstage** only within the context of an LSF job (like **blaunch**). To access a file with the **bstage** command, you must have permission to read it.

**[bstage in](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_command_ref/bstage.1in.1.html?view=kc)**
Stages in data files for jobs with data requirements. **bstage** copies or symbolically links files *from* the data manager staging area *to* the job execution host.

**[bstage out](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_command_ref/bstage.2out.1.html?view=kc)**
Stages out data files for jobs with data requirements. The **bstage** command copies or creates symbolic links to files *from* the job current working directory *to* the data management cache, then requests a transfer job to copy the file or folder to a host.

**[Help and version options](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_command_ref/bstage.3other.1.html?view=kc)**
IBM Spectrum LSF Data Manager help and version display options

**[See also](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_command_ref/bstage.4seealso.1.html?view=kc)**
**bdata**, **bhist**, **bjobs**, **bmod**, **bsub**, lsf.conf, lsf.datamanager