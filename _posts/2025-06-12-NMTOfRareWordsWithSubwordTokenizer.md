---
layout: post
title: "Neural Machine Translation of Rare Words with Subword Units"
date: 2025-06-12
categories: papers
tags: [tokenizer]
description: "Neural machine translation (NMT) models typically operate with a fixed vocabulary, but translation is an open-vocabulary
problem."
image: /images/image1.png
---

<img src="{{ '/poster/tokenizer.png' | relative_url }}">



# Neural Machine Translation of Rare Words with Subword Units

🔗 [**Original Paper (Sennrich et al., 2015)**](https://arxiv.org/pdf/1508.07909)

## Hypothesis

Segmentation of rare words into appropriate **subword units** is sufficient to allow a neural translation model to learn transparent translations, even for **unseen or rare words**.



## Abstract 

* Traditional NMT models struggle with rare or out-of-vocabulary (OOV) words due to limited vocabulary size (typically 30k–50k).
* Prior solutions back off to dictionary lookups, which are brittle and language-dependent.
* This paper proposes using **subword units**, allowing models to construct and translate words from smaller, more frequent components.
* The paper adapts **Byte Pair Encoding (BPE)** — a data compression algorithm — for unsupervised subword segmentation.



## Introduction

* Rare word translation remains a central challenge in NMT.
* Most neural models operate with a limited vocabulary (e.g., 30k-50k word tokens).
* Dictionary-based fallbacks often fail due to:

  * Lack of coverage
  * Context-agnostic translations
  * Poor generalization
* This paper shows that:

  * Encoding rare words as sequences of subword units is a viable alternative.
  * **Byte Pair Encoding** (BPE) can be adapted for unsupervised subword segmentation, helping NMT systems generalize to unseen words.



## Subword Translation

* Many words consist of **multiple morphemes**: prefixes, roots, suffixes, and compounds.
* Translating subwords individually can enable better understanding of compound and rare words.
* **Example**:

  * German **Sonnensystem** → **Sonne** (sun) + **System** (system)
* The model learns to translate each segment, enabling it to:

  * Generalize to new word forms
  * Produce morphologically valid outputs



## Byte Pair Encoding (BPE)

* Originally a compression algorithm that merges the most frequent **adjacent bytes**.
* This paper adapts it to merge the most frequent **character pairs** in text.
* This results in a variable-length subword vocabulary where:

  * Common words remain whole (the, and)
  * Rare words are segmented into common subunits (un, break, able → unbreakable)

<img src="{{ '/images/tokenizer/image1.png' | relative_url }}" alt="BPE process">



## BPE Results

BPE leads to significantly better translation performance on rare words compared to word-level vocabularies or dictionary-based back-off mechanisms.

<img src="{{ '/images/tokenizer/image2.png' | relative_url }}" alt="BPE results graph">


## BPE Implementation

```python
from collections import defaultdict

# Step 1: Prepare corpus
corpus = ["low", "lower", "newest", "widest", "slower", "wildest", "newer", "lowest"]

# Step 2: Convert corpus into vocab of space-separated characters
def get_vocab(corpus):
    vocab = defaultdict(int)
    for word in corpus:
        tokens = list(word) + ["</w>"]
        vocab[" ".join(tokens)] += 1
    return vocab

# Step 3: Count symbol pair frequencies
def get_stats(vocab):
    pairs = defaultdict(int)
    for word, freq in vocab.items():
        symbols = word.split()
        for i in range(len(symbols) - 1):
            pairs[(symbols[i], symbols[i + 1])] += freq
    return pairs

# Step 4: Merge the most frequent pair
def merge_vocab(pair, vocab):
    merged_vocab = {}
    bigram = " ".join(pair)
    replacement = "".join(pair)
    for word in vocab:
        new_word = word.replace(bigram, replacement)
        merged_vocab[new_word] = vocab[word]
    return merged_vocab

# Step 5: Learn BPE until desired vocab size is reached
def learn_bpe(corpus, target_vocab_size):
    vocab = get_vocab(corpus)
    merges = []
    
    # Start with all unique symbols (characters + </w>)
    token_set = set()
    for word in vocab:
        token_set.update(word.split())

    print(f"Initial vocab size: {len(token_set)}")
    
    while len(token_set) < target_vocab_size:
        pairs = get_stats(vocab)
        if not pairs:
            break
        best_pair = max(pairs, key=pairs.get)
        merges.append(best_pair)
        new_token = ''.join(best_pair)
        token_set.add(new_token)
        vocab = merge_vocab(best_pair, vocab)
        print(f"Merged {best_pair} → {new_token}")
        print(f"Vocab size: {len(token_set)}")

    return token_set, merges

# Step 6: Run it
final_vocab, merges = learn_bpe(corpus, target_vocab_size=100)

# Show results
print("\n Final Subword Vocabulary:")
print(sorted(final_vocab))
print(f"\nTotal tokens: {len(final_vocab)}")
```