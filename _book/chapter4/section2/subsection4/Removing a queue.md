# Removing a queue

Edit lsb.queues to remove a queue definition.

## Before you begin

**Important**

Before you remove a queue, make sure that no jobs are running in the queue.

Use the **bqueues** command to view a list of existing queues and the jobs that are running in those queues. If jobs are in the queue that you want to remove, you must switch pending and running jobs to another queue, then remove the queue. If you remove a queue that has pending jobs in it, the jobs are temporarily moved to a lost_and_found queue. The job state does not change. Running jobs continue, and jobs that are pending in the original queue are pending in the lost_and_found queue. Jobs remain pending until the user or the queue administrator uses the **bswitch** command to switch the jobs into a regular queue. Jobs in other queues are not affected.

## Procedure

1. Log in as the primary administrator on any host in the cluster.

2. Close the queue to prevent any new jobs from being submitted.

   ```
   badmin qclose night
   Queue night is closed
   ```

3. Switch all pending and running jobs into another queue.

   For example, the **bswitch -q night idle 0** command chooses jobs from the night queue to the idle queue. The job ID number 0 switches all jobs.

   ```
   bjobs -u all -q night
   JOBID USER  STAT  QUEUE FROM_HOST   EXEC_HOST   JOB_NAME   SUBMIT_TIME 
   5308  user5  RUN   night    hostA     hostD         job5  Nov 21 18:16 
   5310  user5 PEND   night    hostA     hostC        job10  Nov 21 18:17
    
   bswitch -q night idle 0
   Job <5308> is switched to queue <idle> 
   Job <5310> is switched to queue <idle>
   ```

4. Edit the LSB_CONFDIR/cluster_name/configdir/lsb.queues file and remove or comment out the definition for the queue that you want to remove.

5. Save the changes to the lsb.queues file.

6. Run the **badmin reconfig** command to reconfigure the cluster.

   ```
   % badmin reconfig
   Checking configuration files ...
   No errors found.
   Do you want to reconfigure? [y/n] y
   Reconfiguration initiated
   ```

   The **badmin reconfig** command checks for configuration errors. If no unrecoverable errors are found, you are asked to confirm reconfiguration. If unrecoverable errors are found, reconfiguration exits.

## Results

If you get errors, see [Troubleshooting LSF problems](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_admin/chap_troubleshooting_lsf.html?view=kc#v3523448) for help with some common configuration errors.

- For more information about the [lsb.queues](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_config_ref/lsb.queues.5.html?view=kc) file, see the [Configuration Reference](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_welcome/lsf_kc_config_ref.html?view=kc).
- For more information about the [**badmin reconfig**](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_command_ref/badmin.8.html?view=kc) command, see the [Command Reference](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_welcome/lsf_kc_cmd_ref.html?view=kc).