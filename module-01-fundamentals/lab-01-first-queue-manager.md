# IBM MQ Bootcamp

# Lab 01 – First Queue Manager

## Lab Overview

In this lab, students will create their first IBM MQ environment and perform basic messaging operations.

This lab reinforces the concepts introduced in Module 01 and provides hands-on experience with:

* Queue Managers
* Queues
* Messages
* MQSC Commands
* Message PUT and GET Operations

---

# Learning Objectives

At the end of this lab, students will be able to:

* Create an IBM MQ Queue Manager
* Start and stop a Queue Manager
* Create Local Queues
* Put messages into a queue
* Retrieve messages from a queue
* Verify queue depth
* Understand basic Queue Manager administration

---

# Lab Environment

## Option 1 – IBM MQ Container

Recommended environment:

```bash
docker run -d \
--name mq \
-p 1414:1414 \
-p 9443:9443 \
-e LICENSE=accept \
-e MQ_QMGR_NAME=QM1 \
ibmcom/mq
```

Verify container status:

```bash
docker ps
```

Expected output:

```text
mq   Up
```

---

# Accessing the Container

Open a shell session:

```bash
docker exec -it mq bash
```

Switch to MQ administration user:

```bash
su - mqm
```

---

# Exercise 01 – Verify Queue Manager

Display Queue Managers:

```bash
dspmq
```

Expected output:

```text
QMNAME(QM1) STATUS(Running)
```

Discussion:

What is the role of a Queue Manager?

---

# Exercise 02 – Create a Local Queue

Open MQSC:

```bash
runmqsc QM1
```

Create a Local Queue:

```mqsc
DEFINE QLOCAL(DEMO.Q)
```

Expected output:

```text
AMQ8006I:
IBM MQ queue created.
```

Verify queue:

```mqsc
DISPLAY QLOCAL(DEMO.Q)
```

Exit MQSC:

```mqsc
END
```

---

# Exercise 03 – Put a Message

Use the sample utility:

```bash
amqsput DEMO.Q QM1
```

Enter:

```text
Hello IBM MQ
```

Press Enter.

Terminate with:

```text
(blank line)
```

Expected Result:

Message successfully stored.

---

# Exercise 04 – Verify Queue Depth

Open MQSC:

```bash
runmqsc QM1
```

Execute:

```mqsc
DISPLAY QLOCAL(DEMO.Q) CURDEPTH
```

Expected output:

```text
CURDEPTH(1)
```

Discussion:

Why is queue depth important?

---

# Exercise 05 – Retrieve a Message

Execute:

```bash
amqsget DEMO.Q QM1
```

Expected output:

```text
Hello IBM MQ
```

Verify queue depth again:

```mqsc
DISPLAY QLOCAL(DEMO.Q) CURDEPTH
```

Expected output:

```text
CURDEPTH(0)
```

---

# Exercise 06 – Create Additional Messages

Put multiple messages:

```bash
amqsput DEMO.Q QM1
```

Messages:

```text
Message 1
Message 2
Message 3
```

Verify:

```mqsc
DISPLAY QLOCAL(DEMO.Q) CURDEPTH
```

Expected:

```text
CURDEPTH(3)
```

---

# Exercise 07 – Review MQ Objects

Display all Local Queues:

```mqsc
DISPLAY QLOCAL(*)
```

Questions:

* Which queues exist by default?
* Why are system queues important?

---

# Exercise 08 – Stop Queue Manager

Stop Queue Manager:

```bash
endmqm QM1
```

Verify:

```bash
dspmq
```

Expected:

```text
STATUS(Ended normally)
```

Restart:

```bash
strmqm QM1
```

Verify:

```bash
dspmq
```

Expected:

```text
STATUS(Running)
```

---

# Troubleshooting Section

## Queue Does Not Exist

Error:

```text
2085 MQRC_UNKNOWN_OBJECT_NAME
```

Cause:

Queue name is incorrect.

Resolution:

Verify queue definition.

---

## Queue Manager Not Running

Error:

```text
2059 MQRC_Q_MGR_NOT_AVAILABLE
```

Cause:

Queue Manager is stopped.

Resolution:

```bash
strmqm QM1
```

---

## Permission Issues

Error:

```text
2035 MQRC_NOT_AUTHORIZED
```

Cause:

User lacks required permissions.

Resolution:

Review MQ authorization configuration.

---

# Lab Challenge

Create:

```text
ORDERS.Q
PAYMENTS.Q
CUSTOMERS.Q
```

For each queue:

1. Create queue
2. Put message
3. Verify depth
4. Retrieve message

Document results.

---

# Expected Outcomes

Students should be able to:

* Create Queue Managers
* Create Queues
* Put Messages
* Get Messages
* Verify Queue Depth
* Troubleshoot common issues

---

# Lab Completion

Congratulations.

You have successfully created and administered your first IBM MQ environment.

You are now ready for:

Module 02 – IBM MQ Administration & Operations
