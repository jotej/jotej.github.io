---
title: Why Care About Deep Generative Modeling?
description: A Primer on Deep Generative Modeling
date: 2026-01-04
image: embeddings.png
weight: 1
---

“We discover the structure of the world by observing it, not by being told the name of every object.” — *Yann LeCun, Yoshua Bengio & Geoffrey Hinton*, **Nature** (2015)

## The cost of compression

Labels are a lossy projection of reality. They are representations of the world filtered through a semantic lens. That lens can simplify what is seen, but it can also discard nuance and structure that may be essential for understanding.

A familiar example is social memory. We often store others as a face and a feeling. That shortcut works surprisingly well, but it comes at a cost. People are complex and change with context. Meeting someone on their bad day can leave a lasting impression, even if it says little about who they are most of the time. If you were told to train a model on faces you personally labeled good or bad, would it learn more about those people or you? Could you reconstruct their complexity from a label like that?

It makes sense, then, to strive for models that learn free of the distortions our biases and simplifications introduce. The goal of generative modeling is not to force a mapping from reality to an artificial simplification of it, but to learn representations that describe the data distribution directly from the data itself.