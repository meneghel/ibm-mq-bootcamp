# IBM MQ Bootcamp

# Module 02 – Administration & Operations

# Exercises

---

## Overview

These exercises are designed to reinforce the concepts presented throughout Module 02.

Students should complete the exercises after studying the Student Guide and completing the associated hands-on labs.

---

# Section 01 – Queue Manager Lifecycle

## Exercise 1

What is the primary responsibility of an IBM MQ Queue Manager?

A. Store application source code

B. Manage messaging resources and message delivery

C. Manage operating system users

D. Manage network routing

---

## Exercise 2

Which command creates a Queue Manager?

A.

```bash
strmqm
```

B.

```bash
crtmqm
```

C.

```bash
dspmq
```

D.

```bash
runmqsc
```

---

## Exercise 3

What Queue Manager status indicates a successful shutdown?

A. Running

B. Starting

C. Ended Normally

D. Retrying

---

# Section 02 – MQSC Fundamentals

## Exercise 4

What does MQSC stand for?

---

## Exercise 5

Which MQSC command displays Queue Manager information?

---

## Exercise 6

What is the difference between:

```text
DEFINE
```

and

```text
ALTER
```

---

# Section 03 – Queue Administration

## Exercise 7

Match the Queue Type to its purpose.

| Queue Type        | Purpose |
| ----------------- | ------- |
| Local Queue       | ?       |
| Remote Queue      | ?       |
| Alias Queue       | ?       |
| Dead Letter Queue | ?       |

---

## Exercise 8

What does CURDEPTH represent?

A. Queue Size Limit

B. Number of Messages Currently Stored

C. Number of Consumers

D. Queue Creation Date

---

## Exercise 9

Why is a Dead Letter Queue important?

---

# Section 04 – Channel Administration

## Exercise 10

What is the purpose of a Transmission Queue?

---

## Exercise 11

What channel type is used by client applications?

A. SDR

B. RCVR

C. SVRCONN

D. CLUSRCVR

---

## Exercise 12

What does a channel status of RETRYING usually indicate?

---

# Section 05 – Listener Administration

## Exercise 13

What is the default IBM MQ TCP port?

A. 8080

B. 9443

C. 1414

D. 5000

---

## Exercise 14

What is the role of a Listener?

---

## Exercise 15

What is the difference between:

```text
CONTROL(QMGR)
```

and

```text
CONTROL(MANUAL)
```

---

# Section 06 – Monitoring & Operations

## Exercise 16

Which command displays Queue Status?

---

## Exercise 17

What does CHSTATUS provide?

---

## Exercise 18

What is an FDC file?

---

# Section 07 – Backup & Configuration Management

## Exercise 19

What utility exports MQ object definitions?

A. saveqmgr

B. crtmqm

C. dspmq

D. strmqm

---

## Exercise 20

What does RTO mean?

---

## Exercise 21

What does RPO mean?

---

# Scenario-Based Exercises

## Exercise 22

A queue depth is growing continuously.

What possible issues should an administrator investigate?

List at least three.

---

## Exercise 23

A channel remains in RETRYING status.

What troubleshooting steps would you perform?

---

## Exercise 24

An application reports MQRC 2059.

List possible causes.

---

## Exercise 25

A Queue Manager must be rebuilt after a server failure.

Which configuration artifacts would be required?

---

# Knowledge Check

Rate your confidence in the following areas:

| Topic             | Beginner | Intermediate | Advanced |
| ----------------- | -------- | ------------ | -------- |
| Queue Managers    | ☐        | ☐            | ☐        |
| MQSC              | ☐        | ☐            | ☐        |
| Queues            | ☐        | ☐            | ☐        |
| Channels          | ☐        | ☐            | ☐        |
| Listeners         | ☐        | ☐            | ☐        |
| Monitoring        | ☐        | ☐            | ☐        |
| Backup & Recovery | ☐        | ☐            | ☐        |

---

## Expected Outcome

Students should be able to explain the operational responsibilities of an IBM MQ Administrator and demonstrate understanding of the administration concepts covered throughout Module 02.
