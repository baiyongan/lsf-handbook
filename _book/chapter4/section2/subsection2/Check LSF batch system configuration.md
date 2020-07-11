# Check LSF batch system configuration

The **badmin** command controls and monitors the operation of the LSF batch workload system.

Use the **badmin ckconfig** command to check the LSF batch system configuration files. The -v option displays detailed information about the configuration:

The messages in the following output are typical of **badmin ckconfig -v**. Other messages might indicate problems with your LSF batch workload system configuration.

```
% badmin ckconfig -v
Checking configuration files ...
Dec 20 12:22:55 2015 20246 9 9.1.3 minit: Trying to call LIM to get cluster name 
...
Dec 20 12:22:55 2015 20246 9 9.1.3 Batch is enabled
Dec 20 12:22:55 2015 4433 9 9.1.3 Checking Done
---------------------------------------------------------
No errors found.
```

See [Troubleshooting LSF problems](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_admin/chap_troubleshooting_lsf.html?view=kc#v3523448) or the [LSF Command Reference](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_welcome/lsf_kc_cmd_ref.html?view=kc) for help with some common configuration errors.