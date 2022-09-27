# Host types and host models

Hosts in LSF are characterized by host type and host model.

The following example has a host type of X86_64. Host models are Opteron240, Opteron840, Intel_EM64T, Intel_IA64.

![img](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/lsf_users_guide/host_type.jpg)

## Host type

The combination of operating system version and host CPU architecture.

All computers that run the same operating system on the same computer architecture are of the same type — in other words, binary-compatible with each other.

Each host type usually requires a different set of LSF binary files.

Commands:

- **lsinfo -t** — View all host types that are defined in lsf.shared

Configuration:

- Defined in lsf.shared
- Mapped to hosts in lsf.cluster.cluster_name

## Host model

The combination of host type and CPU speed (CPU factor) of the computer.

All hosts of the same relative speed are assigned the same host model.

The CPU factor is taken into consideration when jobs are being dispatched.

Commands:

- **lsinfo -m** — View a list of currently running models
- **lsinfo -M** — View all models that are defined in lsf.shared

Configuration:

- Defined in lsf.shared
- Mapped to hosts in lsf.cluster.cluster_name