# Adding a queue

Edit the lsb.queues file to add the new queue definition. Adding a queue does not affect pending or running jobs.

## Procedure

1. Log in as the administrator on any host in the cluster.

2. Edit the LSB_CONFDIR/cluster_name/configdir/lsb.queues file to add the new queue definition.

   You can copy another queue definition from this file as a starting point. Remember to change the **QUEUE_NAME** parameter of the copied queue.

3. Save the changes to the lsb.queues file.

4. When the configuration files are ready, run the **badmin ckconfig** command to check the new queue definition.

   If any errors are reported, fix the problem and check the configuration again.

5. Run the **badmin reconfig** command to reconfigure the cluster.

   ```
   % badmin reconfig
   Checking configuration files ...
   No errors found.
   Do you want to reconfigure? [y/n] y
   Reconfiguration initiated
   ```

   The **badmin reconfig** command also checks for configuration errors. If no unrecoverable errors are found, you are asked to confirm reconfiguration. If unrecoverable errors are found, reconfiguration exits.

## Results

If you get errors, see [Troubleshooting LSF problems](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_admin/chap_troubleshooting_lsf.html?view=kc#v3523448) for help with some common configuration errors.

- For more information about the [lsb.queues](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_config_ref/lsb.queues.5.html?view=kc) file, see the [Configuration Reference](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_welcome/lsf_kc_config_ref.html?view=kc).
- For more information about the [**badmin reconfig**](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_command_ref/badmin.8.html?view=kc) command, see the [Command Reference](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_welcome/lsf_kc_cmd_ref.html?view=kc).

## Example

```
Begin Queue 
QUEUE_NAME = normal 
PRIORITY = 30 
STACKLIMIT= 2048 
DESCRIPTION = For normal low priority jobs, running only if hosts are lightly loaded. 
QJOB_LIMIT = 60     # job limit of the queue 
PJOB_LIMIT = 2     # job limit per processor 
ut = 0.2 
io = 50/240 
USERS = all 
HOSTS = all  
NICE = 20 
End Queue
```