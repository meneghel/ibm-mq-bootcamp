# IBM MQ Bootcamp

# Module 01 – Exercises

## Overview

These exercises are designed to reinforce the concepts covered in Module 01 and encourage students to apply IBM MQ fundamentals to real-world enterprise scenarios.

Students should complete all exercises before proceeding to Module 02.

---

# Exercise 01 – Messaging Around You

## Objective

Identify messaging and integration patterns currently used within your organization.

## Activities

List at least three applications that exchange information.

For each application pair identify:

* Communication mechanism
* Synchronous or asynchronous communication
* Potential reliability challenges
* Potential scalability challenges

## Example

| Producer   | Consumer     | Technology | Sync/Async   |
| ---------- | ------------ | ---------- | ------------ |
| ERP        | CRM          | REST API   | Synchronous  |
| Mobile App | Core Banking | IBM MQ     | Asynchronous |
| Billing    | Data Lake    | Kafka      | Asynchronous |

## Expected Outcome

Students understand how integration occurs in real enterprise environments.

---

# Exercise 02 – Integration Pattern Selection

## Scenario

An insurance company needs to distribute policy issuance events to:

* CRM
* Billing
* Data Lake
* Notification Platform

## Question

Which messaging pattern would you choose?

* Point-to-Point
* Request/Reply
* Publish/Subscribe

Explain your decision.

## Expected Discussion

Students should identify Publish/Subscribe as the most appropriate pattern because multiple consumers need to receive the same business event.

---

# Exercise 03 – MQ vs REST vs Kafka

## Scenario

A banking application must process financial transactions with guaranteed delivery and transactional consistency.

## Activities

Compare:

* REST
* Kafka
* IBM MQ

Evaluate:

* Reliability
* Scalability
* Transaction Support
* Operational Complexity
* Enterprise Readiness

## Question

Which technology would you recommend and why?

## Expected Discussion

Students should recognize IBM MQ as the preferred option for mission-critical transactional workloads requiring guaranteed delivery.

---

# Exercise 04 – Queue Manager Identification

## Objective

Identify the major IBM MQ runtime components.

## Activity

Analyze the architecture below:

```text
Mobile Application
        |
        v
+-------------------+
|       QM1         |
|   PAYMENTS.Q      |
+-------------------+
        |
        v
Core Banking
```

Identify:

* Producer
* Consumer
* Queue Manager
* Queue

## Expected Outcome

Students correctly identify the role of each component.

---

# Exercise 05 – Message Lifecycle

## Objective

Understand the complete lifecycle of an IBM MQ message.

## Activity

Describe the sequence of events from message creation to consumption.

Include:

1. Producer Application
2. Queue Manager
3. Queue
4. Consumer Application

## Deliverable

Create a flow diagram representing the process.

---

# Exercise 06 – Delivery Guarantees

## Objective

Understand message delivery models.

## Activities

Explain the differences between:

* At Most Once
* At Least Once
* Exactly Once

## Questions

1. Which model prioritizes performance?
2. Which model prioritizes reliability?
3. Which model is most common in financial systems?

## Expected Outcome

Students understand trade-offs between reliability and performance.

---

# Exercise 07 – Dead Letter Queue Analysis

## Scenario

A remote destination becomes unavailable during message delivery.

## Questions

1. What happens to the message?
2. What is the role of the Dead Letter Queue?
3. How should operations teams handle messages accumulated in the DLQ?

## Expected Outcome

Students understand the purpose of exception handling within IBM MQ.

---

# Exercise 08 – Architecture Review

## Objective

Evaluate an existing integration architecture.

## Activities

Review an architecture currently used by your organization.

Identify:

* Single Points of Failure
* Tight Coupling
* Availability Risks
* Scalability Constraints

## Discussion

Describe how IBM MQ could improve the architecture.

---

# Exercise 09 – Modern Architecture Discussion

## Objective

Understand IBM MQ's role in modern integration architectures.

## Questions

Discuss how IBM MQ integrates with:

* Microservices
* APIs
* Event-Driven Architectures
* Hybrid Cloud
* Containers
* Kubernetes

Provide practical examples whenever possible.

---

# Exercise 10 – Design Challenge

## Scenario

A retail organization requires integration between:

* E-Commerce Platform
* ERP
* Inventory System
* Payment Gateway
* Notification Service

## Activity

Design a high-level architecture using IBM MQ.

Include:

* Queue Manager
* Queues
* Producers
* Consumers

## Deliverable

Create a simple architecture diagram and explain your design decisions.

---

# Module Completion

Students should complete all exercises before attempting the Module 01 Assessment.

These exercises are intended to prepare students for administration, troubleshooting and architecture discussions introduced in subsequent modules.
