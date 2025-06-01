---
layout: post
title: "Reasoning Capabilities in Large Language Models"
date: 2025-05-31
categories: papers
tags: [llm, reasoning, chain-of-thought, prompt-engineering]
description: "Exploring the reasoning and planning abilities of large language models in dynamic environments."
image: /images/image3.png
---

# Towards a Deeper Understanding of Reasoning Capabilities in Large Language Models

<a href = "https://arxiv.org/pdf/2505.10543">Paper Link </a>

## 🧠 **Abstract**

Large Language Models (LLMs) demonstrate remarkable performance on standardized benchmarks, but their true capabilities in dynamic, real-world environments remain underexplored. This study evaluates LLMs across a range of interactive and adaptive tasks. 

Key findings include:

* **Model size vs. prompt quality**: Larger models consistently outperform smaller ones, but the performance gap can be significantly reduced through strategic prompting.
* **Prompt length matters**: Excessively long prompts degrade performance, especially in smaller models.
* **Prompting techniques**: Advanced methods like Chain-of-Thought (CoT) and Self-Reflection are beneficial for smaller models but yield diminishing returns for larger ones.
* **Generalization limitations**: While techniques like CoT and Reflexion help in some tasks, they do not generalize well across all domains.
* **Lack of human-like intelligence**: Current LLMs fall short in tasks requiring planning, deep reasoning, or spatial coordination.
* **Benchmark limitations**: Standard benchmarks are often static and narrow, failing to capture the messiness and complexity of real-world decision-making.


## 🔍 **Introduction**

This study presents a **systematic evaluation of LLMs** in dynamic decision-making settings that go beyond traditional static benchmarks. It focuses on how LLMs handle:

* **Prompting strategies** such as:

  * **Reflection** – learning from past responses,
  * **Heuristic mutation** – modifying prompts based on observed behavior,
  * **Planning** – explicit action sequencing for achieving long-term goals.

### 🧪 Key Findings:

* **Prompting impact varies with model size**:

  * Smaller models often suffer when subjected to excessive reasoning chains.
  * Larger models show robustness but gain marginal improvements from advanced prompting.
* **Reasoning is not general-purpose**:

  * CoT, Self-Refine, and Reflexion yield **inconsistent improvements** across different tasks.
* **Inadequacy of current benchmarks**:

  * QA datasets and math word problems **overstate LLM reasoning abilities**.
  * **Static tasks** fail to capture the demands of real-world reasoning.

To address this, the authors use **SMARTPLAY** – a benchmark of **dynamic-interactive tasks** that reveal genuine reasoning and planning capabilities more effectively.



## 🧠 **Background**

LLMs are fundamentally trained to **predict the next token**, not to reason, plan, or coordinate actions across time. This creates major limitations when these models are placed in dynamic environments where memory, feedback, and strategy are essential.

### 🧰 **Emerging Prompting Techniques**:

1. **Chain of Thought (CoT)** – Encourages step-by-step reasoning.
2. **Self-Refine** – Models critique and revise their own outputs iteratively.
3. **ReAct** – Combines reasoning with environment-based actions.
4. **Reflexion** – Models reflect on previous outcomes to guide future behavior.

### ⚙️ **LLM Agent Behavior: Key Enhancements**

* **Iterative Planning Approaches**:

  * **AutoPlan** – Replans based on partial progress and new context.
  * **DEPS** – Leverages a feedback loop for dynamic adjustment.
  * **RCI** – Targets precise task execution in structured environments.

* **Evolutionary Prompt Optimization**:

  * **EvoPrompt** – Uses genetic algorithms to evolve effective prompts.
  * **PLUM / LLaMEA** – Generate and evaluate diverse prompts, selecting the best-performing variants.

These strategies represent **new directions** for improving LLM performance in more complex, real-world settings.



### 🧪 **What This Study Contributes**

* Introduces a **unified benchmark suite** for evaluating dynamic task performance.
* Demonstrates the **non-trivial impact of prompting strategy and model size**.
* Challenges the overreliance on static benchmarks by promoting **interactive and evolving testbeds**.
* Offers critical insight into the **gap between LLM performance on benchmarks and their real-world utility**, especially in **planning, reasoning, and adaptive behavior**.


## Methodology

<img src="{{ '/images/image3.png' | relative_url }}">

* **Agent**:

  * Operates at each timestep to select an action.
  * Uses a prompt composed of: game manual, task, history, current state, and possible actions.
  * Objective: maximize cumulative reward across episodes.

* **Reflection**:

  * Activated at each timestep within an episode.
  * Analyzes the trajectory (state, action, reward, next state) so far.
  * Provides feedback to guide better decision-making during the same episode.
  * Reset between episodes due to potential changes in environment dynamics.

* **Oracle**:

  * Evolves general heuristics across episodes using a (1+1) evolutionary strategy.
  * Generates an initial heuristic from the first episode's trajectory and reflections.
  * After each episode, mutates the heuristic and retains it if the new version performs better.
  * Enables the agent to improve over time without manual prompt engineering.

* **Planner**:

  * Forward-looking module that simulates future action sequences (up to 3 steps ahead).
  * Uses the game manual, objectives, current observation, reflection, and trajectory.
  * Selects the action with the highest expected cumulative reward.
  * Does not use heuristics to avoid prompt interference.

* **Memory**:

  * **Episodic Memory**: Stores the trajectory of the current episode; used by Reflection and Planner.
  * **Persistent Memory**: Stores the best-performing heuristic across episodes; used by Oracle for mutation.



## Test Environments

<img src="{{ '/images/image4.png' | relative_url }}">

The researchers evaluated their framework using **four SmartPlay environments**—each testing a different cognitive or reasoning skill:

### 1. **Bandit**

* Like a multi-armed bandit problem.
* Agent must **balance exploration and exploitation** to find which action (bandit arm) gives the highest reward.

### 2. **Rock Paper Scissors (RPS)**

* The agent plays against an opponent with a **biased and shuffled move distribution**.
* Tests **probabilistic reasoning** and adaptation.

### 3. **Tower of Hanoi**

* Classic planning problem involving **moving disks** according to constraints (can't place a larger disk on a smaller one).
* Tests **spatial reasoning and planning**.

### 4. **Messenger**

* The most complex environment.
* Agent must **understand synonyms in text**, avoid enemies, and **deliver a message** to a goal.
* They increased the allowed steps from 4 to 10 to make the task solvable.

💡 **Training was limited to 20 episodes**, as performance plateaued beyond that.

---

## Results and Analysis

### 📈 Scoring:

* **Bandit / RPS**: Number of optimal actions taken.
* **Hanoi**: Number of correctly moved disks.
* **Messenger**: +1 for good actions, -1 for errors.

### 🧠 **Model Size and Performance**

* **Bigger models = better performance**, generally.

| Model            | Example Score on Bandit |
| ---------------- | ----------------------- |
| **LLAMA3.3-70B** | 41.70 \[40.90 – 41.90]  |
| DEEPSEEK-R1-14B  | 41.00                   |
| MISTRAL-NEMO-12B | 34.20                   |
| LLAMA3-8B        | 40.35                   |

* **Performance gap increases** with game complexity:

  * On **Hanoi**, LLAMA3.3-70B scores **2.00**, while LLAMA3-8B only gets **0.20**.

### 🧠 Key Insight: **Prompting + Modules Help Smaller Models**

While large models perform best overall, smaller ones **can match or beat them** using modules like **Reflection, Oracle, and Planner**.

#### 📌 Examples:

* **LLAMA3-8B + Reflection + Oracle**:

  * RPS score = **26.00**, beating LLAMA3.3-70B baseline (22.20).
* **Messenger**:

  * **MISTRAL-12B + Reflection + Planner**: **1.00**, outperforming LLAMA3.3-70B baseline (**0.10**).
  * DEEPSEEK-14B also matches or beats LLAMA3.3-70B with Reflection+Oracle/Planner.

### ❗But: Improvements Are **Inconsistent**

* Some strategies (e.g., Reflection + Planner on RPS) **vary wildly** in performance (e.g., Mistral-12B scores from 10.00 to 33.00).
* So, **prompting helps, but is not reliable**.


#### Key findings by model:
<img src="{{ '/images/image5.png' | relative_url }}">

* **LLAMA3-8B (smaller model):**

  * Prompting strategies help **most with Instruction-Following** tasks (very strong positive correlations, r = 0.75 to 0.94).
  * **Reflection alone correlates highly with Long-Text Understanding** (r = 0.78).
  * **Reflection + Oracle** correlates best with **Learning-from-Interactions** (r = 0.73).
  * **Reflection + Planner** shows a small positive correlation with **Planning** (r = 0.23).

* **MISTRAL-NEMO-12B (mid-sized model):**

  * Strong correlations for **Instruction-Following** (r = 0.82 to 0.98).
  * Moderate to high correlations with **Long-Text Understanding** (r = 0.55 to 0.81).
  * Slight negative correlations for **Understanding the Odds** and **Generalization** (meaning prompting strategies didn't help or slightly hurt in those areas).

* **DEEPSEEK-R1-14B:**

  * Strongly correlated with **Instruction-Following** (r = 0.87 to 0.94) and **Long-Text Understanding** (r = 0.69 to 0.79).
  * Small negative correlations for **Generalization** and **Understanding the Odds**.

* **LLAMA3.3-70B (largest model):**

  * Gains are strongest on **Learning-from-Interactions** (r = 0.85 to 1.00) and **Understanding the Odds** (r = 0.51 to 0.81).
  * Moderate positive effects on **Instruction-Following** and **Generalization**.
  * Slight negative correlations with **Error Handling, Planning, Reasoning, and Spatial Reasoning**.
  * Near zero correlation with **Long-Text Understanding**, except Reflection + Oracle showing a negative correlation (r = -0.42).



## Conclusion

* **Advanced prompting strategies** like self-reflection, heuristic mutation (Oracle), and planning show both promise and limitations when applied to open-source large language models (LLMs) on the SmartPlay benchmark.

* **Excessive reasoning can hurt smaller models**, especially on simpler tasks. This happens because:

  * The model must shift through more information, increasing **signal-to-noise ratio**, making it harder to focus.
  * It leads to **distraction and overthinking**, causing the model to overcomplicate the task and ignore simpler, more effective solutions.

* **Larger models generally perform better**, but well-designed prompting strategies can **help smaller and mid-sized models close the performance gap**.

* Having a **dense, task-aligned reward signal** helps improve decision-making by the agent, which is an easier approach compared to the significant manual effort needed to engineer the optimal prompts.

* **Small models benefit most from advanced prompting on complex tasks**, but there is **significant variability** in results:

  * The same prompt might lead to substantial performance gains in some runs.
  * Or worse performance than the baseline in others.
  * This shows current prompting methods are **brittle and unreliable**, indicating a need for more robust and stable techniques.

* Many reasoning studies report only **aggregate metrics like accuracy or F1 scores**, but this paper warns that **ignoring variability and instability can mislead conclusions** and hurt reproducibility and generalization.

* Despite some **proficiency on in-distribution data**, the paper finds **little evidence for true emergent reasoning or self-learning** in the LLMs.

  * Common failure modes include **hallucinating invalid action sequences** and **getting stuck in loops** during decision-making.