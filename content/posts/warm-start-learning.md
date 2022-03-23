---
title: "Warm Start Learning"
date: 2022-03-22T22:54:35-07:00
draft: False
---

Let's say you're training a text classification system, for example, to automatically classify support tickets into buckets, "urgent" and "not urgent". You have historical data on the support tickets and some labels on whether or not it was urgent.

The goal is to develop a useful predictive model to help triage these tickets.

Below, we describe a handful of techniques that are worth considering when building a binary model.

The main definition we will have is _warm-start_ learning, as this is the category of techniques I will describe. What characterizes these techniques is that they start with a pretrained language model, such as [this one](https://huggingface.co/sentence-transformers/all-MiniLM-L12-v2) from Microsoft (note, it happens to have been created from another pretrained model). 

1. **Full fine tuning** Freeze none of the weights and simply run your speciic data through to, exactly like training a neural network on a binary classification task (eg. Use cross entropy loss, etc.). Read more about fine tuning [here](https://huggingface.co/docs/transformers/training).

2. **Partial fine tuning** Freeze all of the weights except the second-to-last last layer, essentially running logistic regression on the embeddings produced.

3. **Nearest neighbor search** Here don't run any training, 1) embed the result and 2) be ready to determine whether the majority of top-k, or top-k% nearest neighbors are "urgent"; if so, label them urgent. Of course a reasonable value for k needs to exist, Could simply be k=1 to start.

In this post, I will describe a handful of techniques, with minimal commentary.
