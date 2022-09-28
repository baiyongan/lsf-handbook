# LSF daemons

| LSF daemon         | Role                      |
| :----------------- | :------------------------ |
| **mbatchd**        | Job requests and dispatch |
| **mbschd**         | Job scheduling            |
| **sbatchd****res** | Job execution             |

------

**Parent topic:**

[About IBM Spectrum LSF](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_users_guide/chap_lsf_about.html?view=kc)

## mbatchd

- Master Batch Daemon running on the master host.
- Started by **sbatchd**.
- Responsible for the overall state of jobs in the system.
- Receives job submission, and information query requests.
- Manages jobs that are held in queues. Dispatches jobs to hosts as determined by **mbschd**.

### Configuration

- Port number is defined in lsf.conf.

## mbschd

- Master Batch Scheduler Daemon running on the master host.
- Works with **mbatchd**.
- Started by **mbatchd**.
- Makes scheduling decisions based on job requirements, and policies, and resource availability. Sends scheduling decisions to **mbatchd**.

## sbatchd

- Slave Batch Daemon running on each server host.
- Receives the request to run the job from **mbatchd** and manages local execution of the job.
- Responsible for enforcing local policies and maintaining the state of jobs on the host.
- The **sbatchd** forks a child **sbatchd** for every job. The child **sbatchd** runs an instance of **res** to create the execution environment in which the job runs. The child **sbatchd** exits when the job is complete.

### Commands

- **badmin hstartup** — Starts **sbatchd**
- **badmin hshutdown** — Shuts down **sbatchd**
- **badmin hrestart** — Restarts **sbatchd**

### Configuration

- Port number is defined in lsf.conf

## res

- Remote Execution Server (**res**) running on each server host.
- Accepts remote execution requests to provide transparent and secure remote execution of jobs and tasks.

### Commands

- **lsadmin resstartup** — Starts **res**
- **lsadmin resshutdown** — Shuts down **res**
- **lsadmin resrestart** — Restarts **res**

### Configuration

- Port number is defined in lsf.conf.

## lim

- Load Information Manager (LIM) running on each server host.
- Collects host load and configuration information and forwards it to the master LIM running on the master host.
- Reports the information that is displayed by **lsload** and **lshosts**.
- Static indices are reported when the LIM starts up or when the number of CPUs (ncpus) change. Static indices are:
  - Number of CPUs (ncpus)
  - Number of disks (ndisks)
  - Total available memory (maxmem)
  - Total available swap (maxswp)
  - Total available temp (maxtmp)
  - Dynamic indices for host load collected at regular intervals are:
  - Hosts status (status)
  - 15 second, 1 minute, and 15 minute run queue lengths (r15s, r1m, and r15m)
  - CPU utilization (ut)
  - Paging rate (pg)
  - Number of login sessions (ls)
  - Interactive idle time (it)
  - Available swap space (swp)
  - Available memory (mem)
  - Available temp space (tmp)
  - Disk IO rate (io)

### Commands

- **lsadmin limstartup** — Starts LIM
- **lsadmin limshutdown** — Shuts down LIM
- **lsadmin limrestart** — Restarts LIM
- **lsload** — View dynamic load values
- **lshosts** — View static host load values

### Configuration

- Port number is defined in lsf.conf.

## Master LIM

- The LIM running on the master host. Receives load information from the LIMs running on hosts in the cluster.
- Forwards load information to **mbatchd**, which forwards this information to **mbschd** to support scheduling decisions. If the master LIM becomes unavailable, a LIM on another host automatically takes over.

### Commands

- **lsadmin limstartup** — Starts LIM
- **lsadmin limshutdown** — Shuts down LIM
- **lsadmin limrestart** — Restarts LIM
- **lsload** — View dynamic load values
- **lshosts** — View static host load values

### Configuration

- Port number is defined in lsf.conf.

## ELIM

External LIM (ELIM) is a site-definable executable that collects and tracks custom dynamic load indices. An ELIM can be a shell script or a compiled binary program, which returns the values of the dynamic resources you define. The ELIM executable must be named elim and located in **LSF_SERVERDIR**.

## pim

- Process Information Manager (PIM) running on each server host.
- Started by LIM, which periodically checks on **pim** and restarts it if it dies.
- Collects information about job processes running on the host such as CPU and memory that is used by the job, and reports the information to **sbatchd**.

### Commands

- **bjobs** — View job information