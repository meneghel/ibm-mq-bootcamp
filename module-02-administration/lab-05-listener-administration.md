# IBM MQ Bootcamp

# Module 02 – Administration & Operations

# Lab 05 – Listener Administration

---

## Lab Overview

Listeners are responsible for accepting inbound network connections for IBM MQ.

Without a Listener, Queue Managers and client applications cannot establish communication.

In this lab, students will create, configure, start, stop and monitor IBM MQ Listeners while validating TCP/IP connectivity and troubleshooting common communication issues.

---

## Learning Objectives

By completing this lab, students will be able to:

* Create IBM MQ Listeners
* Configure Listener attributes
* Start and Stop Listeners
* Monitor Listener status
* Validate network connectivity
* Identify common connectivity issues
* Troubleshoot MQRC 2059 scenarios

---

## Estimated Duration

45 Minutes

---

## Prerequisites

Students should have completed:

* Lab 01 – Queue Manager Lifecycle
* Lab 02 – MQSC Fundamentals
* Lab 03 – Queue Administration
* Lab 04 – Channel Administration

Required Environment:

* IBM MQ Installed
* Queue Manager QM1 Running

---

## Environment

Queue Manager:

```text
QM1
```

Default Port:

```text
1414
```

Administration Interface:

```text
MQSC
```

---

## Scenario

A new application team must connect to IBM MQ.

Your responsibility is to configure the network entry point that will allow applications and remote Queue Managers to communicate with the environment.

---

# Exercise 01 – Review Existing Listeners

Start MQSC:

```bash
runmqsc QM1
```

Display existing Listeners:

```mqsc
DISPLAY LISTENER(*)
```

Questions:

1. How many Listeners are defined?
2. Are any Listeners currently running?
3. Why are Listeners required?

---

# Exercise 02 – Create a Listener

Create:

```mqsc
DEFINE LISTENER(LISTENER.TCP)
TRPTYPE(TCP)
PORT(1414)
CONTROL(QMGR)
```

Verify:

```mqsc
DISPLAY LISTENER(LISTENER.TCP)
```

Questions:

1. Which port was configured?
2. What is the purpose of CONTROL(QMGR)?

---

# Exercise 03 – Start the Listener

Start:

```mqsc
START LISTENER(LISTENER.TCP)
```

Verify:

```mqsc
DISPLAY LSSTATUS(*)
```

Expected Result:

```text
STATUS(RUNNING)
```

Discussion:

What changes after the Listener starts?

---

# Exercise 04 – Display Listener Status

Execute:

```mqsc
DISPLAY LSSTATUS(*)
```

Review:

* STATUS
* PORT
* PID
* STARTDATE
* STARTTIME

Questions:

Which information is most useful during troubleshooting?

---

# Exercise 05 – Verify Network Connectivity

Linux:

```bash
netstat -an | grep 1414
```

or

```bash
ss -an | grep 1414
```

Expected:

```text
LISTEN
```

Questions:

1. What does LISTEN indicate?
2. Why is this verification important?

---

# Exercise 06 – Stop the Listener

Execute:

```mqsc
STOP LISTENER(LISTENER.TCP)
```

Verify:

```mqsc
DISPLAY LSSTATUS(*)
```

Expected:

```text
STATUS(STOPPED)
```

Discussion:

What applications are impacted when a Listener is stopped?

---

# Exercise 07 – Listener Startup Modes

Display:

```mqsc
DISPLAY LISTENER(LISTENER.TCP)
```

Review:

```text
CONTROL(QMGR)
```

Discussion:

Compare:

```text
CONTROL(QMGR)
CONTROL(MANUAL)
```

Questions:

Which option is preferred in production environments?

---

# Exercise 08 – Multiple Listener Scenario

Create:

```mqsc
DEFINE LISTENER(LISTENER.1415)
TRPTYPE(TCP)
PORT(1415)
CONTROL(QMGR)
```

Discussion:

Why might organizations deploy multiple Listeners?

Examples:

* Environment Segregation
* Migration Projects
* Security Requirements

---

# Exercise 09 – Investigate MQRC 2059

Research:

```text
MQRC_Q_MGR_NOT_AVAILABLE
```

Discussion:

Common causes:

* Queue Manager Stopped
* Listener Stopped
* Incorrect Hostname
* Incorrect Port
* Firewall Blocking Traffic

---

# Exercise 10 – Port Conflict Analysis

Research:

```text
Port Already In Use
```

Linux:

```bash
netstat -tulpn
```

or

```bash
ss -tulpn
```

Questions:

1. How can administrators identify port conflicts?
2. Why are port conflicts problematic?

---

# Validation Checklist

Confirm that you can:

* Create a Listener
* Start a Listener
* Stop a Listener
* Display Listener Status
* Validate TCP Connectivity
* Understand Listener Startup Modes
* Identify Common Connectivity Issues

---

# Challenge Exercise

Research and document:

1. Default IBM MQ Ports
2. Firewalls and MQ Connectivity
3. Load Balancers and MQ
4. DNS Dependencies
5. Client Connection Flows

---

# Expected Outcome

Upon completion of this lab, students will understand how IBM MQ Listeners enable connectivity and will be able to configure, monitor and troubleshoot Listener-related issues in enterprise environments.

---

## Next Lab

Proceed to:

**Lab 06 – Monitoring & Operations**
