# The TRM Philosophy
## A Technical Manifesto on Distributed Relationship Architecture

> *"Any sufficiently advanced personal life is indistinguishable from a distributed system."*
> — Someone who has clearly been through it

---

## Abstract

Modern relationship management presents a class of problems that are, at their core, distributed systems problems. The failure modes are identical. The mitigation strategies are analogous. The eventual outcomes are similarly humbling.

This document outlines the theoretical foundations of TacticalRelationshipManagement (TRM), explains the architectural decisions that inform its design, and provides a rigorous technical framework for understanding why managing multiple concurrent relationships is, fundamentally, an engineering challenge.

We acknowledge upfront that the correct solution to all problems described in this document is honesty. We are building the wrong solution anyway. We just like the code.

---

## Table of Contents

1. [The Distributed Relationship Problem](#1-the-distributed-relationship-problem)
2. [The CAP Theorem Applied](#2-the-cap-theorem-applied)
3. [Consistency Models](#3-consistency-models)
4. [Failure Modes and Fault Tolerance](#4-failure-modes-and-fault-tolerance)
5. [The Android-Only Doctrine](#5-the-android-only-doctrine)
6. [The Case Against Monolithic Architecture](#6-the-case-against-monolithic-architecture)
7. [Load Balancing Emotional Labour](#7-load-balancing-emotional-labour)
8. [The CAP Theorem Revisited: A Proof](#8-the-cap-theorem-revisited-a-proof)
9. [Observability and the Threat of Logging](#9-observability-and-the-threat-of-logging)
10. [The Eventual Consistency Problem](#10-the-eventual-consistency-problem)
11. [On Latency](#11-on-latency)
12. [The GrapheneOS Addendum](#12-the-grapheneos-addendum)
13. [Conclusion](#conclusion)

---

## 1. The Distributed Relationship Problem

A traditional, monolithic relationship architecture consists of two nodes: Node A (yourself) and Node B (your partner). Communication between nodes is synchronous, transparent, and fully consistent. Both nodes share the same state at all times.

This architecture is simple, reliable, and the engineers who designed it (society, broadly speaking) recommend it strongly. We are not here to argue with them. We are here to document what happens when someone ignores their advice.

When a second node is introduced — Node C — the system transitions from a simple client-server model to a **distributed architecture**. This transition introduces a class of problems that computer scientists have spent decades attempting to solve:

- **State synchronisation** — Nodes B and C must not share state. If they do, the system fails catastrophically.
- **Network partitioning** — Nodes B and C must remain unaware of each other's existence on the network.
- **Consistency guarantees** — The information presented to Node B must be internally consistent. The information presented to Node C must be internally consistent. These two consistent states must not be reconcilable with each other.
- **Fault tolerance** — The system must degrade gracefully when components fail. And they will fail.

TRM is, at its core, a **middleware layer** that sits between the operator (you) and the distributed node cluster (everyone else), managing state, partitioning traffic, and attempting — with limited success — to maintain consistency across a fundamentally inconsistent system.

---

## 2. The CAP Theorem Applied

In distributed systems, the CAP Theorem states that it is impossible for a distributed data store to simultaneously provide more than two of the following three guarantees:

- **Consistency** — Every read receives the most recent write or an error
- **Availability** — Every request receives a response
- **Partition Tolerance** — The system continues to operate despite network partitions

In the context of distributed relationship management, we redefine these properties as follows:

| CAP Property | Distributed Systems Definition | TRM Definition |
|---|---|---|
| **Consistency** | All nodes see the same data at the same time | All parties have the same understanding of your current relationship status |
| **Availability** | The system responds to every request | You are reachable and present to all parties at all times |
| **Partition Tolerance** | The system functions despite network splits | The system functions despite Node B and Node C occupying the same physical space |

### The TRM CAP Theorem

**You cannot have all three.**

This is not a software limitation. This is a mathematical proof. The options are:

**Option 1: Consistency + Availability (no Partition Tolerance)**
Everyone knows the truth. You are available to all parties. The system collapses the moment B and C are in the same room. This is the "one honest conversation" configuration. Recommended by literally everyone.

**Option 2: Consistency + Partition Tolerance (no Availability)**
Everyone who interacts with you has accurate information, but you are not always available. You have achieved honesty through absence. You have also achieved loneliness. Technically sound.

**Option 3: Availability + Partition Tolerance (no Consistency)**
You are always available to all parties. The network remains partitioned. But the data is inconsistent — different nodes have different versions of reality. **This is the configuration TRM is designed to support.**

We are not proud of this. But we have documented it thoroughly.

---

## 3. Consistency Models

Distributed systems offer several consistency models. Each has a direct analogue in relationship architecture.

### Strong Consistency
All nodes see the same state simultaneously. Every party has the same, accurate, up-to-date understanding of your situation.

**Also known as:** Honesty.
**TRM Support:** None. This is out of scope by design.

### Eventual Consistency
All nodes will *eventually* reach the same state, but there may be periods of inconsistency. Given sufficient time, all parties will have consistent information.

**Also known as:** The Truth Coming Out.
**TRM Support:** TRM does not prevent eventual consistency. It only delays it. This is documented in the README. It bears repeating here.

### Causal Consistency
If operation A causally precedes operation B, all nodes will see A before B.

**Also known as:** If you get caught doing one thing, the other things will also surface in causal order.
**TRM Support:** Limited. The `SpatialDataSanitizer` attempts to interrupt causal chains by removing evidence before it can propagate. Results are mixed.

### Read-Your-Own-Writes Consistency
A node will always see the effects of its own operations.

**Also known as:** You know what you've done.
**TRM Support:** Full. Unfortunately.

---

## 4. Failure Modes and Fault Tolerance

All distributed systems fail. The question is not whether failure will occur, but how the system behaves when it does. A well-designed system fails gracefully. A poorly designed system fails catastrophically and publicly.

### Identified Failure Modes

**The Byzantine Fault**
In distributed systems, a Byzantine fault occurs when a node provides different, conflicting information to different parts of the system. In TRM architecture, this is not a fault — it is the entire operational model. However, Byzantine faults become critical when the conflicting information is independently verifiable. 

*Example: You told Node B you were at work. You told Node C you were at the gym. Your running app posted a route to your public Strava. None of these are consistent. The system has failed.*

**The Split-Brain Scenario**
Occurs when network partitioning causes two nodes to both believe they are the primary node. In relationship architecture, this occurs when Node B and Node C are both operating under the assumption of exclusivity simultaneously.

*This is less a failure mode and more the foundational architecture of the problem. TRM does not solve this. TRM manages the symptoms.*

**Cascading Failure**
A failure in one component triggers failures in dependent components. In distributed systems, this can bring down an entire cluster.

*Example: The Contact Camouflage alias fails. Node B sees the real name. Node B calls Node C directly. Node C answers. The entire system fails simultaneously across all nodes. Recovery is not possible. Begin shutdown procedures.*

**The Thundering Herd Problem**
Occurs when a large number of processes are simultaneously triggered by the same event, overwhelming the system.

*Example: You post a photo at an event you said you weren't attending. Multiple nodes process this information simultaneously. Your phone receives eleven messages within ninety seconds. The system cannot respond to all of them with consistent information. This is the thundering herd. You created this.*

### Fault Tolerance Strategies

TRM implements the following fault tolerance patterns:

| Pattern | Implementation | Effectiveness |
|---|---|---|
| **Circuit Breaker** | Ghost Mode — blocks incoming traffic when Node A proximity detected | Moderate |
| **Bulkhead** | Contact Camouflage — isolates node identities to prevent cross-contamination | Low to Moderate |
| **Retry with Backoff** | Auto-SMS "My phone is acting up" — buys time before retry | One use only |
| **Graceful Degradation** | Acoustic Alibi Engine — system continues to function in degraded (lying) mode | Situational |
| **Health Checks** | BLE Watchdog — continuous proximity monitoring | Battery intensive |

---

## 5. The Android-Only Doctrine

The decision to support Android exclusively is not arbitrary. It is the result of a rigorous technical evaluation of platform capabilities against the requirements of distributed relationship management.

### The Requirements Analysis

A viable platform for TRM must support the following:

**R1: Background Process Persistence**
The system must be able to monitor environmental conditions (proximity, location, incoming calls) without requiring the application to be in the foreground.

*Android: Supported via foreground services, WorkManager, and JobScheduler.*
*iOS: Background processes are aggressively suspended by the OS. The application sleeps. The threat does not sleep. This is a fundamental architectural incompatibility.*

**R2: Call Interception**
The system must be able to evaluate incoming calls and make programmatic decisions about their disposition before the user is notified.

*Android: Supported via `CallScreeningService`. The OS explicitly provides this API.*
*iOS: Not supported. Apple's position is that you should answer your phone. Apple does not understand the assignment.*

**R3: System-Level Audio Access**
The system must be able to inject audio into the outgoing microphone stream during active calls.

*Android: Achievable via low-level audio APIs (AAudio, OpenSL ES).*
*iOS: Sandboxed. The microphone is accessible to applications but mixing into system call audio is not permitted. Apple has opinions about what goes into your phone calls. Apple's opinions are, in this context, unhelpful.*

**R4: Custom OS Deployment (Phase 2)**
The platform must support the installation of alternative operating systems to enable Phase 2 MDM deployment.

*Android: Supported. GrapheneOS installs on Pixel devices via fastboot. This is a documented, supported process.*
*iOS: Not supported. The bootloader is locked. Tim Cook has the key. Tim Cook is not giving you the key.*

**R5: Sideloading**
The system must be installable outside of official app store review processes, given that the official app store review process would correctly reject this application immediately.

*Android: APK sideloading is supported. Enable "Install from unknown sources." Done.*
*iOS: Not supported without a developer account, a Mac, and a signed profile that expires every seven days, at which point the application stops working and you must explain to Node B why your "privacy app" has stopped functioning.*

### The Verdict

iOS fails four of five requirements. It passes R3 partially, under conditions that do not apply here.

The platform is excluded on technical grounds. The jokes about iOS users are a secondary benefit.

### A Note On iOS Users

We do not dislike iOS users. Some of our closest friends use iOS. Those friends are not the target demographic for this software, because they have been correctly identified by their operating system as people who should not be running background Bluetooth surveillance services.

This is, genuinely, a feature of iOS. Apple made the right call. We are building on the platform that made the wrong one.

---

## 6. The Case Against Monolithic Architecture

Traditional relationship architecture is monolithic. A single, unified relationship handles all functions: companionship, communication, emotional support, shared logistics, long-term planning. All concerns are tightly coupled. Changes in one area immediately affect all others. The system is simple, well-understood, and benefits from decades of established best practices.

We are not recommending against monolithic architecture. Monolithic architecture is correct.

However, in the interest of completeness, we document the theoretical properties of the alternative:

### Microservices Relationship Architecture

In a microservices model, concerns are separated into independent services that communicate over well-defined interfaces:

```
┌─────────────────────────────────────────────────────────┐
│           Distributed Relationship Cluster              │
│                                                         │
│  ┌──────────────┐         ┌──────────────────────────┐  │
│  │  Node B      │         │  Node C                  │  │
│  │  Service     │         │  Service                 │  │
│  │              │         │                          │  │
│  │ - Weeknights │         │  - Weekends              │  │
│  │ - Emotional  │         │  - Different Borough     │  │
│  │   Support    │         │  - Does not know Node B  │  │
│  │   Layer      │         │    exists                │  │
│  └──────┬───────┘         └─────────────┬────────────┘  │
│         │                               │               │
│         └──────────────┬────────────────┘               │
│                        │                                │
│                   ┌────▼────┐                           │
│                   │   You   │                           │
│                   │ (Chaos  │                           │
│                   │  Core)  │                           │
│                   └─────────┘                           │
└─────────────────────────────────────────────────────────┘
```

**Theoretical Advantages:**
- Independent scaling of individual services
- Fault isolation (problems in one service don't immediately affect others)
- Technology diversity (different communication styles per service)

**Actual Disadvantages:**
- Catastrophically complex to operate
- Failure modes are non-obvious until they are extremely obvious
- Operational overhead is enormous
- There is no on-call rotation. You are always on-call. You are the entire SRE team.
- The system will achieve eventual consistency. See section 10.

**Our Recommendation:** Don't. But here is the middleware layer in case you already did.

---

## 7. Load Balancing Emotional Labour

In distributed systems, load balancing distributes incoming requests across multiple backend servers to prevent any single node from becoming a bottleneck.

In distributed relationship architecture, the operator (you) is the single backend server handling all requests from all nodes. Without load balancing, the operator becomes a bottleneck, then a single point of failure, then a person sitting quietly in their car for forty minutes before going inside.

### Load Balancing Strategies

**Round Robin**
Requests are distributed evenly across all available time slots. Node B gets Tuesday and Thursday. Node C gets Wednesday and Saturday. Sunday is for recovery and infrastructure maintenance.

*Failure mode: Bank holidays. Birthdays. Any event that disrupts the round robin schedule.*

**Least Connections**
New requests are routed to the node with the fewest active connections. The node who is asking for less, gets more attention.

*Failure mode: Nodes are adaptive. A node receiving more attention may begin to expect more attention. The load balancer has created the load it was designed to manage.*

**IP Hash (Geolocation-Based)**
Requests are routed based on origin. Node B gets the flat. Node C gets literally any other borough.

*Failure mode: London is not that big. The Jubilee line is everyone's line.*

**Health Check Based Routing**
Traffic is only routed to healthy nodes. If a node is exhibiting signs of distress — increased contact frequency, unusual questions about your whereabouts, reading your horoscope out loud — that node is flagged as degraded and traffic is temporarily rerouted.

*This is Ghost Mode. This is what Ghost Mode is.*

---

## 8. The CAP Theorem Revisited: A Proof

We stated in Section 2 that you cannot have Consistency, Availability, and Partition Tolerance simultaneously. We now provide a proof.

**Assume** you have achieved Consistency: all parties have accurate, up-to-date information about your situation.

**Then** either:
- All parties know about each other (you have Consistency but no Partition Tolerance — the partition has collapsed), **or**
- No parties know about you (you have Consistency and Partition Tolerance, but you have achieved this through complete social isolation, which is not Availability)

**Therefore**, you cannot have Consistency, Availability, and Partition Tolerance simultaneously. ∎

This proof has been peer reviewed by no one. We are confident in it anyway.

---

## 9. Observability and the Threat of Logging

In production systems, observability is achieved through three pillars: **metrics, logs, and traces**. Observability allows engineers to understand the internal state of a system from its external outputs.

In distributed relationship architecture, observability is your enemy. The goal is **minimum viable observability** — sufficient logging to operate the system yourself, zero external observability.

### Threat Vectors

**Metrics:** Your phone's screen time report. Your location history. Your bank statement. Your Uber receipts. Your calorie tracking app that logged dinner at a restaurant you said you weren't at. These are metrics. They tell a story. Audit them before someone else does.

**Logs:** Your message history. Your call log. Your photo metadata. Every image taken on a modern smartphone contains EXIF data including GPS coordinates and timestamp. You took a photo. It knows where you were. It has always known.

**Traces:** The distributed trace of a single evening is devastating in aggregate: Uber pickup location → restaurant reservation → contactless payment → Uber drop-off location → next morning's location ping. Each data point is innocuous. Together they are a complete audit trail.

### The TRM Approach to Observability Reduction

The `SpatialDataSanitizer` addresses log hygiene. The `ContactCamouflage` module addresses metric obfuscation. But the fundamental problem remains: **modern smartphones are, by design, comprehensive logging infrastructure for your entire life.**

TRM is middleware running on top of a system that was built to remember everything. We are, in engineering terms, fighting the architecture.

We are losing, slowly, over time.

This is fine. This is documented. See section 10.

---

## 10. The Eventual Consistency Problem

This section is the most important section in this document. It is also the section that renders all other sections somewhat moot.

In distributed systems, **eventual consistency** guarantees that, in the absence of new updates, all nodes will eventually converge to the same value. The system does not guarantee *when* this convergence will occur. It only guarantees that it will.

**TRM does not prevent eventual consistency.**

All parties will, given sufficient time and in the absence of extraordinary technical intervention (and sometimes despite it), arrive at a consistent understanding of your situation. The only variables are:

1. **When** convergence occurs
2. **How** convergence occurs (gracefully, or catastrophically)
3. **What** the consistent state is when convergence is reached

TRM optimises for delaying convergence and, where possible, influencing the manner of convergence. It does not prevent it. It cannot prevent it. No software can prevent it. This is a mathematical property of distributed systems and also of human beings, who are, it turns out, quite good at pattern recognition.

### The Convergence Event

When convergence occurs — and it will — the system will transition rapidly from a distributed, partitioned state to a fully consistent state. This transition is not graceful. Distributed systems engineers call this a **partition heal**. Everyone else calls it something else.

TRM has no module for this phase. This is intentional. This is outside the scope of the project. This is between you and the people you have wronged.

We just like the code.

---

## 11. On Latency

In networking, latency is the time delay between a cause and its effect. Low latency is desirable. High latency introduces inconsistencies, timeouts, and degraded user experience.

In the context of this framework, latency is your friend.

Every second between a question and its answer is an opportunity for the system to intervene. Every minute between an event and its discovery is a minute in which the `SpatialDataSanitizer` can run. Every hour between cause and effect is an hour in which the story can be refined, the logs can be cleared, and the contact can be renamed back from Pizza Hut.

TRM is, in a philosophical sense, a **latency injection framework**. It does not change the data. It only delays its arrival.

High latency does not prevent eventual consistency.

See section 10.

---

## 12. The GrapheneOS Addendum

GrapheneOS is a privacy-focused Android distribution. It is well-engineered, rigorously maintained, and used by journalists, security researchers, activists, and people who have read too much about data privacy and cannot sleep at night.

Its inclusion in this document, in the context of Phase 2 deployment, is the section of this manifesto that we feel most ambivalent about.

GrapheneOS did not ask to be here. Its developers are serious people doing serious work. The project's threat model involves nation-state actors, corporate surveillance, and the protection of vulnerable populations.

It does not involve this.

We include it because it is, technically, the correct tool for the Phase 2 requirements: a hardened, auditable, MDM-compatible Android distribution that can be deployed on consumer hardware and configured to prevent data exfiltration.

The fact that "data exfiltration" in this context means "screenshots of conversations" is not GrapheneOS's problem. It is yours.

We are sorry to GrapheneOS. We are less sorry to you.

---

## Conclusion

The problems described in this document are not fundamentally technical problems. They are human problems that happen to have technical surface area. TRM addresses the technical surface area. It does not address the underlying human problems.

The correct solution to all problems described in this manifesto is a single, direct, honest conversation. It is lower latency than any BLE scan. It has no battery impact. It requires no Android permissions. It does not involve renaming anyone Pizza Hut.

We have built the wrong solution. We have built it carefully, with good documentation, sensible architecture, and more disclaimers than any reasonable project requires.

We just like the code.

---

### Appendix A: Recommended Reading

- *Designing Data-Intensive Applications* — Martin Kleppmann (for the distributed systems concepts we have misappropriated)
- *The Art of Deception* — Kevin Mitnick (not recommended, but thematically relevant)
- *Attached* — Amir Levine and Rachel Heller (actually recommended, unironically, please read this one)
- Any book on communication in relationships (there are many, they all say the same thing, that thing is "talk to people")

### Appendix B: Glossary

| Term | Standard Definition | TRM Definition |
|---|---|---|
| Node | A single machine in a distributed network | A person in your life who believes they have your full attention |
| Partition | A network split preventing nodes from communicating | The blessed state in which Node B and Node C do not know each other |
| Eventual Consistency | All nodes converge to the same state over time | The conversation you are going to have eventually |
| Fault Tolerance | System's ability to continue operating despite failures | Your ability to maintain composure when the geofence fires early |
| Load Balancer | Distributes requests across backend servers | Your calendar |
| Single Point of Failure | One component whose failure brings down the system | You |
| Technical Debt | Accumulated shortcuts that make future work harder | This entire situation |
| Deprecation | Planned end-of-life for a system component | What you should do to this architecture immediately |

---

*TacticalRelationshipManagement (TRM) aka CheaterOS*
*PHILOSOPHY.md — v1.0.0*
*"We just like the code."*
