# 安全

Understand the LSF security model, authentication, and user roles.

## LSF security model

![LSF security modell](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_foundations/authentication_authorization_lsf.jpg)

By default, the LSF security model tracks user accounts internally. A user account that is defined in LSF includes a password to provide authentication and an assigned role to provide authorization, such as administrator.

## LSF user roles

LSF, without EGO enabled, supports the following user roles:

- LSF user

  Has permission to submit jobs to the LSF cluster and view the states of jobs and the cluster.

- Primary LSF administrator

  Has permission to perform clusterwide operations, change configuration files, reconfigure the cluster, and control jobs submitted by all users.Configuration files such as lsb.params and lsb.hosts configure all aspects of LSF.

- LSF administrator

  Has permission to perform operations that affect other LSF users.Cluster administratorCan perform administrative operations on all jobs and queues in the cluster. Might not have permission to change LSF configuration files.Queue administratorAdministrative permissions are limited to a specified queue.Host group administratorAdministrative permissions are limited to a specified host group.User group administratorAdministrative permissions are limited to a specified user group.

## LSF user roles with EGO enabled

LSF, with EGO enabled, supports the following roles:

- Cluster administrator

  Can administer any objects and workload in the cluster.

- Consumer administrator

  Can administer any objects and workload in consumers to which they have access.

- Consumer user

  Can run workload in consumers to which they have access

User accounts are created and managed in EGO. EGO authorizes users from its user database.

## LSF user groups

Use any existing UNIX and Linux user groups directly by specifying a UNIX or Linux user group anywhere an LSF user group can be specified.

## External authentication

LSF provides a security plug-in for sites that prefer to use external or third-party security mechanisms, such as Kerberos, LDAP, or ActiveDirectory.

You can create a customized eauth executable file to provide external authentication of users, hosts, and daemons. Credentials are passed from an external security system. The eauth executable file can also be customized to obtain credentials from an operating system or from an authentication protocol such as Kerberos.