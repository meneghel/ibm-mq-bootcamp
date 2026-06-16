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

MQSC (MQ Script Commands) is the primary administrative language used to configure, manage and monitor IBM MQ environments.

MQSC is the command-line interface used by administrators to perform almost every operational activity within IBM MQ.

Using MQSC, administrators can:

* Create Objects
* Modify Objects
* Delete Objects
* Monitor Resources
* Configure Communication Components
* Start and Stop Services
* Troubleshoot Operational Issues

MQSC remains one of the most important skills for IBM MQ administrators.

---

## Why MQSC Matters

Even when graphical tools are available, most enterprise environments rely heavily on MQSC.

Reasons include:

* Automation
* Scripting
* Configuration Management
* Infrastructure as Code
* Disaster Recovery
* Change Control

MQSC scripts are commonly stored in version control repositories and used as part of deployment pipelines.

---

## Starting MQSC

Interactive mode:

```bash id="rt3m55"
runmqsc QM1
```

Example:

```text id="ykh92w"
5724-H72 (C) Copyright IBM Corp.
Starting MQSC for Queue Manager QM1
```

Exit MQSC:

```mqsc id="v0rj2y"
END
```

---

## MQSC Command Structure

Most commands follow a simple pattern:

```mqsc id="g8yhlf"
VERB OBJECT ATTRIBUTES
```

Examples:

```mqsc id="jw3s4d"
DISPLAY QMGR
DEFINE QLOCAL(APP.INPUT)
ALTER QLOCAL(APP.INPUT)
DELETE QLOCAL(APP.INPUT)
```

Common verbs:

* DISPLAY
* DEFINE
* ALTER
* DELETE
* START
* STOP
* RESET

---

## DISPLAY Commands

DISPLAY commands are used to retrieve information.

Example:

```mqsc id="szshl4"
DISPLAY QMGR
```

Displays Queue Manager attributes.

---

Display all Local Queues:

```mqsc id="m7yn8m"
DISPLAY QLOCAL(*)
```

---

Display all Channels:

```mqsc id="z2hdyu"
DISPLAY CHANNEL(*)
```

---

Display Queue Status:

```mqsc id="s7fx7k"
DISPLAY QSTATUS(APP.INPUT)
```

DISPLAY commands are among the most frequently used commands in production environments.

---

## DEFINE Commands

DEFINE commands create new objects.

Example:

```mqsc id="0t0uyn"
DEFINE QLOCAL(APP.INPUT)
```

Create a Remote Queue:

```mqsc id="rw7l6m"
DEFINE QREMOTE(APP.REMOTE)
```

Create a Channel:

```mqsc id="gjv31o"
DEFINE CHANNEL(QM1.TO.QM2)
CHLTYPE(SDR)
TRPTYPE(TCP)
```

---

## ALTER Commands

ALTER commands modify existing objects.

Example:

```mqsc id="x9s0yd"
ALTER QLOCAL(APP.INPUT)
MAXDEPTH(10000)
```

Example:

```mqsc id="fhhb6j"
ALTER CHANNEL(QM1.TO.QM2)
HBINT(300)
```

Administrators frequently use ALTER commands to adjust operational parameters.

---

## DELETE Commands

DELETE commands remove objects.

Example:

```mqsc id="f6xg5m"
DELETE QLOCAL(APP.INPUT)
```

Important:

Objects should only be deleted after impact analysis and approval procedures.

---

## START Commands

Used to start resources.

Examples:

```mqsc id="y8ozm5"
START CHANNEL(QM1.TO.QM2)
```

```mqsc id="dkmn7j"
START LISTENER(LISTENER.TCP)
```

---

## STOP Commands

Used to stop resources.

Examples:

```mqsc id="1z79hq"
STOP CHANNEL(QM1.TO.QM2)
```

```mqsc id="m3t6in"
STOP LISTENER(LISTENER.TCP)
```

---

## RESET Commands

RESET commands recover or reset operational resources.

Example:

```mqsc id="f8b7mz"
RESET CHANNEL(QM1.TO.QM2)
```

RESET commands should be used carefully because they may impact message delivery.

---

## MQSC Batch Mode

MQSC commands can be executed from files.

Example:

Create file:

```text id="rr6v2x"
create-queues.mqsc
```

Content:

```mqsc id="mkgj6p"
DEFINE QLOCAL(APP.INPUT)
DEFINE QLOCAL(APP.OUTPUT)
```

Execute:

```bash id="xv0x33"
runmqsc QM1 < create-queues.mqsc
```

Benefits:

* Automation
* Repeatability
* Version Control

---

## Command Server

Many MQSC operations are processed through the Command Server.

The Command Server receives administrative requests and executes them against the Queue Manager.

Important queue:

```text id="f0oxmw"
SYSTEM.ADMIN.COMMAND.QUEUE
```

Administrators should verify the Command Server is running.

Display status:

```bash id="pqhs8w"
dspmqcsv QM1
```

---

## Exporting Configuration

Configuration export is essential for backup and recovery.

Common tools:

### saveqmgr

Exports MQ object definitions.

Example:

```bash id="j2gn5w"
saveqmgr -m QM1
```

---

### dmpmqcfg

Exports MQ configuration in MQSC format.

Example:

```bash id="lmbf39"
dmpmqcfg -m QM1
```

Benefits:

* Backup
* Migration
* Disaster Recovery

---

## Common MQSC Errors

### Object Already Exists

Example:

```text id="1txmkh"
AMQ8146
```

Cause:

Attempting to create an existing object.

---

### Unknown Object

Example:

```text id="fjlwmr"
2085 MQRC_UNKNOWN_OBJECT_NAME
```

Cause:

Object name incorrect.

---

### Not Authorized

Example:

```text id="5s0vha"
2035 MQRC_NOT_AUTHORIZED
```

Cause:

Insufficient permissions.

---

## MQSC Best Practices

### Use Scripts

Avoid manual configuration whenever possible.

---

### Version Control

Store MQSC scripts in Git repositories.

---

### Use Naming Standards

Maintain consistency across environments.

---

### Test Before Production

Always validate MQSC scripts in lower environments.

---

### Document Changes

Maintain operational change history.

---

## Administrative Checklist

Daily MQSC activities often include:

* DISPLAY QMGR
* DISPLAY QSTATUS
* DISPLAY CHSTATUS
* START CHANNEL
* STOP CHANNEL
* ALTER QLOCAL
* Review Error Logs

MQSC is the primary interface used by administrators to operate IBM MQ environments.

---

## Chapter Summary

You learned:

* MQSC Fundamentals
* Command Structure
* DISPLAY Commands
* DEFINE Commands
* ALTER Commands
* DELETE Commands
* START and STOP Commands
* RESET Commands
* Batch Execution
* Command Server
* Configuration Export
* Administrative Best Practices

MQSC is one of the most important skills for IBM MQ administrators and serves as the foundation for automation, operations and infrastructure management.

---

# Chapter 04 - Queue Administration

## Introduction

Queues are the fundamental storage mechanism of IBM MQ.

Every message processed by IBM MQ passes through one or more queues.

Because of this, queue administration is one of the most important responsibilities of an IBM MQ Administrator.

A poorly configured queue can lead to:

* Message Loss
* Processing Delays
* Capacity Issues
* Application Failures
* Performance Problems

Administrators must understand not only queue types but also operational attributes, monitoring techniques and capacity management practices.

---

## Queue Types

IBM MQ provides several queue types designed for different purposes.

---

### Local Queue

A Local Queue stores messages managed by the local Queue Manager.

Example:

```mqsc
DEFINE QLOCAL(APP.INPUT)
```

Typical use cases:

* Application Input
* Application Output
* Request Queues
* Reply Queues

---

### Remote Queue

A Remote Queue represents a queue located on another Queue Manager.

Example:

```mqsc
DEFINE QREMOTE(ORDERS.REMOTE)
RNAME(ORDERS.INPUT)
RQMNAME(QM2)
XMITQ(QM2.XMITQ)
```

Benefits:

* Location transparency
* Simplified application design

---

### Alias Queue

Provides an alternative name for another queue.

Example:

```mqsc
DEFINE QALIAS(ORDERS)
TARGET(ORDERS.INPUT)
```

Benefits:

* Decoupling
* Easier application migration
* Administrative flexibility

---

### Model Queue

Used as a template for dynamically created queues.

Example:

```mqsc
DEFINE QMODEL(APP.MODEL)
```

Commonly used in:

* Request/Reply Patterns
* Dynamic Reply Queues

---

### Transmission Queue

Stores messages waiting to be transmitted to another Queue Manager.

Example:

```mqsc
DEFINE QLOCAL(QM2.XMITQ)
USAGE(XMITQ)
```

Transmission Queues are critical for distributed messaging environments.

---

### Dead Letter Queue

Stores messages that cannot be delivered.

Example:

```mqsc
ALTER QMGR DEADQ(SYSTEM.DEAD.LETTER.QUEUE)
```

Common reasons messages arrive in the DLQ:

* Destination Queue Missing
* Queue Full
* Authorization Failure
* Routing Problems

---

## Queue Attributes

Queue attributes control behavior and performance.

Administrators should understand the most important attributes.

---

### MAXDEPTH

Maximum number of messages allowed.

Example:

```mqsc
DISPLAY QLOCAL(APP.INPUT) MAXDEPTH
```

Typical values:

```text
5000
10000
50000
```

---

### MAXMSGL

Maximum message size.

Example:

```mqsc
DISPLAY QLOCAL(APP.INPUT) MAXMSGL
```

Large message limits may impact performance and storage consumption.

---

### DEFPSIST

Default persistence behavior.

Values:

```text
YES
NO
```

Persistent messages survive Queue Manager failures.

---

### PUT

Controls whether applications can place messages.

Example:

```text
PUT(ENABLED)
PUT(DISABLED)
```

---

### GET

Controls whether applications can retrieve messages.

Example:

```text
GET(ENABLED)
GET(DISABLED)
```

---

### BOTHRESH

Backout Threshold.

Defines how many processing failures may occur before a message is redirected.

Commonly used with:

```text
Backout Queue
Poison Message Handling
```

---

## Queue Monitoring

Monitoring queues is a daily administrative activity.

---

### Current Queue Depth

Displays current message count.

```mqsc
DISPLAY QSTATUS(APP.INPUT) CURDEPTH
```

Example:

```text
CURDEPTH(150)
```

---

### Open Input Processes

Displays active consumers.

```mqsc
DISPLAY QSTATUS(APP.INPUT) IPPROCS
```

---

### Open Output Processes

Displays active producers.

```mqsc
DISPLAY QSTATUS(APP.INPUT) OPPROCS
```

---

### Last Put Date

Displays last message arrival.

```mqsc
DISPLAY QSTATUS(APP.INPUT) LPUTDATE
```

Useful for detecting inactive applications.

---

### Last Get Date

Displays last message consumption.

```mqsc
DISPLAY QSTATUS(APP.INPUT) LGETDATE
```

Useful for identifying processing delays.

---

## Queue Capacity Management

Administrators should proactively monitor queue growth.

Indicators include:

* Increasing Queue Depth
* Queue Full Conditions
* Slow Consumers
* Application Outages

---

### Queue Full Scenario

Common error:

```text
2053 MQRC_Q_FULL
```

Possible causes:

* Consumer Down
* High Message Volume
* Small MAXDEPTH Value

---

### Slow Consumer Scenario

Symptoms:

```text
CURDEPTH Increasing
IPPROCS Low
OPPROCS High
```

Messages accumulate faster than they are consumed.

---

## Poison Messages

A poison message repeatedly causes application failures.

Example:

```text
Process Message
Fail
Rollback

Process Message
Fail
Rollback
```

Without proper handling, the message remains in the queue indefinitely.

Best practice:

* Configure BOTHRESH
* Configure Backout Queue
* Monitor repeated failures

---

## Queue Administration Best Practices

### Use Naming Standards

Examples:

```text
APP.INPUT
APP.OUTPUT
APP.ERROR
APP.REPLY
```

---

### Monitor Queue Depth

Queue depth growth is often the earliest indicator of a problem.

---

### Configure Dead Letter Queues

Every Queue Manager should have a properly configured DLQ.

---

### Review Queue Utilization

Monitor:

* Message Volume
* Growth Trends
* Peak Utilization

---

### Document Queue Purpose

Maintain documentation describing:

* Queue Owner
* Application
* Message Type
* Retention Requirements

---

## Operational Checklist

Daily queue administration activities:

* Review CURDEPTH
* Review DLQ Activity
* Review Queue Full Events
* Verify Consumer Activity
* Verify Producer Activity
* Review Error Logs

---

## Chapter Summary

You learned:

* Queue Types
* Queue Attributes
* Queue Monitoring
* Capacity Management
* Queue Full Conditions
* Poison Messages
* Administrative Best Practices

Queue administration is one of the most important operational responsibilities within IBM MQ environments and directly impacts reliability, performance and business continuity.

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

## Introduction

Listeners are responsible for accepting inbound TCP/IP connections for IBM MQ.

Without a Listener, remote Queue Managers and client applications cannot establish network communications with IBM MQ.

Listeners are fundamental components in distributed MQ environments and play a critical role in connectivity, availability and troubleshooting.

---

## What Is a Listener?

A Listener is a process that waits for inbound network connections.

When a remote Queue Manager or client application attempts to connect, the Listener accepts the connection and transfers control to the appropriate channel process.

Typical communication flow:

```text
Application
     |
TCP/IP Connection
     |
 Listener
     |
 Channel
     |
 Queue Manager
```

---

## Listener Architecture

A typical MQ Listener operates on a TCP port.

Example:

```text
Queue Manager: QM1
Listener: LISTENER.TCP
Port: 1414
Protocol: TCP/IP
```

When a remote connection arrives:

1. Listener accepts the request
2. Channel process is created
3. Queue Manager processes communication

---

## Creating a Listener

Example:

```mqsc
DEFINE LISTENER(LISTENER.TCP)
TRPTYPE(TCP)
PORT(1414)
CONTROL(QMGR)
```

Attributes:

### TRPTYPE

Transport protocol.

Example:

```text
TCP
```

---

### PORT

Network port used by MQ.

Example:

```text
1414
```

Port 1414 is the default IBM MQ port.

---

### CONTROL

Defines startup behavior.

Values:

```text
QMGR
MANUAL
```

Recommended:

```text
CONTROL(QMGR)
```

Automatically starts when the Queue Manager starts.

---

## Starting a Listener

Example:

```mqsc
START LISTENER(LISTENER.TCP)
```

Verify:

```mqsc
DISPLAY LSSTATUS(*)
```

Expected Output:

```text
STATUS(RUNNING)
```

---

## Stopping a Listener

Example:

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

---

## Listener Status Monitoring

Display all Listeners:

```mqsc
DISPLAY LISTENER(*)
```

Display Listener Status:

```mqsc
DISPLAY LSSTATUS(*)
```

Important attributes:

* STATUS
* PORT
* PID
* STARTDATE
* STARTTIME

---

## Verifying Network Connectivity

Administrators should validate Listener availability.

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

---

## Multiple Listeners

A Queue Manager may support multiple Listeners.

Example:

```text
1414
1415
1416
```

Typical use cases:

* Environment Segregation
* Security Requirements
* Migration Projects

---

## Common Listener Problems

### MQRC 2059

```text
MQRC_Q_MGR_NOT_AVAILABLE
```

Potential causes:

* Queue Manager stopped
* Listener stopped
* Wrong hostname
* Wrong port

---

### Connection Refused

Potential causes:

* Listener not running
* Firewall blocking traffic
* Incorrect port configuration

---

### Port Already In Use

Error occurs when another process already uses the configured port.

Verify:

```bash
netstat -tulpn
```

or

```bash
ss -tulpn
```

---

## Firewall Considerations

Administrators should verify:

* Firewall Rules
* Security Groups
* Network ACLs
* Load Balancers

Common port:

```text
1414
```

---

## Listener Administration Best Practices

### Use CONTROL(QMGR)

Allows automatic startup.

---

### Monitor Listener Availability

Include Listener checks in monitoring platforms.

---

### Document Port Usage

Maintain inventory of:

* Queue Managers
* Ports
* Firewalls
* Dependencies

---

### Verify Connectivity Regularly

Perform periodic connectivity testing.

---

## Chapter Summary

You learned:

* Listener Architecture
* Listener Configuration
* Listener Monitoring
* TCP/IP Connectivity
* Common Listener Failures
* Firewall Considerations
* Administrative Best Practices

Listeners are a critical component of IBM MQ communication and often represent the first area administrators investigate during connectivity incidents.

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

## Introduction

Monitoring is one of the most important responsibilities of an IBM MQ Administrator.

Most production incidents provide warning signs before impacting business operations.

Effective monitoring helps identify:

* Capacity Issues
* Application Failures
* Channel Problems
* Performance Bottlenecks
* Infrastructure Outages

---

## Monitoring Objectives

Administrators should continuously monitor:

* Queue Managers
* Queues
* Channels
* Listeners
* Error Logs
* System Resources

---

## Queue Manager Monitoring

Display Queue Manager Status:

```mqsc
DISPLAY QMSTATUS
```

Useful information:

* Status
* Log Utilization
* Connection Counts

---

## Queue Monitoring

### Current Depth

```mqsc
DISPLAY QSTATUS(APP.INPUT) CURDEPTH
```

Example:

```text
CURDEPTH(150)
```

---

### Input Processes

```mqsc
DISPLAY QSTATUS(APP.INPUT) IPPROCS
```

---

### Output Processes

```mqsc
DISPLAY QSTATUS(APP.INPUT) OPPROCS
```

---

### Last Message Activity

```mqsc
DISPLAY QSTATUS(APP.INPUT)
```

Monitor:

* LPUTDATE
* LPUTTIME
* LGETDATE
* LGETTIME

---

## Queue Depth Monitoring

Queue depth is one of the most important operational indicators.

Warning signs:

```text
CURDEPTH Increasing
Consumers Not Processing
Messages Accumulating
```

Common causes:

* Application Failure
* Slow Consumer
* Infrastructure Issues

---

## Channel Monitoring

Display Channel Status:

```mqsc
DISPLAY CHSTATUS(*)
```

Monitor:

* RUNNING
* RETRYING
* STOPPED

---

## Listener Monitoring

Display:

```mqsc
DISPLAY LSSTATUS(*)
```

Verify:

* Running State
* Listening Port
* Availability

---

## Error Logs

Default location:

```text
/var/mqm/errors
```

Important files:

```text
AMQERR01.LOG
AMQERR02.LOG
AMQERR03.LOG
```

---

## FDC Files

FDC stands for:

```text
First Failure Data Capture
```

Generated when IBM MQ detects unexpected internal conditions.

Location:

```text
/var/mqm/errors
```

FDC files are commonly requested by IBM Support.

---

## Capacity Planning

Administrators should monitor:

* Queue Growth
* Message Volume
* Log Utilization
* Channel Activity

Questions:

* Is workload increasing?
* Is infrastructure sufficient?
* Are queue depths growing?

---

## Monitoring Thresholds

Example:

```text
Queue Depth > 80%
Alert

Queue Depth > 90%
Critical
```

Example:

```text
Channel RETRYING
Alert
```

---

## Common Monitoring Tools

Examples:

* IBM MQ Explorer
* IBM Instana
* IBM Tivoli Monitoring
* Prometheus
* Grafana
* Splunk

---

## Monitoring Best Practices

### Monitor Proactively

Do not wait for users to report issues.

---

### Define Thresholds

Create actionable alerts.

---

### Review Trends

Focus on growth patterns.

---

### Monitor Logs

Review errors regularly.

---

### Automate Monitoring

Integrate MQ with enterprise monitoring platforms.

---

## Chapter Summary

You learned:

* Queue Manager Monitoring
* Queue Monitoring
* Channel Monitoring
* Listener Monitoring
* Error Logs
* FDC Files
* Capacity Planning
* Monitoring Best Practices

Monitoring is one of the most valuable operational disciplines within IBM MQ administration and often determines how quickly incidents can be identified and resolved.

---

# Chapter 09 - Backup and Configuration Management

## Introduction

IBM MQ environments support mission-critical business processes.

Because of this, administrators must implement proper backup, recovery and configuration management procedures.

The goal is not only to recover from failures, but also to ensure configuration consistency, operational stability and business continuity.

A successful backup strategy should protect:

* Queue Manager Configuration
* MQ Objects
* Scripts
* Certificates
* Operational Documentation
* Recovery Procedures

---

## Why Backup Matters

Failures can occur at any time.

Examples include:

* Hardware Failures
* Operating System Corruption
* Human Error
* Storage Failures
* Site Outages
* Security Incidents

Without proper backups, recovery can become extremely difficult and time consuming.

---

## Backup Categories

IBM MQ environments typically require multiple backup types.

### Configuration Backup

Protects:

* Queue Definitions
* Channel Definitions
* Listener Definitions
* Process Definitions
* Service Objects

---

### Queue Manager Backup

Protects:

* Queue Manager Files
* Logs
* Configuration Files

---

### Operating System Backup

Protects:

* MQ Installation
* Scripts
* Automation Components
* SSL Artifacts

---

## Queue Manager Directory Structure

Typical location:

```text id="g9c1yq"
/var/mqm/qmgrs/QM1
```

Important directories:

```text id="tfh8w9"
errors/
ssl/
qm.ini
```

These directories should be included in backup procedures.

---

## Exporting MQ Configuration

Configuration exports are essential for backup and migration activities.

---

### saveqmgr

The saveqmgr utility exports MQ object definitions.

Example:

```bash id="f5j4ko"
saveqmgr -m QM1
```

Example Output:

```text id="h7l4sz"
DEFINE QLOCAL(...)
DEFINE CHANNEL(...)
DEFINE LISTENER(...)
```

Benefits:

* Object Backup
* Migration Support
* Documentation

---

### dmpmqcfg

The dmpmqcfg utility exports MQ configuration in MQSC format.

Example:

```bash id="up7i1v"
dmpmqcfg -m QM1
```

Export to file:

```bash id="5txv9y"
dmpmqcfg -m QM1 > QM1-backup.mqsc
```

Benefits:

* Disaster Recovery
* Environment Replication
* Version Control

---

## Configuration Management

MQSC scripts should be treated as source code.

Recommended approach:

```text id="hhl44u"
Git Repository
      |
 MQSC Scripts
      |
 Pull Requests
      |
 Change Approval
      |
 Deployment
```

Benefits:

* Auditability
* Traceability
* Repeatability

---

## Version Control

Store:

* Queue Definitions
* Channel Definitions
* Listener Definitions
* Security Configuration
* Operational Procedures

Example repository:

```text id="zkls7s"
mq-config/
├── queues
├── channels
├── listeners
├── security
└── recovery
```

---

## SSL Certificate Backup

Certificates are critical for secure communications.

Backup:

* Key Repositories
* Certificates
* Trust Stores

Typical location:

```text id="znzgjf"
/var/mqm/qmgrs/QM1/ssl
```

Loss of SSL artifacts may prevent secure channels from operating.

---

## Recovery Concepts

Recovery planning should answer:

### What failed?

Examples:

* Queue Manager
* Server
* Storage
* Site

---

### What must be recovered?

Examples:

* Configuration
* Messages
* Security
* Connectivity

---

### How quickly?

Recovery objectives should be defined in advance.

---

## Recovery Objectives

### RTO

Recovery Time Objective.

Question:

```text id="ujm9hz"
How long can the business tolerate downtime?
```

---

### RPO

Recovery Point Objective.

Question:

```text id="pnf3ae"
How much data loss is acceptable?
```

---

## Disaster Recovery Considerations

A Disaster Recovery strategy should include:

* Backup Procedures
* Recovery Procedures
* Documentation
* Testing
* Escalation Paths

Recovery plans should be validated regularly.

---

## Change Management

Changes should never be performed directly in production without proper controls.

Recommended workflow:

```text id="g5lw3h"
Development
      |
Testing
      |
Approval
      |
Production
```

---

## Documentation Requirements

Every Queue Manager should have documentation describing:

* Purpose
* Owners
* Applications
* Channels
* Listeners
* Dependencies
* Recovery Procedures

---

## Backup Validation

A backup is only useful if it can be restored.

Administrators should regularly test:

* Configuration Recovery
* Object Recovery
* Disaster Recovery Procedures

---

## Administrative Best Practices

### Automate Backups

Avoid manual backup procedures.

---

### Use Version Control

Store configuration as code.

---

### Test Recovery

Validate recovery procedures periodically.

---

### Protect Certificates

Backup SSL repositories securely.

---

### Document Everything

Documentation reduces recovery time and operational risk.

---

## Operational Checklist

Daily or weekly activities:

* Verify Backup Execution
* Verify Repository Updates
* Validate Recovery Documentation
* Review Configuration Changes
* Verify SSL Artifacts
* Confirm Recovery Procedures

---

## Chapter Summary

You learned:

* Backup Strategies
* Configuration Management
* saveqmgr
* dmpmqcfg
* Version Control
* SSL Backup
* Recovery Concepts
* RTO and RPO
* Disaster Recovery
* Change Management
* Operational Best Practices

Backup and configuration management are critical disciplines that ensure IBM MQ environments remain recoverable, auditable and operational during both routine maintenance and unexpected incidents.

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
