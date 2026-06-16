# IBM MQ Bootcamp

# Module 02 – Administration & Operations

# Lab 02 – MQSC Fundamentals

---

## Lab Overview

MQSC (MQ Script Commands) is the primary administration interface for IBM MQ.

Most operational, administrative and troubleshooting activities performed by IBM MQ administrators rely on MQSC commands.

In this lab, students will learn how to use MQSC to display information, create objects, modify configurations and perform common administrative tasks.

---

## Learning Objectives

By completing this lab, students will be able to:

* Access MQSC
* Execute DISPLAY commands
* Create MQ objects using DEFINE
* Modify MQ objects using ALTER
* Remove MQ objects using DELETE
* Start and stop MQ resources
* Understand MQSC command structure
* Validate administrative changes

---

## Estimated Duration

45–60 Minutes

---

## Prerequisites

Students should have completed:

* Module 01 – Fundamentals
* Lab 01 – Queue Manager Lifecycle

Required environment:

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

You have been assigned administrative access to an existing IBM MQ environment.

Your objective is to become familiar with MQSC and perform basic administration tasks required during daily operations.

---

# Exercise 01 – Launch MQSC

Start MQSC:

```bash
runmqsc QM1
```

Expected Output:

```text
Starting MQSC for Queue Manager QM1
```

Questions:

1. What is MQSC?
2. Why do administrators use MQSC instead of graphical tools?

---

# Exercise 02 – Display Queue Manager Information

Execute:

```mqsc
DISPLAY QMGR
```

Review:

* Queue Manager Name
* Dead Letter Queue
* Logging Attributes
* Command Level

Questions:

1. Which Queue Manager are you connected to?
2. What information is displayed?

---

# Exercise 03 – Display Existing Queues

Display all Local Queues:

```mqsc
DISPLAY QLOCAL(*)
```

Display system queues only:

```mqsc
DISPLAY QLOCAL(SYSTEM.*)
```

Questions:

1. How many queues are displayed?
2. Why are system queues important?

---

# Exercise 04 – Create a Local Queue

Create a queue:

```mqsc
DEFINE QLOCAL(APP.INPUT)
```

Verify:

```mqsc
DISPLAY QLOCAL(APP.INPUT)
```

Questions:

1. Was the queue created successfully?
2. Which attributes were assigned by default?

---

# Exercise 05 – Create an Output Queue

Create:

```mqsc
DEFINE QLOCAL(APP.OUTPUT)
```

Verify:

```mqsc
DISPLAY QLOCAL(APP.OUTPUT)
```

---

# Exercise 06 – Modify Queue Attributes

Modify queue depth:

```mqsc
ALTER QLOCAL(APP.INPUT) MAXDEPTH(10000)
```

Verify:

```mqsc
DISPLAY QLOCAL(APP.INPUT) MAXDEPTH
```

Expected Result:

```text
MAXDEPTH(10000)
```

Questions:

1. What does MAXDEPTH control?
2. What happens when a queue reaches its limit?

---

# Exercise 07 – Create a Dead Letter Queue

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

1. Why is a Dead Letter Queue important?
2. What types of messages may end up in the DLQ?

---

# Exercise 08 – Create an Alias Queue

Create:

```mqsc
DEFINE QALIAS(APP.REQUEST) TARGET(APP.INPUT)
```

Verify:

```mqsc
DISPLAY QALIAS(APP.REQUEST)
```

Questions:

1. Why are Alias Queues useful?
2. What benefits do they provide?

---

# Exercise 09 – Start and Stop Resources

Display listeners:

```mqsc
DISPLAY LISTENER(*)
```

Display channels:

```mqsc
DISPLAY CHANNEL(*)
```

Discussion:

* Which resources can be controlled using MQSC?
* Why is operational visibility important?

---

# Exercise 10 – Delete an Object

Delete the Alias Queue:

```mqsc
DELETE QALIAS(APP.REQUEST)
```

Verify:

```mqsc
DISPLAY QALIAS(APP.REQUEST)
```

Expected Result:

```text
Object not found
```

Discussion:

Why should DELETE commands be used carefully in production environments?

---

# Exercise 11 – Exit MQSC

Exit MQSC:

```mqsc
END
```

Verify return to operating system prompt.

---

# Validation Checklist

Confirm that you can:

* Launch MQSC
* Execute DISPLAY commands
* Create Local Queues
* Modify Queue Attributes
* Configure a Dead Letter Queue
* Create Alias Queues
* Delete Objects
* Exit MQSC safely

---

# Challenge Exercise

Research and document:

1. Difference between DEFINE and ALTER
2. Difference between Local, Remote and Alias Queues
3. Purpose of SYSTEM.ADMIN.COMMAND.QUEUE
4. Purpose of Command Server
5. Benefits of MQSC scripting

---

# Expected Outcome

Upon completion of this lab, students will be able to perform basic IBM MQ administration using MQSC and will understand how MQ objects are created, modified and managed within a Queue Manager.

These skills form the foundation for queue administration, channel administration and operational support activities.

---

## Next Lab

Proceed to:

**Lab 03 – Queue Administration**
