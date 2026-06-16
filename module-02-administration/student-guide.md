# IBM MQ Bootcamp - Module 02

# IBM MQ Administration & Operations

## Module Description

This module introduces the operational and administrative responsibilities associated with IBM MQ environments.

Students will learn how to create, start, stop and manage Queue Managers, administer MQ objects, configure communication components and perform common operational tasks required in enterprise environments.

This module establishes the foundation required for security, troubleshooting, high availability and modernization topics covered later in the bootcamp.

---

## Learning Objectives

At the end of this module, students will be able to:

* Understand the role of an IBM MQ Administrator
* Manage Queue Manager lifecycles
* Use MQSC to administer MQ environments
* Create and manage MQ objects
* Configure Channels and Listeners
* Understand Service Objects
* Monitor Queue Managers and Queues
* Perform basic backup and recovery activities
* Execute common operational procedures
* Apply administrative best practices

---

# Chapter 01 - IBM MQ Administration Overview

## The Role of the MQ Administrator

IBM MQ Administrators are responsible for ensuring that messaging environments remain available, secure and operational.

Typical responsibilities include:

* Queue Manager Administration
* Object Management
* Monitoring
* Troubleshooting
* Capacity Planning
* Security Administration
* Operational Support

MQ Administrators often work closely with:

* Application Teams
* Infrastructure Teams
* Security Teams
* Enterprise Architects

---

## Enterprise MQ Environments

A typical enterprise environment may contain:

* Development
* Testing
* Staging
* Production

Each environment should be managed independently following change control procedures.

---

# Chapter 02 - Queue Manager Lifecycle

## What Is a Queue Manager?

A Queue Manager is the central runtime component of IBM MQ.

It is responsible for:

* Managing Queues
* Managing Channels
* Storing Messages
* Processing Transactions
* Maintaining Logs
* Recovery Operations

---

## Creating a Queue Manager

Example:

```bash
crtmqm QM1
```

This command creates a new Queue Manager named QM1.

---

## Starting a Queue Manager

```bash
strmqm QM1
```

---

## Stopping a Queue Manager

```bash
endmqm QM1
```

For immediate shutdown:

```bash
endmqm -i QM1
```

---

## Displaying Queue Manager Status

```bash
dspmq
```

Example Output:

```text
QMNAME(QM1) STATUS(Running)
```

---

# Chapter 03 - MQSC Fundamentals

## What Is MQSC?

MQSC (MQ Script Commands) is the primary administrative language used to configure IBM MQ environments.

MQSC provides a command-based interface for:

* Creating Objects
* Modifying Objects
* Displaying Configuration
* Monitoring Resources

---

## Starting MQSC

```bash
runmqsc QM1
```

---

## Display Queue Manager Information

```mqsc
DISPLAY QMGR
```

---

## Display Queues

```mqsc
DISPLAY QLOCAL(*)
```

---

## Display Channels

```mqsc
DISPLAY CHANNEL(*)
```

---

# Chapter 04 - Queue Administration

## Local Queues

Used to store messages locally.

Example:

```mqsc
DEFINE QLOCAL(APP.INPUT)
```

---

## Remote Queues

Represent destinations hosted by another Queue Manager.

Example:

```mqsc
DEFINE QREMOTE(APP.REMOTE)
```

---

## Alias Queues

Provide alternate names for existing queues.

Example:

```mqsc
DEFINE QALIAS(APP.ALIAS)
```

---

## Dead Letter Queue

Stores messages that cannot be delivered.

Example:

```mqsc
ALTER QMGR DEADQ(SYSTEM.DEAD.LETTER.QUEUE)
```

---

# Chapter 05 - Channel Administration

## What Is a Channel?

Channels provide communication paths between Queue Managers or client applications.

Without channels, Queue Managers cannot exchange messages.

---

## Channel Types

Common types include:

* Sender (SDR)
* Receiver (RCVR)
* Server Connection (SVRCONN)
* Requester
* Cluster Sender
* Cluster Receiver

---

## Create a Sender Channel

Example:

```mqsc
DEFINE CHANNEL(QM1.TO.QM2) CHLTYPE(SDR) TRPTYPE(TCP)
```

---

## Display Channel Status

```mqsc
DISPLAY CHSTATUS(*)
```

---

# Chapter 06 - Listener Administration

## What Is a Listener?

Listeners accept inbound TCP/IP connections for IBM MQ.

They enable channels and clients to establish network communications.

---

## Create a Listener

```mqsc
DEFINE LISTENER(LISTENER.TCP)
TRPTYPE(TCP)
PORT(1414)
CONTROL(QMGR)
```

---

## Start Listener

```mqsc
START LISTENER(LISTENER.TCP)
```

---

## Display Listener Status

```mqsc
DISPLAY LSSTATUS(*)
```

---

# Chapter 07 - Service Objects

## What Is a Service Object?

Service Objects allow IBM MQ to automatically start and manage operating system processes.

Typical use cases include:

* Trigger Monitors
* Custom Services
* Automation Scripts

---

## Service Example

```mqsc
DEFINE SERVICE(MY.SERVICE)
```

---

# Chapter 08 - Monitoring Fundamentals

## Why Monitoring Matters

Monitoring helps prevent outages and capacity issues.

Common monitoring activities include:

* Queue Depth Analysis
* Channel Status Monitoring
* Queue Manager Availability
* Error Log Review

---

## Queue Depth

Display Queue Status:

```mqsc
DISPLAY QSTATUS(APP.INPUT)
```

---

## Channel Status

```mqsc
DISPLAY CHSTATUS(*)
```

---

## Error Logs

Common log location:

```text
/var/mqm/errors
```

---

# Chapter 09 - Backup and Configuration Management

## Backup Objectives

Protect:

* Queue Manager Configuration
* MQSC Definitions
* Operational Procedures

---

## Export MQSC Definitions

Example:

```bash
runmqsc QM1 < backup.mqsc
```

---

## Change Control

Best practices:

* Version control MQSC scripts
* Document changes
* Use approval workflows

---

# Chapter 10 - Common Operational Tasks

Daily activities include:

* Create Queue
* Delete Queue
* Start Channel
* Stop Channel
* Start Listener
* Stop Listener
* Check Queue Depth
* Review Logs

---

## Example

Display Queue Depth:

```mqsc
DISPLAY QLOCAL(APP.INPUT) CURDEPTH
```

---

# Chapter 11 - Operational Best Practices

## Naming Standards

Examples:

```text
APP.INPUT
APP.OUTPUT
APP.ERROR
```

---

## Environment Separation

Maintain clear separation between:

* DEV
* TEST
* QA
* PROD

---

## Monitoring Standards

Monitor:

* Queue Depth
* Channel Status
* Error Logs
* Queue Manager Availability

---

## Documentation

Document:

* Queue Definitions
* Channel Definitions
* Listener Configuration
* Operational Procedures

---

# Chapter 12 - Module Summary

In this module, you learned:

* Queue Manager Administration
* MQSC Fundamentals
* Queue Administration
* Channel Administration
* Listener Administration
* Service Objects
* Monitoring Fundamentals
* Backup Concepts
* Operational Procedures
* Administrative Best Practices

You are now able to perform the most common IBM MQ administrative tasks and are prepared to continue with security and troubleshooting topics.

---

# Next Step

Proceed to:

Lab 01 - Queue Manager Lifecycle
