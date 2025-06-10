---
layout: post
title: "A Survey of Multi-Agent Systems"
date: 2025-06-05
categories: papers
tags: [software, agents, framework]
description: "A classical, foundational survey paper covering agent architectures, cooperation, competition, and communication in MAS"
image: /images/image1.png
---

# Multi-Agent Systems : MASs 

<a href = "https://ieeexplore.ieee.org/document/8352646">Paper Link </a>


**Note** : Paper is paper from 2018

## 📝 Abstract
Multi-Agent Systems (MAS) involve autonomous agents working collaboratively to solve complex problems. These systems face challenges like coordination, communication, task allocation, and security. This paper gives a holistic view of all these aspects with theoretical and structural insights.



## Introduction
Distributed AI can be grouped into:

1. **Parallel AI**

   * Enhances performance of classical AI using task-parallelism.

2. **Distributed Problem Solving (DPS)**

   * Decomposes a task across multiple computing nodes.

3. **Multi-Agent Systems (MAS)**

   * Uses cooperation between independent agents to solve complex tasks.

The paper aims to be domain-agnostic and broadly applicable.



## 🤖 What is an Agent?

An **agent** is a flexible, autonomous entity situated in an environment. It:

* Perceives the environment through sensors.
* Makes decisions based on goals and environmental feedback.
* Acts upon the environment using actuators.

### Key Environmental Features:

* **Accessibility**: Accuracy of data sensing.
* **Determinism**: Predictability of actions’ outcomes.
* **Dynamism**: Frequency and impact of environmental changes.
* **Continuity**: Degree to which environment behaves in discrete vs. continuous manner.

Agents use:

* Environmental data
* Neighbor knowledge
* Historical actions

While agents can function alone, true MAS benefits emerge from **collaboration**.


<img src="{{ '/images/mass-1.png' | relative_url }}">




## 🤝 Why Multi-Agent Systems?

MAS are characterized by:

* **Efficiency**: Task decomposition + parallelism = faster execution.
* **Low Cost**: Shared resources reduce overhead.
* **Flexibility**: Each agent can operate semi-independently.
* **Reliability**: System can tolerate individual agent failures.


<img src="{{ '/images/mass-2.png' | relative_url }}">

### Role of Mediator:
* Acts as coordinator/orchestrator.
* May allow both centralized and decentralized communication


### Features of Multi Agent Systems
- **Leadership**  : MAS can be leaderless or leader-follow, where a leader agent directs others toward a common goal.

- **Decision Function** : Agents make decisions either proportionally (linear) or non-proportionally (non-linear) to input changes.

- **Heterogeneity** : MAS can have identical (homogeneous) or diverse (heterogeneous) agent capabilities.

- **Agreement Parameters** : Agents may agree on one, two, or multiple metrics and their derivatives (first, second, or high-order).

- **Delay Consideration** : MAS may model communication and processing delays or assume delay-free operation.

- **Topology** : Agent positions and relationships can remain static or dynamically change over time.

- **Data Transmission Frequency** : Agents transmit data periodically (time-triggered) or only upon specific events (event-triggered).

- **Mobility** : Agents can be stationary or capable of moving within and interacting across the environment.

## Differentiating MAS

<img src="{{ '/images/mass-3.png' | relative_url }}">



## 🚧 MAS Challenges

### 1. **Coordination and Control**

In a Multi-Agent System (MAS), each agent’s actions influence the environment, thereby affecting the decisions of other agents. Effective coordination is crucial for collaboratively achieving system-wide goals.

Key coordination challenges include:

* **Consensus**
  Achieving a global agreement among agents on a shared variable or feature of interest. Essential for coordinated decisions and actions.

* **Controllability**
  Refers to the ability to steer the MAS from one state to another through regulatory inputs. The degree of system dynamism (e.g., agent mobility, changing environments) influences controllability.
  Common strategy: Use of a centralized leader or controller to guide other agents toward a shared goal.

* **Synchronization**
  Ensuring that actions of agents are aligned temporally—i.e., they act at the right time in harmony. This is often interdependent with consensus, especially in time-sensitive applications like swarm robotics.

* **Connectivity**
  Agents need reliable and consistent communication links.
  Major challenges:

  * Mobility of agents (e.g., in drone swarms or vehicular networks)
  * Noisy or lossy communication environments
  * Partial or incomplete knowledge of the network topology

* **Formation**
  Designing and maintaining an optimal spatial or logical structure among agents. This includes:

  * Defining desired formations (e.g., flocking, grid, or leader-follower patterns)
  * Preserving formation under dynamic conditions



### 2. **Agent Learning**

Agents should be capable of perceiving the environment, learning from interactions, and adapting their behaviors over time.

* Use of algorithms like Reinforcement Learning (RL), Evolutionary Algorithms, or Genetic Programming.
* Agents can share learned knowledge with neighbors to improve collective performance and reduce redundant learning or negative externalities.



### 3. **Fault Detection and Robustness**

Fault detection ensures the MAS continues operating despite agent failures.

* Use of unknown observers or anomaly detection methods to identify malfunctioning agents.
* Robust MAS design often includes fault tolerance, redundancy, and self-healing mechanisms.



### 4. **Task Allocation**

Assigning tasks efficiently to agents based on their capabilities and environmental factors.

* **Centralized**: A master controller allocates tasks, which may create a bottleneck.
* **Decentralized**: Agents self-organize to distribute tasks, enhancing scalability and fault tolerance.
* **Metrics for Allocation**:

  * Agent capabilities or "talent"
  * Physical or logical proximity to the task
  * Energy or resource constraints



### 5. **Agent Organization**

The structural design that defines how agents interact, communicate, and collaborate.

Common organizational models:

* **Flat**: All agents are equal; suitable for small, simple systems.
* **Hierarchical**: Tree-based authority; easier control but prone to bottlenecks or single points of failure.
* **Holonic**: Agents are grouped into autonomous units (holons), each capable of cooperation and self-organization. Promotes scalability and flexibility.
* **Hybrid**: Combines multiple models depending on the context and requirements.



### 6. **Security and Trust**

Security in MAS is especially challenging due to decentralization and agent mobility.

* **Key Challenges**:

  * A compromised mobile agent can propagate threats across the system.
  * Dynamic membership makes authentication and access control harder.
* **Essential Security Requirements**:

  * **Authentication** – Verifying agent identity
  * **Authorization** – Defining access permissions
  * **Confidentiality** – Protecting data from unauthorized access
  * **Integrity** – Ensuring data isn't tampered with
  * **Non-repudiation** – Accountability for actions


## Summary

* MAS = multiple autonomous agents working together (or competing) to solve complex problems.
* Key benefits: **efficiency**, **flexibility**, **reliability**, and **scalability**.
* Agents perceive, decide, and act based on goals and environment.
* MAS challenges include:

  * **Coordination** (consensus, synchronization, controllability)
  * **Learning** (via RL or evolution)
  * **Task allocation** (centralized or decentralized)
  * **Fault tolerance** and **robustness**
  * **Security & trust** (authentication, integrity, etc.)
* Organizational models: **flat**, **hierarchical**, **holonic**, **hybrid**.
* MAS enable distributed problem-solving beyond traditional single-agent systems.
