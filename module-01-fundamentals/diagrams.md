# IBM MQ Bootcamp

# Module 01 – Diagrams

This document contains the reference diagrams used throughout Module 01.

---

# Diagram 01 – Basic Messaging Flow

```text
+---------------+
| Application A |
+---------------+
        |
        | PUT
        v
+---------------+
| IBM MQ Queue  |
+---------------+
        |
        | GET
        v
+---------------+
| Application B |
+---------------+
```

Purpose:

Illustrates the most basic messaging pattern where a producer sends a message and a consumer receives it.

---

# Diagram 02 – Queue Manager Architecture

```text
+-----------------------------------+
|         Queue Manager             |
|                                   |
|  +---------+   +-------------+    |
|  | Queue   |   | Queue       |    |
|  | LOCAL   |   | REMOTE      |    |
|  +---------+   +-------------+    |
|                                   |
|  +---------+   +-------------+    |
|  | Channel |   | Listener    |    |
|  +---------+   +-------------+    |
|                                   |
+-----------------------------------+
```

Purpose:

Illustrates the major runtime components managed by a Queue Manager.

---

# Diagram 03 – Point-to-Point Messaging

```text
Producer
    |
    v
+---------+
| Queue   |
+---------+
    |
    v
Consumer
```

Characteristics:

* One producer
* One consumer
* Reliable delivery

---

# Diagram 04 – Request / Reply Pattern

```text
Application A
      |
      v
+---------------+
| Request Queue |
+---------------+
      |
      v
Application B
      |
      v
+-------------+
| Reply Queue |
+-------------+
      |
      v
Application A
```

Characteristics:

* Request requires response
* Common in transactional workloads

---

# Diagram 05 – Publish / Subscribe Pattern

```text
             +--------+
             | Topic  |
             +--------+
                 |
      +----------+----------+
      |          |          |
      v          v          v

Subscriber A  Subscriber B  Subscriber C
```

Characteristics:

* One publisher
* Multiple consumers
* Event distribution

---

# Diagram 06 – Message Lifecycle

```text
Application
      |
      v
 Message Created
      |
      v
 MQPUT
      |
      v
 Queue Manager
      |
      v
 Queue Storage
      |
      v
 MQGET
      |
      v
 Consumer
```

Purpose:

Illustrates the complete lifecycle of an IBM MQ message.

---

# Diagram 07 – Delivery Guarantee Models

```text
At Most Once
     |
     +--> Possible Loss
     +--> No Duplicates

At Least Once
     |
     +--> No Loss
     +--> Possible Duplicates

Exactly Once
     |
     +--> No Loss
     +--> No Duplicates
```

Purpose:

Illustrates message delivery guarantees.

---

# Diagram 08 – IBM MQ in Modern Architectures

```text
                +------------------+
                | API Connect      |
                +------------------+
                         |
                         v

+-----------+     +-------------+     +-------------+
| Mobile    | --> | IBM MQ      | --> | Core System |
| Apps      |     | Queue Mgr   |     |             |
+-----------+     +-------------+     +-------------+

                         |
                         v

                +------------------+
                | App Connect      |
                +------------------+

                         |
                         v

                +------------------+
                | Event Streams    |
                +------------------+
```

Purpose:

Demonstrates IBM MQ as part of a modern integration platform.

---

# Diagram 09 – Hybrid Cloud Architecture

```text
On-Premises
+------------------+
| Queue Manager A  |
+------------------+
          |
          |
          v
-----------------------------
        Network
-----------------------------
          |
          |
          v

Cloud
+------------------+
| Queue Manager B  |
+------------------+
```

Purpose:

Illustrates IBM MQ communication across hybrid environments.

---

# End of Diagrams
