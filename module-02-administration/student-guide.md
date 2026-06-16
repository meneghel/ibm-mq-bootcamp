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

The Queue Manager is the central runtime component of IBM MQ.

Every IBM MQ environment is built around one or more Queue Managers.

A Queue Manager is responsible for:

* Message Storage
* Queue Management
* Channel Management
* Logging
* Recovery
* Security Enforcement
* Transaction Coordination

Without a running Queue Manager, applications cannot exchange messages.

---

## Queue Manager Architecture

A Queue Manager consists of several internal components working together.

Typical components include:

* Object Definitions
* Message Storage
* Active Logs
* Archive Logs
* Recovery Information
* Channel Processes
* Listener Processes

Typical location:

```text
/var/mqm/qmgrs/QM1
```

Important subdirectories:

```text
errors/
active/
qm.ini
queues/
ssl/
```

Understanding the Queue Manager directory structure is essential for backup, troubleshooting and recovery activities.

---

## Creating a Queue Manager

Queue Managers are created using the crtmqm command.

Example:

```bash
crtmqm QM1
```

Example Output:

```text
WebSphere MQ queue manager created.
Directory '/var/mqm/qmgrs/QM1' created.
The queue manager is associated with installation 'Installation1'.
```

At this stage the Queue Manager exists but is not yet running.

---

## Starting a Queue Manager

Start the Queue Manager:

```bash
strmqm QM1
```

Expected Result:

```text
IBM MQ queue manager 'QM1' starting.
IBM MQ queue manager 'QM1' started.
```

Verify status:

```bash
dspmq
```

Output:

```text
QMNAME(QM1) STATUS(Running)
```

---

## Queue Manager States

Administrators must understand Queue Manager states.

Common states include:

### Running

Queue Manager is operational.

```text
STATUS(Running)
```

Applications may connect and process messages.

---

### Ended Normally

Queue Manager stopped successfully.

```text
STATUS(Ended normally)
```

No recovery required.

---

### Starting

Queue Manager startup in progress.

```text
STATUS(Starting)
```

---

### Running Elsewhere

Typically seen in HA environments.

```text
STATUS(Running elsewhere)
```

The Queue Manager is active on another node.

---

## Stopping a Queue Manager

### Normal Shutdown

Recommended method.

```bash
endmqm QM1
```

Behavior:

* Waits for applications
* Completes transactions
* Shuts down cleanly

---

### Immediate Shutdown

```bash
endmqm -i QM1
```

Behavior:

* Terminates active applications
* Rolls back uncommitted work
* Faster shutdown

Used during operational emergencies.

---

### Preemptive Shutdown

```bash
endmqm -p QM1
```

Behavior:

* Forcefully terminates Queue Manager processes

Use only when normal methods fail.

---

## Logging and Recovery

IBM MQ maintains transaction logs.

Purpose:

* Recover persistent messages
* Recover Queue Manager state
* Ensure transactional consistency

Log types:

### Active Logs

Used during normal processing.

### Archive Logs

Retained for long-term recovery.

---

## Crash Recovery

If a server crashes unexpectedly:

```text
Power Failure
Operating System Crash
Hardware Failure
```

IBM MQ automatically performs recovery during startup.

Recovery uses transaction logs to restore a consistent state.

This is one of the key reasons IBM MQ is trusted for mission-critical workloads.

---

## Administrative Best Practices

### Use Consistent Naming

Example:

```text
QM.DEV
QM.TEST
QM.PROD
```

---

### Separate Environments

Never share Queue Managers between:

* Development
* Testing
* Production

---

### Monitor Startup and Shutdown Events

Administrators should always review:

```text
/var/mqm/errors
```

after unexpected outages.

---

### Document Queue Managers

Maintain documentation for:

* Purpose
* Owner
* Environment
* Recovery Procedures
* Dependencies

---

## Chapter Summary

You learned:

* Queue Manager architecture
* Queue Manager lifecycle
* Startup and shutdown procedures
* Queue Manager states
* Logging concepts
* Recovery fundamentals
* Administrative best practices

The Queue Manager is the foundation of every IBM MQ environment and one of the most important components an administrator must understand.

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

Channels are the communication mechanisms used by IBM MQ to exchange messages between Queue Managers and applications.

Without channels, Queue Managers cannot communicate with each other and client applications cannot establish MQ connections.

Channels provide:

* Reliable Communication
* Message Transport
* Network Connectivity
* Security Integration
* Workload Distribution

Understanding channels is one of the most important skills for IBM MQ administrators.

---

## Channel Architecture

A typical distributed messaging flow looks like:

```text
QM1
 |
 | Sender Channel
 |
 XMITQ
 |
 TCP/IP Network
 |
 Receiver Channel
 |
QM2
```

Message Flow:

1. Application puts message
2. Message is stored in a Transmission Queue
3. Sender Channel retrieves message
4. Message travels across the network
5. Receiver Channel receives message
6. Message is stored on the destination Queue Manager

---

## Channel Components

### Sender Channel (SDR)

Responsible for transmitting messages to another Queue Manager.

Characteristics:

* Initiates communication
* Reads messages from XMITQ
* Establishes TCP/IP sessions

Example:

```mqsc
DEFINE CHANNEL(QM1.TO.QM2)
CHLTYPE(SDR)
TRPTYPE(TCP)
XMITQ(QM2.XMITQ)
CONNAME('server2.company.com(1414)')
```

---

### Receiver Channel (RCVR)

Accepts inbound connections from Sender Channels.

Characteristics:

* Receives messages
* Processes incoming traffic
* Runs on destination Queue Manager

Example:

```mqsc
DEFINE CHANNEL(QM1.TO.QM2)
CHLTYPE(RCVR)
TRPTYPE(TCP)
```

---

### Server Connection Channel (SVRCONN)

Used by client applications.

Typical examples:

* Java Applications
* .NET Applications
* MQ Explorer
* Monitoring Tools

Example:

```mqsc
DEFINE CHANNEL(APP.SVRCONN)
CHLTYPE(SVRCONN)
TRPTYPE(TCP)
```

---

### Requester Channel

Used primarily in older MQ architectures.

Requests communication from a Sender Channel.

Less common in modern environments.

---

### Cluster Sender (CLUSSDR)

Used in MQ Clusters.

Responsible for advertising cluster information.

---

### Cluster Receiver (CLUSRCVR)

Receives cluster information from other Queue Managers.

Fundamental component of MQ Clusters.

---

## Transmission Queues

Transmission Queues (XMITQ) temporarily store messages awaiting transmission.

Example:

```mqsc
DEFINE QLOCAL(QM2.XMITQ)
USAGE(XMITQ)
```

Messages accumulate here when:

* Destination unavailable
* Network failure
* Channel stopped

Queue depth growth often indicates communication issues.

---

## Channel States

Administrators should monitor channel status regularly.

---

### RUNNING

Channel operating normally.

```mqsc
DISPLAY CHSTATUS(*)
```

Example:

```text
STATUS(RUNNING)
```

---

### STOPPED

Channel not active.

Example:

```text
STATUS(STOPPED)
```

May require manual intervention.

---

### RETRYING

Channel attempting reconnection.

Example:

```text
STATUS(RETRYING)
```

Common causes:

* Network unavailable
* Listener stopped
* Destination unavailable

---

### INITIALIZING

Channel startup in progress.

---

### BINDING

Channel establishing network resources.

Usually temporary.

---

## Important Channel Attributes

### CONNAME

Defines destination host and port.

Example:

```text
server.company.com(1414)
```

---

### XMITQ

Transmission Queue associated with Sender Channel.

---

### DISCINT

Disconnect Interval.

Defines how long a channel remains connected while idle.

Example:

```mqsc
DISCINT(6000)
```

---

### HBINT

Heartbeat Interval.

Defines heartbeat frequency.

Example:

```mqsc
HBINT(300)
```

---

### BATCHSZ

Maximum number of messages per transmission batch.

Example:

```mqsc
BATCHSZ(50)
```

Higher values improve throughput but increase recovery complexity.

---

## Starting and Stopping Channels

### Start Channel

```mqsc
START CHANNEL(QM1.TO.QM2)
```

---

### Stop Channel

```mqsc
STOP CHANNEL(QM1.TO.QM2)
```

---

## Monitoring Channels

Display Channel Status:

```mqsc
DISPLAY CHSTATUS(*)
```

Display Specific Channel:

```mqsc
DISPLAY CHSTATUS(QM1.TO.QM2)
```

Monitor:

* Status
* Messages Sent
* Messages Received
* Retry Activity
* Connection State

---

## Common Channel Problems

### Messages Stuck in XMITQ

Symptoms:

* Growing Queue Depth
* No message delivery

Potential Causes:

* Channel stopped
* Network outage
* Listener unavailable

---

### MQRC 2059

```text
MQRC_Q_MGR_NOT_AVAILABLE
```

Common causes:

* Queue Manager stopped
* Listener unavailable
* Incorrect connection details

---

### MQRC 2009

```text
MQRC_CONNECTION_BROKEN
```

Common causes:

* Firewall interruption
* Network instability
* TLS issues

---

### Sequence Number Error

Occurs when channel sequence numbers become inconsistent.

Resolution may require:

```mqsc
RESET CHANNEL(...)
```

This should only be performed after proper analysis.

---

## Channel Administration Best Practices

### Use Consistent Naming

Examples:

```text
QM1.TO.QM2
QM2.TO.QM3
```

---

### Monitor XMITQ Depth

Growing XMITQ depth is often the first sign of communication problems.

---

### Review Retry Activity

Persistent RETRYING states indicate underlying infrastructure issues.

---

### Document Channel Topology

Maintain documentation for:

* Queue Managers
* Channels
* Listeners
* Network Ports
* Firewall Rules

---

## Chapter Summary

You learned:

* Channel Architecture
* Channel Types
* Transmission Queues
* Channel States
* Channel Attributes
* Monitoring Techniques
* Common Failures
* Administrative Best Practices

Channel administration is one of the most critical responsibilities of an IBM MQ Administrator and a foundational skill for troubleshooting distributed messaging environments.

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
