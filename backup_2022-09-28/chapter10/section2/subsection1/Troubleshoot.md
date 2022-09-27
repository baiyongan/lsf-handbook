# Troubleshoot

## Procedure

1. If you receive the following message, configure your Windows host name and IP address in the /etc/hosts file on the master host:

   Failed in an LSF library call: Failed in sending/receiving a message: error 0: The operation completed successfully.

2. To enable the **blhosts** command, make sure that your Windows host can resolve the master host IP address correctly.