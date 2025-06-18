---
layout: post
title: "Prompt Engineering Guide"
date: 2025-06-18
categories: blog
tags: [prompting]
description: "Prompt engineering is a relatively new discipline for developing and optimizing prompts to efficiently use language models"
---

<img src="{{ '/poster/prompt_enginnering.png' | relative_url }}">

# Prompt Enginnering Guide


## Introduction

**Prompt Engineering (PE)** is a discipline focused on designing and optimizing prompts to effectively utilize Language Models (LMs) for a broad range of applications and research tasks.

Researchers use PE to:

* Explore the capabilities and limitations of large language models (LLMs).
* Improve LLM performance on a wide range of complex tasks.
* Augment LLMs with domain-specific knowledge and external tools.
* Enhance safety by implementing safeguards and behavioral guardrails.

---

## LLM Settings

Interaction with LLMs typically occurs via APIs. Tuning parameters in these APIs is essential to control the behavior, reliability, and quality of model outputs.

<img src="{{ '/images/promptengineering/image1.png' | relative_url }}">

* **Temperature**

  * Controls randomness in outputs.
  * Low temperature (e.g., 0.2) leads to more deterministic, factual responses.
  * High temperature (e.g., 0.8–1.0) encourages creativity and diversity.

* **Top-p (Nucleus Sampling)**

  * Limits the next-token selection to the smallest set of tokens whose cumulative probability exceeds *p*.

  * Low values (e.g., 0.3) restrict outputs to high-confidence completions.

  * High values allow more exploratory, creative responses.

  > 🔹 **Note**: Adjust *either* Temperature *or* Top-p — not both — for best control.

* **Max Tokens**

  * Sets the upper limit on the length of the response.
  * Helps control cost and avoids overly long or irrelevant outputs.

* **Stop Sequences**

  * Define specific tokens or phrases at which the model will stop generating.
  * Useful for structuring responses (e.g., stopping after 10 list items or at a delimiter).

* **Frequency Penalty**

  * Applies a penalty to tokens that have already appeared frequently.
  * Higher values reduce repetition and encourage more varied wording.

---

## Zero-Shot Prompting

* Prompts include no examples—only direct instructions.
* Relies on the model’s pre-trained understanding of the task.

```python
Classify the text into neutral, negative, or positive.
Text: I think the vacation is okay.
Sentiment:
```

* Instruction tuning has significantly improved zero-shot task performance in modern LLMs.

---

## Few-Shot Prompting

* Includes a few curated examples to guide the model’s behavior.

```python
This is awesome! // Positive  
This is bad! // Negative  
Wow, that movie was rad! // Positive  
What a horrible show! //
```

* Few-shot prompting improves performance on simpler tasks, but may still fall short for reasoning-intensive tasks (e.g., arithmetic, logic, commonsense reasoning).

---

## Chain-of-Thought Prompting

* Encourages intermediate reasoning steps to solve complex problems.
* Often combined with few-shot examples for optimal performance.

```python
Q: If there are 3 cars and each car has 4 tires, how many tires are there?  
A: Let's think step by step.  
There are 3 cars.  
Each car has 4 tires.  
So, 3 * 4 = 12 tires.  
Answer: 12
```

<img src="{{ '/images/promptengineering/image4.png' | relative_url }}">
<img src="{{ '/images/promptengineering/image5.png' | relative_url }}">

---

## Meta Prompting

* Focuses on the structure and style of the task rather than its content.
* Useful for generalizing tasks, building reusable prompt templates, or training LLMs on abstract task formats.

<img src="{{ '/images/promptengineering/image6.png' | relative_url }}">

---

## Self-Consistency

* An enhancement over standard Chain-of-Thought prompting.
* Involves sampling multiple reasoning paths and selecting the most common or consistent final answer.
* Helps increase accuracy and robustness in reasoning tasks.

---

## Prompt Chaining

* Decomposes a complex task into smaller, sequential sub-tasks.
* Each step uses the output of the previous prompt as input to the next.
* Improves transparency, modularity, and interpretability in LLM workflows.

<img src="{{ '/images/promptengineering/image7.png' | relative_url }}">


## Tree of THought

*  Maintains tree of thoughts, where thoughts represent coherent language sequence.
* Enables an LM to self-evaluate the progress through intermediate thoughts made towards solving a problem through a deliberate reasoning process.
* Comes from the idea of graph BFS i.e compare branches.


<img src="{{ '/images/promptengineering/image8.png' | relative_url }}">




## References
* <a href="https://www.promptingguide.ai/">Prompt Engineering Guide</a>