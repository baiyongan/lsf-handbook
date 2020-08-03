# 故障排查

## 技巧

- Run **blstat** to check the current license usage information.
- Run **blusers** to check the current job and license usage. This information is the set intersection of License Scheduler Jobs and FlexNet information.
- Run **blinfo** command to check the current License Scheduler configuration.
- Run **bld -c** to check that the configuration is correct. This action, with **LOG_DEBUG**, writes detailed configuration settings to the debug log.
- Turn on debugging by setting **LSF_LOG_MASK=LOG_DEBUG** and reconfiguring the daemon with **bladmin reconfig all**.
- Set the log class for **mbatchd** debug (**LSB_DEBUG_MBD**) in lsf.conf: **LC_LICSCHED**.
- Use **LSB_TIME_SCH=timelevel** (similar to **LSB_TIME_MBD**) in lsf.conf to enable the logging of timing information.
- Run **bhosts -s** to check that the resources are being reported correctly to LSF.



- **[File locations](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/license_scheduler/troubleshooting_files.html?view=kc)**
  The following files are useful for troubleshooting purposes.
- **[Check that lmstat is supported by blcollect](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/license_scheduler/troubleshooting_lmstat_blcollect.html?view=kc)**
  Some problems are due to the license manager not being supported by the LSF License Scheduler collector.
- **[Do not delete lsb.tokens unless you defined a LSF License Scheduler elim](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/license_scheduler/troubleshooting_lsb_tokens.html?view=kc)**
  The lsb.tokens file contains allocation and usage information on features that are allocated to the cluster. Do not remove or modify this file unless you defined an **elim** for LSF License Scheduler to ensure that LSF can still schedule LSF License Scheduler jobs even if the connection between **mbatchd** and **bld** is broken.