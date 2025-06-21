---
layout: post
title: "FineTuned Language Models Are Zero-Shot Learners"
date: 2025-06-21
categories: [papers]
tags: [llm]
description: "FineTuned Language Models Are Zero-Shot Learners"
image: /images/image1.png
---

<img src="{{ '/poster/finetunemodelarezeroshot.png' | relative_url }}">


# FineTuned Language Models Are Zero-Shot Learners

🔗 [**Original Paper (Sennrich et al., 2015)**](https://arxiv.org/pdf/2109.01652)


## Abstract

* Proposes **instruction tuning**: finetuning pretrained LMs on >60 NLP tasks phrased as natural‑language instructions.
* Produces **FLAN**, a 137B‑parameter model.
* On **unseen tasks**, FLAN beats zero‑shot GPT‑3 (175B) on 20/25 datasets and even few‑shot GPT‑3 on benchmarks like ANLI, RTE, BoolQ, AI2‑ARC, OpenBookQA, and StoryCloze.
* Finds that **task diversity**, **model scale**, and **instruction usage** are critical drivers.


## Introduction

* Highlights the limitations of zero‑shot performance in large LMs like GPT‑3.
* Motivates converting tasks into **natural‑language instruction templates** (e.g., “Translate: ...”, “Is it positive or negative?”).
* Presents the concept of **instruction tuning** to align LMs with human-style instructions.


## Model Architecture

* Uses a **decoder-only Transformer** model (~137B params), pretrained on diverse data (web text, code, dialogue, multilingual).
* The base model (“LaMDA‑PT”) is similar in scale to GPT‑3, but with different pretraining corpora.


## Instruction Tuning (FLAN)

* Aggregates 62 datasets from TensorFlow Datasets across **12 task clusters** (e.g., translation, NLI, commonsense, reading comprehension).
* Converts each dataset into **instruction‑input → output** pairs using 10 templates per dataset cluster.
* Finetunes with up to 30,000 examples per dataset, balanced via proportional mixing and gradient updates (total ~30k steps).


## Evaluation & Results

* **Unseen-task protocol**: hold out entire task clusters during tuning to test on zero‑shot generalization.
* **Comparisons**: base model vs FLAN vs zero‑few‑shot GPT‑3.
* **Findings**:

  * FLAN surpasses zero‑shot GPT‑3 on 20/25 tasks.
  * Outperforms few‑shot GPT‑3 on key benchmarks such as ANLI, RTE, BoolQ, AI2‑ARC, OpenBookQA, StoryCloze.
  * Benefits consistent across task clusters: NLI, QA types, etc.


## Ablation Studies

* **Scale Effect**: models of 422M, 2B, 8B, 68B, 137B params tested. Instruction tuning yields significant gains primarily at larger scales (≥8B–137B).
* **Task diversity**: increasing number of tuning tasks improves zero‑shot performance on unseen tasks.
* **Instruction necessity**: removing templates or replacing them with dataset names degrades performance significantly.
* **Few‑shot exemplar augmentation**: adding a few examples within instructions further boosts performance and stabilizes results.
* **Prompt tuning compatibility**: FLAN serves as a better base for continuous prompt tuning, achieving strong performance with few labeled examples .



## Implementation Details

* Datasets limited to 30k examples each (others capped proportionally).
* Finetuning config: 30k gradient updates, batch size 8,192, learning rate 3e‑5, sequence lengths 1,024/256, using Adafactor optimizer.
* Training is efficient: only ~2% extra compute over pretraining .



## Discussion & Conclusion

* Instruction tuning effectively bridges prompting and fine‑tuning approaches.
* FLAN showcases strong zero‑shot capabilities by learning to "follow instructions."
* Shows that labeled data can augment pretrained LMs beyond single‑task fine‑tuning.
* Suggests future directions: broader task clusters, cross‑lingual tuning, reducing bias, behavior control .


## Ethical & Environmental Considerations

* **Bias risk**: tasks and templates may embed social biases, which instruction‑tuned models could amplify.
* **Accessibility trade‑off**: easier-to-use models have pros and cons regarding misuse.
* **Energy impact**: FLAN uses \~2% more compute post‑pretraining (\~451 MWh for base LM, carbon \~26 tCO₂e) .



## Summary

FLAN, a 137B‑parameter model trained with **instruction tuning** on over 60 tasks, substantially enhances zero‑shot performance—outperforming zero‑ and few‑shot GPT‑3 on most benchmarks. Core contributions include demonstrating that **model scale**, **instruction diversity**, and **structured tasks** are key, while also showing compatibility with few‑shot prompting and prompt tuning.
