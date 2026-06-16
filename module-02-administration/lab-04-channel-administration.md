# IBM MQ Bootcamp

# Module 02 – Administration & Operations

# Lab 04 – Channel Administration

---

## Lab Overview

Channels are responsible for communication between Queue Managers and client applications.

Without channels, distributed messaging cannot occur.

In this lab, students will create and manage channels, configure transmission queues, monitor channel status and troubleshoot common communication issues.

This lab simulates activities frequently performed by IBM MQ administrators in production environments.

---

## Learning Objectives

By completing this lab, students will be able to:

* Understand channel architecture
* Create Transmission Queues
* Create Sender Channels
* Create Receiver Channels
* Monitor Channel Status
* Start and Stop Channels
* Interpret Channel States
* Troubleshoot common communication failures

---

## Estimated Duration

75 Minutes

---

## Prerequisites

Students should have completed:

* Lab 01 – Queue Manager Lifecycle
* Lab 02 – MQSC Fundamentals
* Lab 03 – Queue Administration

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

---

## Scenario

Your organization is deploying a new integration flow that requires communication between two IBM MQ environments.

As the MQ Administrator, you must configure the required communication components and validate connectivity.

---

# Exercise 01 – Review Existing Channels

Start MQSC:

```bash
runmqsc QM1
```

Display all channels:

```mqsc
DISPLAY CHANNEL(*)
```

Questions:

1. How many channels exist?
2. Which channels are system channels?
3. Why are channels required?

---

# Exercise 02 – Create a Transmission Queue

Create:

```mqsc
DEFINE QLOCAL(QM2.XMITQ)
USAGE(XMITQ)
```

Verify:

```mqsc
DISPLAY QLOCAL(QM2.XMITQ)
```

Questions:

1. What is the purpose of a Transmission Queue?
2. When are messages stored in an XMITQ?

---

# Exercise 03 – Create a Sender Channel

Create:

```mqsc
DEFINE CHANNEL(QM1.TO.QM2)
CHLTYPE(SDR)
TRPTYPE(TCP)
XMITQ(QM2.XMITQ)
CONNAME('server2.company.com(1414)')
```

Verify:

```mqsc
DISPLAY CHANNEL(QM1.TO.QM2)
```

Discussion:

* What is the role of a Sender Channel?
* Why is CONNAME required?

---

# Exercise 04 – Create a Receiver Channel

Create:

```mqsc
DEFINE CHANNEL(QM1.TO.QM2)
CHLTYPE(RCVR)
TRPTYPE(TCP)
```

Discussion:

* Why must Sender and Receiver Channels share the same name?
* What happens if one side is missing?

---

# Exercise 05 – Create a Server Connection Channel

Create:

```mqsc
DEFINE CHANNEL(APP.SVRCONN)
CHLTYPE(SVRCONN)
TRPTYPE(TCP)
```

Verify:

```mqsc
DISPLAY CHANNEL(APP.SVRCONN)
```

Discussion:

* Which applications typically use SVRCONN channels?
* Why are they critical for client connectivity?

---

# Exercise 06 – Start a Channel

Start:

```mqsc
START CHANNEL(QM1.TO.QM2)
```

Verify:

```mqsc
DISPLAY CHSTATUS(QM1.TO.QM2)
```

Expected Status:

```text
RUNNING
```

or

```text
RETRYING
```

depending on connectivity.

---

# Exercise 07 – Review Channel Status

Display:

```mqsc
DISPLAY CHSTATUS(*)
```

Review:

```text
STATUS
MSGS
XQMSGS
CONNAME
```

Questions:

1. What does STATUS represent?
2. What information is useful during troubleshooting?

---

# Exercise 08 – Analyze Channel States

Research and document:

```text
RUNNING
STOPPED
RETRYING
INITIALIZING
BINDING
```

Discussion:

Which states indicate healthy operation?

Which states indicate a problem?

---

# Exercise 09 – Stop a Channel

Execute:

```mqsc
STOP CHANNEL(QM1.TO.QM2)
```

Verify:

```mqsc
DISPLAY CHSTATUS(QM1.TO.QM2)
```

Discussion:

Why might an administrator intentionally stop a channel?

---

# Exercise 10 – Simulate XMITQ Growth

Display:

```mqsc
DISPLAY QSTATUS(QM2.XMITQ)
```

Discussion:

If the Receiver Channel becomes unavailable:

* What happens to messages?
* Where are they stored?
* What symptoms would administrators observe?

---

# Exercise 11 – Investigate MQRC 2059

Research:

```text
MQRC_Q_MGR_NOT_AVAILABLE
```

Discussion:

Common causes:

* Queue Manager Down
* Listener Down
* Wrong Hostname
* Wrong Port

---

# Exercise 12 – Investigate MQRC 2009

Research:

```text
MQRC_CONNECTION_BROKEN
```

Discussion:

Common causes:

* Network Failure
* Firewall Interruption
* TLS Problems
* Server Restart

---

# Exercise 13 – Reset Channel Discussion

Research:

```mqsc
RESET CHANNEL(...)
```

Questions:

1. Why should RESET CHANNEL be used carefully?
2. What problems does it solve?

---

# Validation Checklist

Confirm that you can:

* Create a Transmission Queue
* Create Sender Channels
* Create Receiver Channels
* Create SVRCONN Channels
* Start Channels
* Stop Channels
* Display Channel Status
* Interpret Channel States
* Identify common communication failures

---

# Challenge Exercise

Research and document:

1. Cluster Sender Channels
2. Cluster Receiver Channels
3. HBINT
4. DISCINT
5. BATCHSZ
6. Sequence Number Errors

---

# Expected Outcome

Upon completion of this lab, students will understand how IBM MQ channels enable communication between Queue Managers and applications.

Students will also be able to identify and troubleshoot common channel-related issues frequently encountered in production environments.

---

## Next Lab

Proceed to:

**Lab 05 – Listener Administration**
