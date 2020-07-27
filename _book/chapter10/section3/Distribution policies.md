# Distribution policies

The most important part of License Scheduler is license token distribution. The license distribution policy determines how license tokens are shared among projects or clusters. Whenever there is competition, the configured share assignment determines the portion of license tokens each project or cluster is entitled to.

We refer to both licenses and license tokens because License Scheduler does not control licenses directly. Instead, it controls the dispatch of jobs that require licenses that are submitted through LSF or **taskman** by tracking license tokens.

## Total license tokens

The total number of license tokens that are managed by License Scheduler for a single feature in one service domain depends on the following factors:

- The number of active license servers in the service domain
- The number of licenses that are checked out by applications that are not managed by LSF

## License shares

License shares that are assigned in the distribution policy determine what portion of total licenses a project (in project mode) or cluster (in cluster mode) receives. Each project or cluster able to use a license feature must have a share of the license feature in the service domain.

The formula for converting a number of shares to a number of licenses for any license feature is:

```
(shares assigned to project or cluster)
______________________________          x (total number of licenses) 
(sum of all shares assigned)
```

The number of shares that are assigned to a license project or cluster is only meaningful when you compare it to the number assigned to other projects or clusters, or to the total number of shares.

When there are no jobs in the system, each project or cluster is assigned license tokens that are based on share assignments.

**Parent topic:**

[LSF License Scheduler concepts](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/license_scheduler/chap_concepts_ls.html?view=kc)

## Cluster mode distribution policies

- static

  A portion of the total licenses is allocated to the cluster based on the configured share. The amount is static, and does not depend on the workload in the system.

- dynamic

  Shares of the total licenses are assigned to each cluster, along with a buffer size. The configured shares set the number of licenses each cluster receives initially, but this number is adjusted regularly based on demand from the cluster.License distribution changes whenever a cluster requests an allocation update, by default every 15 seconds. In each update, the allocation can increase by as much as the buffer size. There is no restriction on decreasing cluster allocation.When dynamic license distribution is used in cluster mode, minimum and maximum allocation values can be configured for each cluster. The minimum allocation is like the number of non-shared licenses for project mode, as this number of tokens is reserved for the exclusive use of the cluster.If the minimum value configured exceeds the share assignment for the cluster, only the assigned share is reserved for the cluster.Cluster shares take precedence over minimum allocations configured. If the minimum allocation exceeds the cluster's share of the total tokens, a cluster's allocation as given by **bld** may be less than the configured minimum allocation.

- guarantees within a cluster

  Guaranteed shares of licenses are assigned to projects within a cluster that use LSF guarantee-type SLAs. Optionally, sharing of guaranteed licenses not in use can be configured.Guarantees are like ownership for cluster mode, and can be used with both static and dynamic distribution policies.**Note**Guarantee-type SLAs are only available in LSF version 8.0 or newer.

### When to use static license distribution

Configure shares for all license features in cluster mode. Static license distribution is the basic license distribution policy, and is built on by adding more configuration.

The basic static configuration can meet your needs if the demand for licenses across clusters is predictable and unchanging, or licenses are strictly owned by clusters, or you always have extra licenses.

### When to use dynamic license distribution

Dynamic license allocation can meet your needs if the demand for licenses changes across clusters.

### When to use LSF guarantee SLAs with License Scheduler

Configuring guarantee SLAs within LSF clusters can meet your needs if the licenses within a cluster are owned, and used either preferentially or exclusively by the license owners.

## Project mode distribution policies

- fairshare

  Shares of the total licenses are assigned to each license project.Unused licenses are shared wherever there is demand, however, when demand exceeds the number of licenses, share assignments are followed. Jobs are not preempted to redistribute licenses; instead licenses are redistributed when jobs finish running.

- ownership and preemption

  Shares of the total licenses are assigned to each license project. Owned shares of licenses are also assigned.Unused licenses are shared wherever there is demand, however, when demand exceeds the number of licenses, the owned share is reclaimed using preemption.Preemption occurs only while the specified number of owned licenses are not yet in use, and no free licenses are available. Once all owned licenses are used, License Scheduler waits for licenses to become free (instead of using preemption) and then distributes more tokens until the share is reached.Jobs that are preempted by License Scheduler are automatically resumed once licenses become available.By default, LSF releases the job slot of a suspended job when License Scheduler preempts the license from the job.**Note**For License Scheduler to give a license token to another project, the applications must be able to release their licenses upon job suspension.

- active ownership

  Active ownership allows ownership to automatically adjust based on project activity. Ownership is expressed as a percent of the total ownership for active projects. The actual ownership for each project decreases as more projects become active. Set percentage ownership values to total more than 100% to benefit from active ownership.

- non-shared licenses

  Some licenses are designated as non-shared, and are reserved for exclusive use instead of being shared when not in use.The number of non-shared licenses is contained by the number of owned licenses, but this number is not included in share calculations for the project. To designate some licenses as non-shared, add the non-shared number to both the owned and the non-shared values.

### When to use fairshare with project mode

Configure fairshare for all license features in project mode. Fairshare is the basic license distribution policy, and is built on by adding additional configuration.

The basic fairshare configuration can meet your needs without configuring additional distribution policies if the licenses are assigned to specific license projects, but not strictly owned.

### When to add ownership (and preemption)

Configure licenses as owned when:

- Licenses are owned by licenses projects, but can be loaned out when not in use.
- Maximizing license usage and license ownership are both important considerations. Loaned licenses must be returned to the owners as quickly as possible when needed (using preemption).
- Jobs borrowing licenses can be preempted.

### When to add active ownership

Configure active ownership for owned licenses when:

- Ownership values are dynamic instead of being fixed values, and usually decrease as more projects actively seek licenses.

### When to add non-shared licenses

Configure licenses as non-shared when:

- Licenses are owned.
- Licenses are used exclusively by the owners.
- Having licenses always available to the owners is more important than maximizing license use.