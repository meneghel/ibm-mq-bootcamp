# IBM MQ Bootcamp

# Module 02 – Administration & Operations

# Lab 07 – Backup & Configuration Management

---

## Lab Overview

IBM MQ environments support mission-critical business processes and therefore require proper backup, recovery and configuration management procedures.

In this lab, students will learn how to export MQ configurations, protect administrative assets, understand recovery concepts and apply operational governance practices used in enterprise environments.

This lab introduces the foundations of disaster recovery, change management and configuration-as-code for IBM MQ.

---

## Learning Objectives

By completing this lab, students will be able to:

* Export MQ configurations
* Use saveqmgr
* Use dmpmqcfg
* Understand backup strategies
* Protect MQ configuration assets
* Understand recovery concepts
* Apply configuration management practices
* Implement operational governance principles

---

## Estimated Duration

60 Minutes

---

## Prerequisites

Students should have completed:

* Lab 01 – Queue Manager Lifecycle
* Lab 02 – MQSC Fundamentals
* Lab 03 – Queue Administration
* Lab 04 – Channel Administration
* Lab 05 – Listener Administration
* Lab 06 – Monitoring & Operations

Required Environment:

* IBM MQ Installed
* Queue Manager QM1 Running

---

## Environment

Queue Manager:

```text id="0p8mku"
QM1
```

Configuration Directory:

```text id="4q3x89"
/var/mqm/qmgrs/QM1
```

Administration Interface:

```text id="yb4c9i"
MQSC
```

---

## Scenario

Your organization requires all middleware platforms to follow enterprise backup and recovery procedures.

As the IBM MQ Administrator, you must document, export and protect Queue Manager configurations while preparing the environment for recovery scenarios.

---

# Exercise 01 – Review Queue Manager Structure

Navigate to:

```bash id="m0dxu2"
cd /var/mqm/qmgrs/QM1
```

Display contents:

```bash id="9u5y8m"
ls -la
```

Review:

```text id="a1w3sd"
qm.ini
errors/
ssl/
```

Discussion:

* Which components should be protected?
* Which files are critical for recovery?

---

# Exercise 02 – Review MQ Configuration Assets

Identify:

```text id="up6cl4"
Queues
Channels
Listeners
Services
```

Discussion:

Why is configuration backup important even when messages are not being backed up?

---

# Exercise 03 – Export Configuration with saveqmgr

Execute:

```bash id="6r0e7g"
saveqmgr -m QM1
```

Review the output.

Identify:

```text id="bg4gmi"
DEFINE QLOCAL(...)
DEFINE CHANNEL(...)
DEFINE LISTENER(...)
```

Questions:

1. What information was exported?
2. How could this file be used during recovery?

---

# Exercise 04 – Export Configuration to File

Execute:

```bash id="a9a1kr"
saveqmgr -m QM1 > QM1-saveqmgr-backup.mqsc
```

Verify:

```bash id="r95vzm"
ls -la
```

Discussion:

Why should backup files be stored outside the Queue Manager directory?

---

# Exercise 05 – Export Configuration with dmpmqcfg

Execute:

```bash id="7cfm3w"
dmpmqcfg -m QM1
```

Review the output.

Discussion:

Compare:

```text id="q3n0m3"
saveqmgr
```

versus

```text id="gb3kns"
dmpmqcfg
```

Questions:

* What similarities exist?
* What differences exist?

---

# Exercise 06 – Create a Configuration Backup File

Execute:

```bash id="mxn8q7"
dmpmqcfg -m QM1 > QM1-backup.mqsc
```

Verify:

```bash id="qly2u0"
ls -la *.mqsc
```

Expected Result:

```text id="w6xv4r"
QM1-backup.mqsc
```

---

# Exercise 07 – Configuration as Code

Create a directory:

```bash id="rt3n7u"
mkdir mq-config
```

Discussion:

Example structure:

```text id="6pqj3n"
mq-config/
├── queues/
├── channels/
├── listeners/
├── security/
└── recovery/
```

Questions:

Why should MQ configuration be version controlled?

---

# Exercise 08 – SSL Backup Review

Navigate to:

```bash id="1y55k0"
cd /var/mqm/qmgrs/QM1/ssl
```

Review contents.

Discussion:

Why are SSL repositories critical?

What happens if certificates are lost?

---

# Exercise 09 – Recovery Planning

Review:

```text id="d5i2oh"
Queue Manager Failure
Storage Failure
Server Failure
Site Failure
```

Discussion:

For each scenario:

* What must be recovered?
* Which assets are required?
* What recovery steps are necessary?

---

# Exercise 10 – RTO and RPO Analysis

Define:

### RTO

```text id="fx2v29"
Recovery Time Objective
```

### RPO

```text id="vf4pzn"
Recovery Point Objective
```

Discussion:

Why should business requirements drive backup strategies?

---

# Exercise 11 – Change Management Review

Create a sample change workflow:

```text id="i2q4m4"
Development
      ↓
Testing
      ↓
Approval
      ↓
Production
```

Discussion:

Why should MQ changes follow controlled processes?

---

# Exercise 12 – Recovery Validation

Discussion:

Why is a backup insufficient if recovery procedures are never tested?

Questions:

1. How often should recovery tests occur?
2. What risks exist when recovery is never validated?

---

# Validation Checklist

Confirm that you can:

* Export MQ Configurations
* Use saveqmgr
* Use dmpmqcfg
* Identify Critical Assets
* Understand Recovery Concepts
* Define RTO and RPO
* Apply Change Management Principles
* Design Basic Backup Procedures

---

# Challenge Exercise

Research and document:

1. Multi-Instance Queue Managers
2. Native HA
3. Disaster Recovery Architectures
4. Backup Automation
5. Git-Based Configuration Management

---

# Expected Outcome

Upon completion of this lab, students will understand how IBM MQ environments are protected, documented and prepared for recovery.

Students will also understand how enterprise organizations manage configuration governance, recovery planning and operational resilience.

---

## Module Completion

Congratulations!

You have completed all hands-on laboratories for:

**Module 02 – Administration & Operations**

---

## Next Module

Proceed to:

**Module 03 – Security**
