---
layout: post
title: "Tokenizers in LLMs"
date: 2025-06-12
categories: blog
tags: [llm]
description: "Tokenizer breaks down text into smaller units, called tokens, which can be words, subwords, or even individual characters"
---

<img src="{{ '/poster/tokenizer.png' | relative_url }}">


# Tokenizers in NLP

## What is a Tokenizer?

A **tokenizer** is a tool that splits input text into smaller units called **tokens**, which are then used as inputs to NLP models.

There are three common types of tokenization strategies:

<img src="{{ '/images/tokenizer_p1.png' | relative_url }}">

**Subword tokenization** has emerged as the standard in large language models due to its ability to:

* Handle unknown or rare words
* Maintain a compact vocabulary
* Generalize better across morphology (e.g., “talked”, “talking”, “talks”)


<br>

---


## Subword Tokenizers Overview

Subword tokenizers sit between character-level and word-level tokenizers, breaking text into **meaningful chunks**, often learned from training data.

### Popular Algorithms:

* **Byte-Pair Encoding (BPE)** – used in GPT, RoBERTa
* **WordPiece** – used in BERT
* **Unigram LM** – used in XLNet, ALBERT
* **SentencePiece** – implements BPE or Unigram and supports raw text input


<br>

---

## Byte-Pair Encoding (BPE) – In Depth

### How It Works

1. **Start with a character-level vocabulary**: e.g., `**'e', 'x', 'a', 'm', 'p', 'l', 'e']**
2. **Count frequent adjacent pairs** across your training corpus.
3. **Merge** the most frequent pair into a new token.
4. **Repeat** until a vocabulary size limit is reached.

### Example – Training Phase

Given a toy dataset:

```
low low lower newest widest
```

**Initial tokenization**:

```
l o w   l o w   l o w e r   n e w e s t   w i d e s t
```

**Count most frequent pairs** (e.g., **l o**, **o w**, **e s**...).

Suppose **l o** is the most frequent → Merge → **lo**

Update all texts:

```
lo w   lo w   lo w e r   n e w e s t   w i d e s t
```

Repeat merging like: **lo** + **w** → **ow**, **low** + **e** → **lowe**, ...

Final learned subword vocabulary might include:

```
["l", "o", "w", "e", "r", "n", "s", "t", "lo", "low", "lowe", "new", "est", "wid", "wide"]
```



### Inference (Tokenization at Test Time)

Let’s tokenize the word **lowering**.

Step-by-step:

* Greedy left-to-right matching:

```
lowering → low + er + ing (if in vocab)
```

If **lower** is in the vocabulary but **lowering** is not, then:

```
lowering → lower + ing
```

If **lower**, **ing** aren't in vocab, fallback might be:

```
lowering → l + o + w + e + r + i + n + g
```

So **granularity depends on the training data and merges**.


<br>

---

## WordPiece – A Smarter Variation

### How It Works

* Like BPE, WordPiece builds a subword vocabulary.
* But instead of merging based on frequency alone, it uses a **likelihood-based approach**.
* It finds a tokenization that **maximizes the likelihood of the entire sentence** using a probabilistic model.

### Example

Let’s say the sentence is:

```
The runner was unbelievable.
```

And your model has the following subword vocabulary:

```
["the", "run", "##ner", "was", "un", "##believ", "##able", "."]
```

Then WordPiece tokenizes as:

```
["the", "run", "##ner", "was", "un", "##believ", "##able", "."]
```

### Special Notation:

* WordPiece uses **##** to mark that a token is a **suffix** (i.e., not the start of a word).
* Helps preserve word boundaries for downstream models.

---

## BPE vs. WordPiece – Key Differences

<img src="{{ '/images/tokenizer_p2.png' | relative_url }}">

---

## Summary

- Tokenization is the **gateway** to building any NLP model.

- Subword tokenization helps handle vocabulary diversity and OOV (out-of-vocabulary) words.

- BPE and WordPiece are the most popular subword strategies, each with its own advantages.



## Want to Try It Yourself?

Try tokenizing with Hugging Face’s tokenizer API:

```python
from transformers import AutoTokenizer

tokenizer = AutoTokenizer.from_pretrained("bert-base-uncased")
tokens = tokenizer.tokenize("The unbelievable runner jumped.")
print(tokens)
# Output: ['the', 'un', '##believ', '##able', 'runner', 'jumped', '.']
```
