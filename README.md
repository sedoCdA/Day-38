# Week 07 - NLP Foundations Assignment

## Overview

This assignment explores **word embeddings, semantic similarity, and representation learning** using the ShopSense reviews dataset.

We work with:

* Word2Vec (word-level embeddings)
* BOW and TF-IDF (classical methods)
* Sentence-BERT (context-aware embeddings)

---

## Q1: Word2Vec & Polysemy

### (a) Problem: Polysemy of "cheap"

The word *cheap* has two meanings:

1. Affordable (positive)
2. Low-quality (negative)

**Key Limitation:**
Word2Vec assigns **only ONE vector per word**, regardless of meaning.

So:

* "cheap"  single vector
* Cannot distinguish meaning without context

We compare:

* cosine(cheap, affordable)
* cosine(cheap, flimsy)

---

### (b) Disambiguation using Context

We resolve meaning using:

* Context word embeddings
* Anchor vectors:

  * Affordable anchor = average of ["affordable", "budget", "value"]
  * Low-quality anchor = average of ["flimsy", "poor", "bad"]

Process:

1. Get embeddings of context words
2. Average them → context vector
3. Compare similarity with anchors
4. Choose closest meaning

---

### (c) Window Size Effect

| Window Size | Captures                          |
| ----------- | --------------------------------- |
| Small (2)   | Syntax (grammar, local relations) |
| Large (10)  | Semantics (topic, meaning)        |

Conclusion:

* window=2 syntactic relationships
* window=10 semantic relationships

---

## Q2: Sentence Similarity

### Given:

Review A: "incredible camera but terrible battery life"
Review B: "Battery drains fast, although photos are stunning"

---

### Representations Compared

#### 1. Bag of Words (BOW)

* Counts word overlap
* Ignores meaning
* Fails when words differ

#### 2. TF-IDF

* Weighted BOW
* Still lexical (not semantic)

#### 3. Word2Vec Averaging

* Averages word embeddings
* Captures partial meaning

#### 4. Sentence-BERT

* Context-aware sentence embeddings
* Best semantic understanding

---

### (a) Which Works Best?

Sentence-BERT performs best because:

* Understands "camera" ≈ "photos"
* Understands "terrible battery" ≈ "battery drains fast"

---

### (b) Why BOW Fails

Word overlap:

* Common: "battery"
* Different:

  * "camera" vs "photos"
  * "terrible" vs "drains fast"
  * "incredible" vs "stunning"

BOW sees low overlap → low similarity

---

### (c) Semantic Gap

Semantic gap = difference between **word-level matching** and **actual meaning**

Progression:

BOW -> TF-IDF -> Word2Vec -> Sentence-BERT

* BOW: no semantics
* TF-IDF: importance weighting
* Word2Vec: word meaning
* Sentence-BERT: full sentence understanding

---

## Conclusion

* Word2Vec cannot handle polysemy alone
* Context-based methods improve interpretation
* Sentence-level embeddings are best for semantic tasks

---
