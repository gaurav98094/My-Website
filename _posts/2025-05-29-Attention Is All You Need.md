---
layout: post
title: "Attention Is All You Need"
date: 2025-05-31
categories: papers
tags: [transformers, attention, deep-learning, nlp]
description: "A summary and explanation of the Transformer architecture and its impact on deep learning."
image: /images/image1.png
---

# Transformer: Attention Is All You Need

<a href="https://arxiv.org/abs/1706.03762"> Paper Link</a>

## Overview

This project introduces the **Transformer** architecture — a novel neural network model solely based on the attention mechanism. It achieves state-of-the-art performance in sequence modeling tasks such as machine translation, with superior quality, faster training times, and better parallelization compared to traditional RNN-based models.

* Achieves **28.4 BLEU** on WMT 2014 English-to-German translation.
* Achieves **41.8 BLEU** on WMT 2014 English-to-French after 3.5 days training on 8 GPUs.
* More parallelizable and requires less training time.



## Introduction

Traditional sequence models like RNNs, LSTMs, and GRUs process input tokens sequentially, limiting parallelization and increasing training time. Although tricks like factorization and conditional computation helped, these models remain inherently sequential.

Earlier attention mechanisms were used alongside RNNs to improve performance, but the Transformer is the first architecture to **fully replace recurrence with self-attention**, allowing global dependencies between input and output tokens to be modeled efficiently.

The Transformer enables:

* Greater parallelization
* Better translation quality
* Faster training (e.g., trained for 8 hours on 8 P100 GPUs)



## Background

* Sequential processing of tokens is slow and inefficient for tasks like language translation.
* CNNs were attempted for parallelization but struggled to capture long-range dependencies.
* The Transformer leverages **self-attention**, allowing every token to attend directly to every other token in the sequence.
* Single attention can dilute information; hence, **multi-head attention** is used to capture multiple aspects of dependencies.
* Transformer eliminates the need for RNNs and CNNs, relying purely on attention to process sequences.

<img src="{{ '/images/image1.png' | relative_url }}">


## Model Architecture

The Transformer follows the common encoder-decoder structure for sequence-to-sequence modeling.

* **Input tokens** are converted to contextual embeddings $(z_1, ..., z_n)$.
* Each output token depends on previous outputs.
* Uses **self-attention** and **feedforward neural networks (FFN)** instead of RNNs or CNNs.
* Multiple layers of attention + MLP layers form the encoder and decoder.

### Encoder Stack

* 6 identical layers.
* Each layer has two sub-layers:

  * Multi-head self-attention.
  * Position-wise feedforward network.
* Residual connections followed by layer normalization.
* Model dimension $d_{model} = 512$.

### Decoder Stack

* 6 identical layers (similar structure).
* Includes masked self-attention to prevent access to future tokens.



## Attention Mechanism

* Attention maps a **query** and a set of **key-value pairs** to an output.
* Output is a weighted sum of the values, where weights come from a compatibility function between the query and keys.
* Known as **Scaled Dot-Product Attention**:

  * Compute dot product between query and keys.
  * Scale by $\sqrt{d_k}$ to avoid large magnitude values.
  * Apply softmax to get weights.

<img src="{{ '/images/image2.png' | relative_url }}">

## Multi-Head Attention

* Multiple attention heads run in parallel.
* Each head learns different representation subspaces, capturing richer relationships.
* Each head operates in a subspace of dimension $d_{model} / h$, improving efficiency.



## Types of Attention in Transformer

* **Encoder-Decoder Attention:** Decoder attends to encoder output.
* **Encoder Self-Attention:** Encoder attends to input tokens.
* **Decoder Self-Attention:** Masked to prevent access to future tokens (leftward information).



## Position-Wise Feedforward Networks (FFN)

* Fully connected feedforward networks applied at each layer of encoder and decoder.
* Process embeddings independently for each position.



## Positional Encoding

Since the Transformer uses no recurrence or convolution, positional information is added via **sinusoidal positional embeddings**, enabling the model to capture token order.



## Training Details

* Dataset: WMT 2014 English-German (\~4.5 million sentence pairs).
* Hardware: 8 NVIDIA P100 GPUs.
* Training steps: 100,000 (\~12 hours); larger model trained for 300,000 steps.
* Optimizer: Adam with $\beta_1=0.9$, $\beta_2=0.98$, $\epsilon=10^{-9}$.
* Regularization: Residual dropout and label smoothing.



## Results

| Task                      | BLEU Score |
| - | - |
| WMT 2014 English → German | 28.4       |
| WMT 2014 English → French | 41.8       |


<br><br>

# Transformer Multi-Head Attention — Dimensions from Input to Output

### Setup (example numbers)

* Batch size = 32
* Sequence length = 10 tokens
* Model dimension $d_{model} = 512$
* Number of heads $h = 8$
* Dimension per head $d_k = d_v = \frac{512}{8} = 64$



## Step 1: Input embeddings

* Input is a sequence of token embeddings (or output from previous layer).
* Shape:

$$
X \in (32, 10, 512)
$$

(batch\_size, seq\_len, embedding\_dim)



## Step 2: Linear projections for queries (Q), keys (K), and values (V)

For each attention head $i$ (from 1 to 8), you have **three** projection matrices:

* $W_i^Q \in \mathbb{R}^{512 \times 64}$
* $W_i^K \in \mathbb{R}^{512 \times 64}$
* $W_i^V \in \mathbb{R}^{512 \times 64}$

You multiply the input $X$ by these:

$$
Q_i = X W_i^Q \quad\rightarrow (32, 10, 512) \times (512, 64) = (32, 10, 64)
$$

Similarly for $K_i$ and $V_i$:

$$
K_i, V_i \in (32, 10, 64)
$$



## Step 3: Scaled Dot-Product Attention (per head)

* For each head, calculate attention scores:

$$
\text{Attention}(Q_i, K_i, V_i) = \text{softmax}\left(\frac{Q_i K_i^T}{\sqrt{d_k}}\right) V_i
$$

* Shapes involved:

  * $Q_i$ is $(32, 10, 64)$
  * $K_i^T$ (transpose on last two dims) is $(32, 64, 10)$
  * Dot product $Q_i K_i^T$ yields $(32, 10, 10)$ — attention weights between tokens
  * After softmax, multiply with $V_i$ $(32, 10, 64)$
  * Result is $\text{head}_i \in (32, 10, 64)$



## Step 4: Concatenate all heads

* Concatenate the outputs from all $h=8$ heads along the last dimension:

$$
\text{Concat}(\text{head}_1, \dots, \text{head}_8) \in (32, 10, 8 \times 64) = (32, 10, 512)
$$



## Step 5: Final linear projection

* Apply output projection matrix $W^O \in \mathbb{R}^{512 \times 512}$:

$$
\text{MultiHeadOutput} = \text{Concat} \times W^O
$$

* Result shape:

$$
(32, 10, 512) \times (512, 512) = (32, 10, 512)
$$



## Summary: Complete flow of dimensions

| Step                                | Output Shape      |
| -- | -- |
| Input embeddings $X$                | (32, 10, 512)     |
| Project to Q, K, V per head         | (32, 10, 64) each |
| Scaled dot-product attention output | (32, 10, 64) each |
| Concatenate all heads               | (32, 10, 512)     |
| Final linear projection $W^O$       | (32, 10, 512)     |


