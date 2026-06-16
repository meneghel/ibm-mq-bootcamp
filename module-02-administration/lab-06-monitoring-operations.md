# IBM MQ Bootcamp

# Module 02 – Administration & Operations

# Lab 06 – Monitoring & Operations

---

## Lab Overview

Monitoring is one of the most important responsibilities of an IBM MQ Administrator.

Most production incidents provide warning signs before they impact business processes.

In this lab, students will learn how to monitor Queue Managers, Queues, Channels and Listeners while analyzing operational indicators, logs and common troubleshooting scenarios.

This lab introduces the monitoring mindset required for supporting IBM MQ in enterprise production environments.

---

## Learning Objectives

By completing this lab, students will be able to:

* Monitor Queue Managers
* Monitor Queue Depth
* Monitor Channel Status
* Monitor Listener Status
* Analyze Error Logs
* Understand FDC Files
* Identify operational anomalies
* Apply monitoring best practices

---

## Estimated Duration

60 Minutes

---

## Prerequisites

Students should have completed:

* Lab 01 – Queue Manager Lifecycle
* Lab 02 – MQSC Fundamentals
* Lab 03 – Queue Administration
* Lab 04 – Channel Administration
* Lab 05 – Listener Administration

Required Environment:

* IBM MQ Installed
* Queue Manager QM1 Running

---

## Environment

Queue Manager:

```text
QM1
```

Administration Interface:

```text
MQSC
```

Log Directory:

```text
/var/mqm/errors
```

---

## Scenario

You are part of the middleware operations team responsible for monitoring a production IBM MQ environment.

Your objective is to verify the health of the Queue Manager, identify potential issues and understand how administrators detect and troubleshoot operational problems before they impact business services.

---

# Exercise 01 – Verify Queue Manager Status

Start MQSC:

```bash
runmqsc QM1
```

Execute:

```mqsc
DISPLAY QMSTATUS
```

Review:

* Queue Manager Status
* Connection Information
* Log Utilization

Questions:

1. Why should Queue Manager status be monitored?
2. What indicators suggest operational issues?

---

# Exercise 02 – Monitor Queue Depth

Display Queue Status:

```mqsc
DISPLAY QSTATUS(APP.REQUEST)
```

Review:

```text
CURDEPTH
IPPROCS
OPPROCS
```

Questions:

1. What does CURDEPTH represent?
2. Why is queue growth important?

---

# Exercise 03 – Analyze Queue Activity

Execute:

```mqsc
DISPLAY QSTATUS(APP.REQUEST)
LPUTDATE
LPUTTIME
LGETDATE
LGETTIME
```

Discussion:

* When was the last message received?
* When was the last message consumed?
* How can this information assist troubleshooting?

---

# Exercise 04 – Monitor Channel Status

Display:

```mqsc
DISPLAY CHSTATUS(*)
```

Review:

```text
STATUS
CONNAME
MSGS
XQMSGS
```

Questions:

1. Which channels are RUNNING?
2. Are any channels RETRYING?
3. What information is useful during incident analysis?

---

# Exercise 05 – Monitor Listener Status

Display:

```mqsc
DISPLAY LSSTATUS(*)
```

Review:

```text
STATUS
PORT
STARTDATE
STARTTIME
```

Discussion:

Why is Listener availability critical?

---

# Exercise 06 – Review Error Logs

Navigate to:

```bash
cd /var/mqm/errors
```

Display recent entries:

```bash
tail -50 AMQERR01.LOG
```

Questions:

1. What types of messages appear in the error log?
2. How can logs assist troubleshooting?

---

# Exercise 07 – Identify FDC Files

Display:

```bash
ls -la /var/mqm/errors
```

Look for:

```text
*.FDC
```

Discussion:

1. What does FDC stand for?
2. When are FDC files generated?
3. Why are they important for IBM Support?

---

# Exercise 08 – Queue Capacity Analysis

Display:

```mqsc
DISPLAY QLOCAL(APP.REQUEST)
MAXDEPTH
```

Display:

```mqsc
DISPLAY QSTATUS(APP.REQUEST)
CURDEPTH
```

Calculate:

```text
Queue Utilization %
```

Discussion:

At what point should administrators generate alerts?

---

# Exercise 09 – Operational Health Review

Review:

```text
Queue Manager Status
Queue Depth
Channel Status
Listener Status
Error Logs
```

Create a simple operational report describing:

* Current State
* Risks Identified
* Recommended Actions

---

# Exercise 10 – Monitoring Threshold Design

Define thresholds for:

### Queue Depth

```text
Warning: 80%
Critical: 90%
```

### Channel Status

```text
RETRYING = Warning
STOPPED = Critical
```

### Listener Status

```text
STOPPED = Critical
```

Discussion:

Why are thresholds important?

---

# Validation Checklist

Confirm that you can:

* Display Queue Manager Status
* Monitor Queue Depth
* Monitor Queue Activity
* Monitor Channel Status
* Monitor Listener Status
* Review MQ Error Logs
* Identify FDC Files
* Define Monitoring Thresholds

---

# Challenge Exercise

Research and document:

1. IBM Instana
2. Prometheus Monitoring for MQ
3. Grafana Dashboards
4. Splunk Integration
5. Enterprise Monitoring Strategies

---

# Expected Outcome

Upon completion of this lab, students will understand how IBM MQ environments are monitored and how administrators identify issues before they impact production workloads.

Students will be able to perform basic operational monitoring and contribute to enterprise middleware support activities.

---

## Next Lab

Proceed to:

**Lab 07 – Backup & Configuration Management**
