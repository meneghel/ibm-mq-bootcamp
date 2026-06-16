# IBM MQ Bootcamp

# Module 02 – Administration & Operations

# Presentation Guide

---

## Presentation Overview

This presentation supports the delivery of Module 02 – Administration & Operations.

The material is intended for:

* Instructor-Led Training
* Virtual Training
* Self-Paced Learning
* Enterprise Workshops

Estimated Duration:

```text id="4f1k8s"
4 Hours
```

Recommended Delivery:

```text id="u7r3m5"
2 Sessions of 2 Hours
```

---

# Slide 01 – Module Introduction

Title:

```text id="b5e9t4"
IBM MQ Administration & Operations
```

Topics:

* Module Objectives
* Learning Journey
* Hands-On Labs
* Expected Outcomes

---

# Slide 02 – Learning Objectives

Students will learn:

* Queue Manager Administration
* MQSC Fundamentals
* Queue Administration
* Channel Administration
* Listener Administration
* Monitoring
* Backup & Recovery

---

# Slide 03 – The Role of an MQ Administrator

Topics:

* Operational Responsibilities
* Daily Activities
* Production Support
* Enterprise Governance

Diagram:

```text id="q9m2c7"
IBM MQ Administrator Responsibilities
```

---

# Slide 04 – Queue Manager Fundamentals

Topics:

* What is a Queue Manager?
* Core Responsibilities
* Runtime Components

Diagram:

```text id="v6t8w1"
Queue Manager Architecture
```

---

# Slide 05 – Queue Manager Lifecycle

Topics:

* Creation
* Startup
* Shutdown
* Recovery

Commands:

```bash id="t3r6y9"
crtmqm
strmqm
endmqm
dspmq
```

Diagram:

```text id="p4k7d3"
Queue Manager Lifecycle
```

---

# Slide 06 – Queue Manager States

Topics:

* Running
* Starting
* Ended Normally
* Running Elsewhere

Operational Considerations

---

# Slide 07 – MQSC Fundamentals

Topics:

* Administrative Interface
* MQSC Syntax
* Common Commands

Examples:

```mqsc id="e5u4r2"
DISPLAY
DEFINE
ALTER
DELETE
```

---

# Slide 08 – MQSC Administration Workflow

Diagram:

```text id="k1z6v5"
MQSC Administration Flow
```

Discussion:

Why MQSC remains essential for administrators.

---

# Slide 09 – Queue Administration

Topics:

* Local Queues
* Remote Queues
* Alias Queues
* Dead Letter Queues

Diagram:

```text id="n7x2c4"
Queue Types
```

---

# Slide 10 – Queue Monitoring

Topics:

* CURDEPTH
* MAXDEPTH
* IPPROCS
* OPPROCS

Operational Best Practices

---

# Slide 11 – Request / Reply Pattern

Topics:

* Enterprise Messaging
* Request Processing
* Response Handling

Diagram:

```text id="r2v8m1"
Request / Reply Pattern
```

---

# Slide 12 – Channel Fundamentals

Topics:

* Channel Architecture
* Communication Flow
* Distributed Messaging

Diagram:

```text id="h4p9z6"
Channel Architecture
```

---

# Slide 13 – Channel Types

Topics:

* SDR
* RCVR
* SVRCONN
* Cluster Channels

Discussion:

Common Use Cases

---

# Slide 14 – Channel Monitoring

Topics:

* CHSTATUS
* RETRYING
* RUNNING
* STOPPED

Common Operational Issues

---

# Slide 15 – MQRC 2059

Title:

```text id="w8q5r2"
Queue Manager Not Available
```

Topics:

* Common Causes
* Troubleshooting Workflow
* Resolution Steps

---

# Slide 16 – MQRC 2009

Title:

```text id="c6n4m8"
Connection Broken
```

Topics:

* Network Failures
* Firewall Issues
* Connectivity Validation

---

# Slide 17 – Listener Administration

Topics:

* Listener Concepts
* TCP/IP Connectivity
* Listener Lifecycle

Diagram:

```text id="m9t1x3"
Listener Architecture
```

---

# Slide 18 – Client Connectivity

Topics:

* MQ Client
* SVRCONN
* Listener
* Queue Manager

Diagram:

```text id="j5k7v4"
Client Connectivity
```

---

# Slide 19 – Monitoring Fundamentals

Topics:

* Operational Visibility
* Incident Prevention
* Capacity Monitoring

Diagram:

```text id="a7f3n9"
Monitoring Components
```

---

# Slide 20 – Operational Monitoring

Topics:

* Queue Monitoring
* Channel Monitoring
* Listener Monitoring
* Queue Manager Monitoring

---

# Slide 21 – Error Logs

Topics:

* AMQERR01.LOG
* Log Analysis
* Troubleshooting Workflow

---

# Slide 22 – FDC Files

Topics:

* First Failure Data Capture
* IBM Support
* Diagnostic Analysis

---

# Slide 23 – Backup Concepts

Topics:

* Configuration Protection
* Recovery Planning
* Governance

Diagram:

```text id="y2g8k6"
Backup Strategy
```

---

# Slide 24 – saveqmgr

Topics:

* Exporting Definitions
* Configuration Backup
* Recovery Use Cases

Examples:

```bash id="d8r1t5"
saveqmgr -m QM1
```

---

# Slide 25 – dmpmqcfg

Topics:

* Configuration Export
* Automation
* Version Control

Examples:

```bash id="u4v7m3"
dmpmqcfg -m QM1
```

---

# Slide 26 – Configuration as Code

Topics:

* Git Repositories
* Version Control
* Change Tracking

Discussion:

Modern MQ Administration

---

# Slide 27 – Change Management

Diagram:

```text id="x9p2k7"
Development → Testing → Approval → Production
```

Topics:

* Governance
* Compliance
* Operational Discipline

---

# Slide 28 – Recovery Planning

Topics:

* RTO
* RPO
* Recovery Procedures

Diagram:

```text id="b7m4q1"
Recovery Planning
```

---

# Slide 29 – Operational Best Practices

Topics:

* Naming Standards
* Monitoring Standards
* Environment Separation
* Documentation

---

# Slide 30 – Module Summary

Students Learned:

* Queue Manager Administration
* MQSC Fundamentals
* Queue Administration
* Channel Administration
* Listener Administration
* Monitoring
* Backup & Recovery

---

# Slide 31 – Hands-On Labs Review

Completed Labs:

* Lab 01 – Queue Manager Lifecycle
* Lab 02 – MQSC Fundamentals
* Lab 03 – Queue Administration
* Lab 04 – Channel Administration
* Lab 05 – Listener Administration
* Lab 06 – Monitoring & Operations
* Lab 07 – Backup & Configuration Management

---

# Slide 32 – Assessment

Topics:

* Assessment Overview
* Passing Criteria
* Next Steps

Passing Score:

```text id="v8q6t2"
70%
```

---

# Slide 33 – Next Module

Title:

```text id="m5x1p8"
Module 03 – Security
```

Topics:

* Authentication
* Authorization
* CHLAUTH
* TLS
* Certificates

---

# Slide 34 – Closing

Thank You

Questions & Answers

---

## Presentation Statistics

| Item                 | Quantity |
| -------------------- | -------- |
| Slides               | 34       |
| Diagrams             | 15       |
| Labs                 | 7        |
| Assessment Questions | 30       |

---

## Module Status

Administration & Operations

```text id="t4w7m9"
COMPLETE
```
