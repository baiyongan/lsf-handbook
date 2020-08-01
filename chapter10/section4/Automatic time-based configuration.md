# Automatic time-based configuration

Variable time-based configuration is used in both project mode and cluster mode to automatically change configuration that is set in lsf.licensescheduler based on time windows. For example, if you have design centers in remote locations, one use of time-based configuration is to switch ownership of license tokens that are based on local time of day.

You define automatic configuration changes in lsf.licensescheduler by using if-else constructs and time expressions. After you change the files, reconfigure the cluster with the **bladmin reconfig** command.

The expressions are evaluated by License Scheduler every 10 minutes based on **bld** start time. When an expression evaluates true, License Scheduler dynamically changes the configuration that is based on the associated configuration statements and restarts **bld**

The #if, #else, #endif keywords are not interpreted as comments by License Scheduler, but as if-else constructs.

**Parent topic:**

[Configuring License Scheduler](https://www.ibm.com/support/knowledgecenter/SSWRJV_10.1.0/license_scheduler/chap_config_ls.html?view=kc)

## Syntax

```
time = hour | hour:minute | day:hour:minute
```

- hour

  Specify an integer from 0 to 23, representing the hour of the day.

- minute

  integer from 0 to 59, representing the minute of the hour.If you do not specify the minute, License Scheduler assumes the first minute of the hour (:00).

- day

  Specify an integer from 0 to 7, representing the day of the week, where 0 represents every day, 1 represents Monday, and 7 represents Sunday.If you do not specify the day, License Scheduler assumes every day. If you do specify the day, you must also specify the minute.

## Specify time values

### Procedure

Specify at least the hour.

Day and minutes are optional.

## Specify time windows

### Procedure

Specify two time values that are separated by a hyphen (-), with no space in between.

```
time_window = time1-time2
```

time1 is the start of the window and time2 is the end of the window. Both time values must use the same syntax.

Use one of the following ways to specify a time window:

- hour-hour
- hour:minute-hour:minute
- day:hour:minute-day:hour:minute

For example:

- Daily window

  To specify a daily window, omit the day field from the time window. Use either the hour-hour or hour:minute-hour:minute format. For example, to specify a daily 8:30 a.m. to 6:30 p.m. window:

  ```
  8:30-18:30
  ```

- Overnight window

  To specify an overnight window, make time1 greater than time2. For example, to specify 6:30 p.m. to 8:30 a.m. the following day:

  ```
  18:30-8:30
  ```

- Weekend window

  To specify a weekend window, use the day field. For example, to specify Friday at 6:30 p.m to Monday at 8:30 a.m.:

  ```
  5:18:30-1:8:30
  ```

## Specify time expressions

### About this task

Time expressions use time windows to specify when to change configurations.

### Procedure

Define a time expression.

A time expression is made up of the time keyword followed by one or more space-separated time windows that are enclosed in parentheses. Use the &&, ||, and ! logical operators to combine time expressions.

```
expression = time(time_window[ time_window ...])
             | expression && expression
             | expression || expression
             | !expression
```

For example:

Both of the following expressions specify weekends (Friday evening at 6:30 p.m. until Monday morning at 8:30 a.m.) and nights (8:00 p.m. to 8:30 a.m. daily).

```
time(5:18:30-1:8:30 20:00-8:30)
time(5:18:30-1:8:30) || time(20:00-8:30)
```

## Create if-else constructs

### About this task

The if-else construct can express single decisions and multi-way decisions by including elif statements in the construct.

### Procedure

- Define an if-else expression.

  ```
  #if time(expression) 
  statement 
  #else
  statement 
  #endif
  ```

  The #endif part is mandatory and the #else part is optional.

- Define an elif expression.

  The #elif expressions are evaluated in order. If any expression is true, the associated statement is used, and this terminates the whole chain.

  The #else part handles the default case where no other conditions are satisfied.

  ```
  #if time(expression)
  statement
  #elif time(expression)
  statement
  #elif time(expression)
  statement
  #else 
  statement 
  #endif
  ```

  When you use #elif, the #else and #endif parts are required.

## Restart to implement configuration changes

### About this task

All time-based configuration is within the lsf.licensescheduler file, so restarting the **bld** applies all changes.

### Procedure

1. Run bladmin ckconfig to check configuration.
2. Run lsadmin limrestart or bladmin restart to restart the **bld**.

## Verify configuration

### About this task

Verify time-based configuration by viewing License Scheduler information.

### Procedure

1. Run blinfo.
2. Run blstat.

## Examples

### Project configuration in project mode

```
Begin Feature
NAME = f1 
#if time(5:16:30-1:8:30 20:00-8:30)
DISTRIBUTION=Lan(P1 2/5  P2 1)
#elif time(3:8:30-3:18:30)
DISTRIBUTION=Lan(P3 1)
#else
DISTRIBUTION=Lan(P1 1 P2 2/5)
#endif
End Feature
```

### Project group configuration in project mode

```
#
# ProjectGroup section
#
Begin ProjectGroup
GROUP             SHARES   OWNERSHIP  LIMITS     NON_SHARED
(group1 (A B))    (1 1)    (5 -)         ()         ()
End ProjectGroup
 
Begin ProjectGroup
GROUP             SHARES   OWNERSHIP  LIMITS     NON_SHARED
(group2 (A B))    (1 1)    (- 5)         ()         ()
End ProjectGroup
 
#
# Feature section
#
Begin Feature
NAME = f1 
#if time(5:16:30-1:8:30 20:00-8:30)
GROUP_DISTRIBUTION=group1
#elif time(3:8:30-3:18:30)
GROUP_DISTRIBUTION=group2
#else
GROUP_DISTRIBUTION=group2
#endif
SERVICE_DOMAINS=Lan1 Lan2
End Feature
```

### Cluster distribution configuration in cluster mode

```
Begin Feature
NAME = f1
#if time(5:16:30-1:8:30 20:00-8:30)
CLUSTER_DISTRIBUTION=Wan(Cl1 1 Cl2 1)
#elif time(3:8:30-3:18:30)
CLUSTER_DISTRIBUTION= Wan(Cl1 2 Cl2 1/2/100) Lan(Cl2 1)
#else
CLUSTER_DISTRIBUTION= Wan(Cl1 10 Cl2 1/1/10) Lan(Cl1 1)
#endif
End Feature
```