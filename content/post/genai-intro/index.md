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

The following derivation is meant to build intuition for why discriminative modeling can be a lousy way for a model to learn the structure of the data distribution.

Under the usual i.i.d. assumption for labeled data $\\{(x_i,y_i)\\}_{i=1}^n$, the MLE is:

$$
\hat{\theta}_{\mathrm{MLE}}=\arg\max_{\theta}\;\prod_{i=1}^{n} p_{\theta}(y_i \mid x_i).
$$

Let’s reframe the labels as given beliefs $y$ attached to observations $x$. From this view, we can see a conceptual Bayes decomposition of the same conditional likelihood, written in generative terms. Assuming $y$ takes values in a small discrete set $\mathcal{Y}$, we take the prior to be fixed from the dataset, so it does not depend on $\theta$. Bayes’ rule then gives:

$$
\hat{\theta}_{\mathrm{MLE}}
=\arg\max_{\theta}\;\prod_{i=1}^{n}\frac{p_{\theta}(x_i \mid y_i)\,p(y_i)}{p_{\theta}(x_i)}
=\arg\max_{\theta}\;\prod_{i=1}^{n}\frac{p_{\theta}(x_i \mid y_i)}{\sum_{y\in\mathcal{Y}} p_{\theta}(x_i\mid y)\,p(y)}.
$$

Now consider what it would mean to learn $p_{\theta}(x_i \mid y_i)$ under this objective. A hand-crafted belief $y$ can correspond to countless observations $x$. We cannot realistically describe every relevant nuance manually, and even if we tried, what would be the right way to embed the beliefs so the model generalizes? More fundamentally, fitting $p_{\theta}(y\mid x)$ does not define a unique $p_{\theta}(x)$, so there is no single generative story for the model to recover.

A better approach is to let the model learn the structure of the data first, and let its own internal beliefs about the data form from what it observes.
