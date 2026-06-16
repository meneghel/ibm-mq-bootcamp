# IBM MQ Bootcamp

# Module 02 – Administration & Operations

# Assessment

---

## Assessment Overview

This assessment evaluates the student's understanding of IBM MQ administration and operational concepts covered throughout Module 02.

Topics include:

* Queue Manager Administration
* MQSC Fundamentals
* Queue Administration
* Channel Administration
* Listener Administration
* Monitoring & Operations
* Backup & Configuration Management

---

## Assessment Information

Passing Score:

```text
70%
```

Recommended Time:

```text
45 Minutes
```

Total Questions:

```text
30
```

---

# Section 01 – Queue Manager Administration

## Question 1

What is the primary responsibility of an IBM MQ Queue Manager?

A. Store application source code

B. Manage messaging resources and message delivery

C. Manage operating system users

D. Manage TCP routing

---

## Question 2

Which command starts a Queue Manager?

A. crtmqm

B. dspmq

C. strmqm

D. runmqsc

---

## Question 3

Which Queue Manager status indicates a clean shutdown?

A. Running

B. Starting

C. Ended Normally

D. Retrying

---

## Question 4

Which directory commonly contains Queue Manager error logs?

A. /var/log

B. /tmp

C. /var/mqm/errors

D. /mq/data

---

# Section 02 – MQSC Fundamentals

## Question 5

What does MQSC stand for?

A. MQ Service Commands

B. MQ Script Commands

C. MQ System Control

D. MQ Secure Commands

---

## Question 6

Which MQSC command displays Queue Manager information?

A.

```mqsc
DISPLAY QMGR
```

B.

```mqsc
SHOW QMGR
```

C.

```mqsc
LIST QMGR
```

D.

```mqsc
STATUS QMGR
```

---

## Question 7

Which command modifies an existing MQ object?

A. DEFINE

B. ALTER

C. DISPLAY

D. DELETE

---

## Question 8

Which command removes an MQ object?

A. REMOVE

B. ERASE

C. DELETE

D. DROP

---

# Section 03 – Queue Administration

## Question 9

Which queue type stores messages locally?

A. Remote Queue

B. Alias Queue

C. Local Queue

D. Cluster Queue

---

## Question 10

What does CURDEPTH represent?

A. Maximum queue depth

B. Current number of messages

C. Queue creation date

D. Number of consumers

---

## Question 11

What is the primary purpose of a Dead Letter Queue?

A. Archive messages

B. Store undeliverable messages

C. Store backups

D. Store logs

---

## Question 12

Which queue type provides an alternate name for another queue?

A. Remote Queue

B. Alias Queue

C. Transmission Queue

D. Model Queue

---

# Section 04 – Channel Administration

## Question 13

What is the purpose of a Transmission Queue?

A. Store logs

B. Store messages awaiting transfer

C. Store certificates

D. Store commands

---

## Question 14

Which channel type is used by MQ client applications?

A. SDR

B. RCVR

C. SVRCONN

D. CLUSSDR

---

## Question 15

What does a channel status of RETRYING usually indicate?

A. Healthy communication

B. Communication failure

C. High performance

D. Queue overflow

---

## Question 16

Which attribute defines the remote host and port?

A. TRPTYPE

B. CONNAME

C. XMITQ

D. MAXMSGL

---

# Section 05 – Listener Administration

## Question 17

What is the default IBM MQ TCP port?

A. 8080

B. 9443

C. 1414

D. 5000

---

## Question 18

What is the purpose of a Listener?

A. Accept inbound connections

B. Store messages

C. Manage security

D. Manage transactions

---

## Question 19

Which Listener control mode automatically starts with the Queue Manager?

A. CONTROL(MANUAL)

B. CONTROL(QMGR)

C. CONTROL(AUTO)

D. CONTROL(START)

---

## Question 20

What MQRC is commonly associated with unavailable Queue Managers?

A. 2009

B. 2035

C. 2053

D. 2059

---

# Section 06 – Monitoring & Operations

## Question 21

Which MQSC command displays Queue Status?

A. DISPLAY QLOCAL

B. DISPLAY QSTATUS

C. DISPLAY QDEPTH

D. DISPLAY STATUS

---

## Question 22

What does CHSTATUS display?

A. Queue Depth

B. Channel Status

C. Queue Manager Status

D. Listener Status

---

## Question 23

What is an FDC file?

A. Backup File

B. Configuration File

C. First Failure Data Capture File

D. Queue Definition File

---

## Question 24

Which operational indicator should be monitored for queue growth?

A. CURDEPTH

B. MAXMSGL

C. SHARE

D. PUT

---

# Section 07 – Backup & Configuration Management

## Question 25

Which utility exports MQ object definitions?

A. saveqmgr

B. strmqm

C. dspmq

D. endmqm

---

## Question 26

What does RTO mean?

A. Recovery Time Objective

B. Recovery Transfer Objective

C. Restore Time Option

D. Runtime Transfer Operation

---

## Question 27

What does RPO mean?

A. Recovery Point Objective

B. Runtime Protection Option

C. Recovery Port Objective

D. Restore Process Operation

---

## Question 28

Why should MQ configuration be version controlled?

A. Improve performance

B. Reduce storage usage

C. Track and manage changes

D. Increase queue depth

---

# Scenario-Based Questions

## Question 29

A queue depth continues to increase while no messages are being consumed.

List three possible causes.

---

## Question 30

A channel remains in RETRYING status for an extended period.

Describe the troubleshooting steps you would perform.

---

# Assessment Results

| Score     | Result                   |
| --------- | ------------------------ |
| 90–100%   | Excellent                |
| 80–89%    | Very Good                |
| 70–79%    | Pass                     |
| Below 70% | Review Module and Retake |

---

# Module Completion

Students who successfully complete this assessment should demonstrate foundational IBM MQ administration skills and be prepared to continue with:

Module 03 – Security
