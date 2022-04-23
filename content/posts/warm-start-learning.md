---
title: "Warm-start Learning"
date: 2022-03-22T22:54:35-07:00
draft: True
---

Let's say you're training a text classification system, for example, to automatically classify support tickets into buckets, "urgent" and "not urgent". You have historical data on the support tickets and some labels on whether or not it was urgent.

The goal is to develop a useful predictive model to help triage these tickets.

Below, we describe a handful of techniques that are worth considering when building a binary model.

The main definition we will have is _warm-start_ learning, as this is the category of techniques I will describe. These techniques are characterized by using a pretrained neural network language model, such as [this one](https://huggingface.co/sentence-transformers/all-MiniLM-L12-v2) from Microsoft. 

1. **Full tuning** Freeze none of the weights, run your speciic data through adjust the weights based on gradients computed on cross entropy error, exactly like training a neural network on a binary classification task. Read more about fine tuning in pytorch [here](https://huggingface.co/docs/transformers/training).

1. **Last layer tuning** Freeze all of the weights except the second-to-last last layer, and do the same as the previous step. This is like running logistic regression on the embeddings produced on the pretrained model.

3. **Transfer learning** A more general case of the previous step is Transfer learning. This time, use the embeddings and apply any classifier. So take it out of the neural net and use any classifier, not just Logistic Regression.

3. **Nearest neighbor search** Here don't run any training, 1) embed the result and 2) be ready to determine whether the majority of top-k, or top-k% nearest neighbors are "urgent"; if so, label them urgent. k=1 may be a good starting point. Or, time permitting, a validation procedure can be done to select k.

For most data scientists and machine learners, the days training of models from scratch (i.e. determining the "best" way to randomly initialize parameters), are over. Nowadays, warm-start learning is what we should expect with complex data. It's now a question of which warm-start technique to employ at a given use-case.

Even the pretrained model referenced in this article was fully tuned using a pretrained SOTA-level network.

Where can I find some 2022 examples of training large neural networks (100+ million parameters), _not_ from pretrained networks, in industry?
