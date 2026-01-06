---
title: Why Care About Deep Generative Modeling?
description: A Perspective on Deep Generative Modeling
date: 2026-01-04
image: embeddings.png
math: true
weight: 1
---

## The cost of compression

“We discover the structure of the world by observing it, not by being told the name of every object.” — *Yann LeCun, Yoshua Bengio & Geoffrey Hinton*, **Nature** (2015)

Labels are a lossy projection of reality. They are representations of the world filtered through a semantic lens. That lens can simplify what is seen, but it can also discard nuance and structure that may be essential for true understanding.

A familiar example is social memory. We often store others as a face and a feeling. That shortcut works surprisingly well, but it comes at a cost. People are complex and change with context. Meeting someone on their bad day can leave a lasting impression, even if it says little about who they are most of the time. If you trained a model on images of people you personally labeled good or bad, would it learn more about them or you? Could you reconstruct who they are from a label like that?

It makes sense, then, to strive for models that learn free of the distortions our biases and simplifications introduce. The goal of generative modeling is not for models to conform to hand-crafted beliefs about the data, but to learn their own beliefs.

## Labels as imposed beliefs

The following is a quick way to see why training only a classifier can be an unreliable way to learn the structure of the data distribution:

We have labeled pairs \(\{(x_i,y_i)\}_{i=1}^n\). The usual conditional MLE objective is
\[
\hat\theta_{\text{MLE}}=\arg\max_{\theta}\prod_{i=1}^n p_{\theta}(y_i\mid x_i).
\]

Now ask a broad question. After training \(p_\theta(y\mid x)\), what can we actually say about the data distribution \(p(x)\)?

Bayes rule gives
\[
p(y\mid x)=\frac{p(x\mid y)p(y)}{p(x)}
\quad\text{and}\quad
p(x)=\sum_{y'\in\mathcal Y} p(x\mid y')p(y').
\]
So we can also write
\[
p(y\mid x)=\frac{p(x\mid y)p(y)}{\sum_{y'\in\mathcal Y} p(x\mid y')p(y')}.
\]

Now connect this to labels. In most supervised settings, labels are coarse. Many distinct observations \(x\) share the same label \(y\). That means there are typically many different ways to choose class-conditional densities that are consistent with the same learned conditional \(p_\theta(y\mid x)\). To make this explicit, pick any such choice and denote it by \(\{q_{\phi}(x\mid y)\}_{y\in\mathcal Y}\). Then
\[
p_{\theta}(y\mid x)=\frac{q_{\phi}(x\mid y)p(y)}{\sum_{y'\in\mathcal Y} q_{\phi}(x\mid y')p(y')}.
\]

The key point is that this \(\{q_{\phi}(x\mid y)\}_{y\in\mathcal Y}\) is not unique. Many different families can induce the same conditional \(p_{\theta}(y\mid x)\). So fitting \(p_{\theta}(y\mid x)\) does not pin down a unique marginal
\[
p(x)=\sum_{y\in\mathcal Y} q_{\phi}(x\mid y)p(y).
\]

If the goal is for the model to understand the structure in the observations, we should train with an objective that directly targets the data distribution \(p(x)\).
