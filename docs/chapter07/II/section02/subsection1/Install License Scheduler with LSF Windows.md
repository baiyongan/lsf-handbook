# Install License Scheduler with LSF (Windows)

## Before you begin

You must already have LSF installed on all Windows hosts you intend to install License Scheduler on.

## About this task

This installation option means that License Scheduler manages licenses for jobs that are submitted through LSF and through any other applications.

Install License Scheduler on Windows hosts only when your LSF cluster includes both UNIX and Windows hosts.

## Procedure

1. Download the License Scheduler Client for Windows package.
2. Copy all commands to **$LSF_BINDIR** (the bin subdirectory in your LSF installation directory) on your Windows hosts.
3. Copy lsf.licensescheduler to **$LSF_ENVDIR**.
4. Edit lsf.licensescheduler to suit your License Scheduler Master host configuration.