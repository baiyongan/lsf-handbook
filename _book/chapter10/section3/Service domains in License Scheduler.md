# Service domains in License Scheduler

A service domain is a group of one or more license servers. License Scheduler manages the scheduling of the license tokens, but the license server actually supplies the licenses. You configure the service domain with the license server names and port numbers that serve licenses to a network.

- LAN: a service domain that serves licenses to a single cluster
- WAN: a sevice domain that serves licenses to multiple clusters

License Scheduler assumes that any license in the service domain is available to any user who can receive a token from License Scheduler. Therefore, every user that is associated with a project specified in the distribution policy must meet the following requirements:

- The user is able to make a network connection to every license server host in the service domain.
- The user environment is configured with permissions to check out the license from every license server host in the service domain.

You must configure at least one service domain for License Scheduler. It groups license server hosts that serve licenses to LSF jobs and is used when you define a policy for sharing software licenses among your projects.

If a license server is not part of a License Scheduler service domain, its licenses are not managed by License Scheduler (the license distribution policies you configure in LSF do not apply to these licenses and usage of these licenses does not influence LSF scheduling decisions).

## Service domain locality

You can use license feature locality to limit features from different service domains to a specific cluster so that License Scheduler does not grant tokens to jobs from license that legally cannot be used on the cluster that requested the token. The LAN service domains that are used in cluster mode are configured with single-cluster locality.

## Project mode

In project mode, a cluster can access the same license feature from multiple service domains.

If your license servers restrict the serving of license tokens to specific geographical locations, use **LOCAL_TO** to specify the locality of a license token for any features that cannot be shared across all the locations. This parameter avoids having to define different distribution and allocation policies for different service domains, and allows hierarchical project group configurations.

To use License Scheduler tokens in project mode, a job submission must specify the **-Lp** (license project) option. The project must be defined for the requested feature in lsf.licensescheduler.

## Cluster mode

In cluster mode, each license feature in a cluster can access a single license feature from at most one WAN and one LAN service domain.

License Scheduler does not control application checkout behavior. If the same license is available from both the LAN and WAN service domains, License Scheduler expects jobs to try to obtain the license from the LAN first.

## Parallel jobs

When LSF dispatches a parallel job, LSF License Scheduler attempts to check out user@host keys in the parallel job constructed using the user name and all execution host names, and merges the corresponding checkout information on the service domain if found.

For example, in project mode, for feature F1 with two projects (P1 and P2) in service domain sd1, with ten tokens, a parallel job is dispatched to four execution hosts using the following command:

bsub -n 4 -Lp P1 -R "rusage[F1=4]" mycmd

The job on each execution host checks out one F1 license from the sd1 service domain. If the four execution hosts are hostA, hostB, hostC, and hostD, there are checkout keys for user@hostA, user@hostB, user@hostC, and user@hostD, and each entry contributes corresponds with one token checked out. These tokens all merge into data for the P1 project in the F1 feature. Therefore, running **blstat** displays the following information for the F1 feature:

```
FEATURE: F1
 SERVICE_DOMAIN: LanServer
 TOTAL_INUSE: 4    TOTAL_RESERVE: 0    TOTAL_FREE: 6    OTHERS: 0
  PROJECT                 SHARE     OWN       INUSE     RESERVE   FREE      DEMAND
  P1                      50.0 %    0         4         0         1         0
  P2                      50.0 %    0         0         0         5         0
```

The four checkout keys from the four execution hosts are merged into the P1 project.

If MERGE_BY_SERVICE_DOMAIN=Y is defined, LSF License Scheduler also merges multiple user@host data for parallel jobs across different service domains.

For example, if you have the same setup as the previous example, but with an additional service domain sd2 also with two projects (P1 and P2) and ten tokens, and you have MERGE_BY_SERVICE_DOMAIN=Y defined, running **blstat** displays the following information for the F1 feature:

```
blstat
FEATURE: F1
 SERVICE_DOMAIN: sd1
 TOTAL_INUSE: 2    TOTAL_RESERVE: 0    TOTAL_FREE: 8    OTHERS: 0
  PROJECT                 SHARE     OWN       INUSE     RESERVE   FREE      DEMAND
  P1                      50.0 %    0         2         0         3         0
  P2                      50.0 %    0         0         0         5         0
 SERVICE_DOMAIN: sd2
 TOTAL_INUSE: 2    TOTAL_RESERVE: 0    TOTAL_FREE: 8    OTHERS: 0
  PROJECT                 SHARE     OWN       INUSE     RESERVE   FREE      DEMAND
  P1                      50.0 %    0         2         0         3         0
  P2                      50.0 %    0         0         0         5         0
```

Two checkout keys are merged into the P1 project in the sd1 domain, while two checkout keys are merged into the P1 project under the sd2 domain.

If CHECKOUT_FROM_FIRST_HOST_ONLY=Y is defined, LSF License Scheduler only considers user@host information for the first execution host of a parallel job when merging the license usage data. Setting in individual Feature sections overrides the global setting in the Parameters section.

If a feature has multiple Feature sections (using **LOCAL_TO**), each section must have the same setting for **CHECKOUT_FROM_FIRST_HOST_ONLY**.