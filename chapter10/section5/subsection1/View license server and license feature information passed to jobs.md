# View license server and license feature information passed to jobs

## About this task

You can display the license servers that are used by each service domain that is allocated to the license features.

## Procedure

Run blstat -S.

```
blstat -S
FEATURE: feature1
SERVICE_DOMAIN: domain1
SERVERS     INUSE  FREE
 server1      1      0
 server2      0      1
 TOTAL        1      1
SERVICE_DOMAIN: domain2
SERVERS     INUSE  FREE
 server3      1      0
 TOTAL        1      0
```

The license feature feature1 is assigned to server1 and server2 in the domain1 service domain and server3 in the domain2 service domain. A job uses the feature1 license feature when the job is submitted with "rusage[feature1=1]" as the rusage string.

**Parent topic:**

[About viewing available licenses](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/license_scheduler/view_available_licenses.html?view=kc)

## View license usage

### Procedure

Run **blstat -s** to display license usage.

```
blstat -s
FEATURE: p1_f2
SERVICE_DOMAIN: app_1 TOTAL_LICENSE: 10
LSF_USE LSF_DESERVE LSF_FREE   NON_LSF_USE NON_LSF_DESERVE  NON_LSF_FREE
     0       10         10          0           0                 0 
FEATURE: p1_f1
SERVICE_DOMAIN: app_1 TOTAL_LICENSE: 5  
LSF_USE LSF_DESERVE LSF_FREE   NON_LSF_USE NON_LSF_DESERVE  NON_LSF_FREE
     0       5          5           0           0                 0 
```

If there are any distribution policy violations, **blstat** marks these violations with an asterisk (*) at the beginning of the line.

## View workload distribution information

### Procedure

Run **blinfo -a** to display WORKLOAD_DISTRIBUTION information.

```
blinfo -a
FEATURE      MODE       SERVICE_DOMAIN  TOTAL  DISTRIBUTION
g1           Project    LS              10     [p1, 50.0%] [p2, 50.0%]
                                  WORKLOAD_DISTRIBUTION
                                  [LSF 66.7%, NON_LSF 33.3%]
```

## Sort license feature information

### About this task

You can sort license feature information alphabetically, by total licenses, or by available licenses.

The value of total licenses is calculated with the number of licenses LSF workload deserves from all service domains that supply licenses to the feature, regardless of whether non-LSF workload borrowed licenses from LSF workload.

### Procedure

- Sort alphabetically:

  blstat -o alpha

- Sort by total licenses:

  blstat -o total

  The feature with the largest number of total licenses displays first.

- Sort by available licenses:

  blstat -o avail

  The feature with the largest number of available licenses displays first.

  You can also run **blstat -o** with options **-Lp**, **-t**, **-D**, **-G**, **-s**, **-S**.

  **Note**

  The values of "total licenses" and "licenses available" are calculated differently when **blstat -o** is used with different options:

  - Options **-Lp**, **-t**, **-D**, **-G**: Total licenses means the sum of licenses that are allocated to LSF workload from all the service domains that are configured to supply licenses to the feature. Licenses that are borrowed by non-LSF workload are subtracted from this sum.
  - Options**-s**, **-S**: Total licenses means all the licenses (supplied by the license vendor daemon) from all the service domains that are configured to supply licenses to that feature.

## Limitations with viewing multiple jobs running on an execution host

If there are multiple jobs submitted by a user that run on the same execution host, **blstat** might not display the correct license usage information. This is because **lmstat** only provides the user and host information of each license checkout, but does not provide additional information for LSF License Scheduler to match the license checkout to a specific LSF job.

LSF License Scheduler attempts to match the license checkout to each LSF job based on the user, execution host, and rusage string. If the multiple jobs running on the same execution host are submitted by the same user and request the same license, the information that **lmstat** provides is insufficient for LSF License Scheduler to provide an exact match for each LSF job. LSF License Scheduler estimates the job, but this may be incorrect.

For example,

- There are multiple service domains providing the same feature and a user submits multiple jobs that run on the same execution host.

  Although LSF License Scheduler dispatches the tokens correctly, **blstat** might not show the correct token usage (such as TOTAL_INUSE, TOTAL_RESERVE, or TOTAL_FREE). Incorrect tokens are counted in OTHERS.

- There is one license server with multiple projects and a user submits multiple jobs with some jobs reserving tokens for a time. The jobs that reserve tokens are running on the same host as other

   

  LSF License Scheduler

   

  jobs.

  Although LSF License Scheduler dispatches the tokens correctly, **blstat** may show reversed token usage, so that some INUSE tokens are counted in RESERVED, and some RESERVED tokens are counted in INUSE.