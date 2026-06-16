# IBM MQ Bootcamp

# Module 02 – Administration & Operations

# Lab 01 – Queue Manager Lifecycle

---

## Lab Overview

The Queue Manager is the core runtime component of IBM MQ.

Every queue, channel, listener and message ultimately depends on the Queue Manager.

In this lab, students will create, start, stop and administer an IBM MQ Queue Manager while becoming familiar with the most common operational commands used by enterprise administrators.

---

## Learning Objectives

By completing this lab, students will be able to:

* Create a Queue Manager
* Start and stop a Queue Manager
* Verify Queue Manager status
* Navigate Queue Manager directories
* Access MQSC
* Display Queue Manager attributes
* Understand Queue Manager lifecycle states

---

## Estimated Duration

30–45 Minutes

---

## Prerequisites

Students should have:

* IBM MQ Installed
* Local Administrative Access
* Linux Command Line Access
* Completion of Module 01 – Fundamentals

---

## Environment

Operating System:

```text
Linux
```

Queue Manager:

```text
QM1
```

---

## Scenario

You have joined the middleware operations team of a large enterprise.

Your first assignment is to deploy and administer a new IBM MQ Queue Manager that will be used by a business-critical application.

Your objective is to create the Queue Manager, verify its status and become familiar with its operational lifecycle.

---

# Exercise 01 – Verify Existing Queue Managers

Display all Queue Managers:

```bash
dspmq
```

Example Output:

```text
QMNAME(QM1) STATUS(Running)
```

Questions:

1. Are any Queue Managers already defined?
2. What status is displayed?
3. Which Queue Manager is currently active?

---

# Exercise 02 – Create a Queue Manager

Create a new Queue Manager:

```bash
crtmqm QM1
```

Expected Output:

```text
WebSphere MQ queue manager created.
Directory '/var/mqm/qmgrs/QM1' created.
```

Questions:

1. Was the Queue Manager successfully created?
2. Is the Queue Manager automatically started?

---

# Exercise 03 – Verify Queue Manager Status

Display Queue Managers again:

```bash
dspmq
```

Expected Result:

```text
QMNAME(QM1) STATUS(Ended normally)
```

Discussion:

Why does IBM MQ create the Queue Manager without automatically starting it?

---

# Exercise 04 – Start the Queue Manager

Start the Queue Manager:

```bash
strmqm QM1
```

Expected Output:

```text
IBM MQ queue manager 'QM1' starting.
IBM MQ queue manager 'QM1' started.
```

Verify:

```bash
dspmq
```

Expected Result:

```text
QMNAME(QM1) STATUS(Running)
```

Questions:

1. What changed after executing the command?
2. Which services became available?

---

# Exercise 05 – Explore Queue Manager Directories

Navigate to the Queue Manager directory:

```bash
cd /var/mqm/qmgrs/QM1
```

Display contents:

```bash
ls -la
```

Review:

```text
errors/
ssl/
qm.ini
```

Discussion:

* What is the purpose of the errors directory?
* What is stored in ssl?
* Why is qm.ini important?

---

# Exercise 06 – Open MQSC

Start MQSC:

```bash
runmqsc QM1
```

Display Queue Manager attributes:

```mqsc
DISPLAY QMGR
```

Review the output.

Identify:

* Queue Manager Name
* Dead Letter Queue
* Logging Configuration
* Command Level

Exit MQSC:

```mqsc
END
```

---

# Exercise 07 – Normal Shutdown

Stop the Queue Manager:

```bash
endmqm QM1
```

Verify:

```bash
dspmq
```

Expected Result:

```text
STATUS(Ended normally)
```

Discussion:

Why is a normal shutdown preferred in production environments?

---

# Exercise 08 – Immediate Shutdown

Start the Queue Manager again:

```bash
strmqm QM1
```

Execute:

```bash
endmqm -i QM1
```

Discussion:

Compare:

```text
endmqm QM1
```

versus

```text
endmqm -i QM1
```

Questions:

* Which is safer?
* Which is faster?
* When should each be used?

---

# Exercise 09 – Queue Manager States

Research and document the meaning of:

```text
Running
Ended normally
Starting
Running elsewhere
```

Discussion:

In which scenarios would an administrator encounter each state?

---

# Validation Checklist

Confirm that you can:

* Create a Queue Manager
* Start a Queue Manager
* Stop a Queue Manager
* Access MQSC
* Display Queue Manager attributes
* Locate Queue Manager files
* Interpret Queue Manager states

---

# Challenge Exercise

Research the following topics and prepare a brief explanation:

1. Active Logs
2. Archive Logs
3. Crash Recovery
4. Immediate Shutdown
5. Preemptive Shutdown

---

# Expected Outcome

Upon completion of this lab, students will understand the Queue Manager lifecycle and will be capable of performing the most common operational tasks required by IBM MQ administrators.

This knowledge serves as the foundation for all subsequent administration activities throughout the bootcamp.

---

## Next Lab

Proceed to:

**Lab 02 – MQSC Fundamentals**
