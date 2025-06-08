---
layout: post
title: "A Survey of Multi-Agent Systems"
date: 2025-06-05
categories: papers
tags: [agents]
description: "A classical, foundational survey paper covering agent architectures, cooperation, competition, and communication in MAS"
image: /images/image1.png
---

# Multi-Agent Systems : MASs 

<a href = "https://ieeexplore.ieee.org/document/8352646">Paper Link </a>


**Note** : Paper is paper from 2018

## 📝 Abstract
Multi-Agent Systems (MAS) involve autonomous agents working collaboratively to solve complex problems. These systems face challenges like coordination, communication, task allocation, and security. This paper gives a holistic view of all these aspects with theoretical and structural insights.

---

## Introduction
Distributed AI can be grouped into:

1. **Parallel AI**

   * Enhances performance of classical AI using task-parallelism.

2. **Distributed Problem Solving (DPS)**

   * Decomposes a task across multiple computing nodes.

3. **Multi-Agent Systems (MAS)**

   * Uses cooperation between independent agents to solve complex tasks.

The paper aims to be domain-agnostic and broadly applicable.

---

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

---


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

