# IBM MQ Bootcamp

# Module 02 – Administration & Operations

# Lab 03 – Queue Administration

---

## Lab Overview

Queues are the primary storage mechanism of IBM MQ.

Every message exchanged through IBM MQ is stored in one or more queues during its lifecycle.

In this lab, students will learn how to create, configure, monitor and administer IBM MQ queues while applying operational practices commonly used in production environments.

---

## Learning Objectives

By completing this lab, students will be able to:

* Create Local Queues
* Create Remote Queues
* Create Alias Queues
* Configure a Dead Letter Queue
* Monitor Queue Depth
* Analyze Queue Status
* Configure Queue Attributes
* Identify common queue-related issues

---

## Estimated Duration

60 Minutes

---

## Prerequisites

Students should have completed:

* Module 01 – Fundamentals
* Lab 01 – Queue Manager Lifecycle
* Lab 02 – MQSC Fundamentals

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

You have been assigned responsibility for supporting a business application that exchanges messages through IBM MQ.

Your objective is to create and manage the queues required by the application while monitoring queue activity and validating operational readiness.

---

# Exercise 01 – Review Existing Queues

Start MQSC:

```bash
runmqsc QM1
```

Display Local Queues:

```mqsc
DISPLAY QLOCAL(*)
```

Questions:

1. How many queues exist?
2. Which queues are system queues?
3. Which queues were created during previous labs?

---

# Exercise 02 – Create Application Queues

Create:

```mqsc
DEFINE QLOCAL(APP.REQUEST)
```

Create:

```mqsc
DEFINE QLOCAL(APP.REPLY)
```

Verify:

```mqsc
DISPLAY QLOCAL(APP.*)
```

Questions:

1. Why are separate request and reply queues commonly used?
2. Which messaging pattern uses this approach?

---

# Exercise 03 – Create a Dead Letter Queue

Create:

```mqsc
DEFINE QLOCAL(APP.DLQ)
```

Configure:

```mqsc
ALTER QMGR DEADQ(APP.DLQ)
```

Verify:

```mqsc
DISPLAY QMGR DEADQ
```

Questions:

1. Why should every Queue Manager have a DLQ?
2. What types of failures generate DLQ messages?

---

# Exercise 04 – Create an Alias Queue

Create:

```mqsc
DEFINE QALIAS(APP.INPUT) TARGET(APP.REQUEST)
```

Verify:

```mqsc
DISPLAY QALIAS(APP.INPUT)
```

Discussion:

* Why would administrators use Alias Queues?
* How can Alias Queues simplify migrations?

---

# Exercise 05 – Create a Remote Queue

Create:

```mqsc
DEFINE QREMOTE(APP.REMOTE)
RNAME(APP.REQUEST)
RQMNAME(QM2)
```

Verify:

```mqsc
DISPLAY QREMOTE(APP.REMOTE)
```

Discussion:

* What is the difference between Local and Remote Queues?
* Why does a Remote Queue not store messages?

---

# Exercise 06 – Modify Queue Attributes

Modify:

```mqsc
ALTER QLOCAL(APP.REQUEST)
MAXDEPTH(10000)
DEFPSIST(YES)
```

Verify:

```mqsc
DISPLAY QLOCAL(APP.REQUEST)
MAXDEPTH
DEFPSIST
```

Questions:

1. What does MAXDEPTH control?
2. What is the purpose of DEFPSIST?

---

# Exercise 07 – Monitor Queue Status

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

Discussion:

* What does CURDEPTH represent?
* What do IPPROCS and OPPROCS indicate?

---

# Exercise 08 – Monitor Queue Activity

Display:

```mqsc
DISPLAY QSTATUS(APP.REQUEST)
LPUTDATE
LPUTTIME
LGETDATE
LGETTIME
```

Questions:

1. When was the last message put?
2. When was the last message retrieved?
3. How can this information assist troubleshooting?

---

# Exercise 09 – Queue Capacity Planning

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

Why should administrators monitor queue growth trends?

---

# Exercise 10 – Queue Full Scenario

Research:

```text
MQRC 2053
```

Discussion:

1. What causes Queue Full conditions?
2. How should administrators respond?
3. What preventive measures can be implemented?

---

# Exercise 11 – Clean Up Objects

Delete:

```mqsc
DELETE QALIAS(APP.INPUT)
```

Delete:

```mqsc
DELETE QREMOTE(APP.REMOTE)
```

Verify:

```mqsc
DISPLAY QALIAS(APP.INPUT)
DISPLAY QREMOTE(APP.REMOTE)
```

Expected:

```text
Object not found
```

---

# Validation Checklist

Confirm that you can:

* Create Local Queues
* Create Remote Queues
* Create Alias Queues
* Configure a Dead Letter Queue
* Modify Queue Attributes
* Monitor Queue Status
* Monitor Queue Activity
* Interpret Queue Metrics

---

# Challenge Exercise

Research and document:

1. Model Queues
2. Transmission Queues
3. Backout Queues
4. Poison Messages
5. Queue Full Recovery Strategies

---

# Expected Outcome

Upon completion of this lab, students will be able to administer IBM MQ queues, monitor queue activity and apply operational practices commonly required in enterprise messaging environments.

These skills are foundational for supporting production IBM MQ workloads.

---

## Next Lab

Proceed to:

**Lab 04 – Channel Administration**
