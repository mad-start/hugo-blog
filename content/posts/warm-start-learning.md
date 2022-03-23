---
title: "Warm-start Learning"
date: 2022-03-22T22:54:35-07:00
draft: False
---

Let's say you're training a text classification system, for example, to automatically classify support tickets into buckets, "urgent" and "not urgent". You have historical data on the support tickets and some labels on whether or not it was urgent.

The goal is to develop a useful predictive model to help triage these tickets.

Below, we describe a handful of techniques that are worth considering when building a binary model.

The main definition we will have is _warm-start_ learning, as this is the category of techniques I will describe. These techniques are characterized by using a pretrained neural network language model, such as [this one](https://huggingface.co/sentence-transformers/all-MiniLM-L12-v2) from Microsoft. 

1. **Full fine tuning** Freeze none of the weights and simply run your speciic data through to, exactly like training a neural network on a binary classification task (eg. Use cross entropy loss, etc.). Read more about fine tuning [here](https://huggingface.co/docs/transformers/training).

1. **Last layer tuning** Freeze all of the weights except the second-to-last last layer, and do the same as the previous step. This is like running logistic regression on the embeddings produced on the pretrained model.

3. **Transfer learning** A more general case of the previous step is Transfer learning. This time, use the embeddings and apply any classifer. So take it out of the neural net and use any classifier, not just Logistic Regresssion.

3. **Nearest neighbor search** Here don't run any training, 1) embed the result and 2) be ready to determine whether the majority of top-k, or top-k% nearest neighbors are "urgent"; if so, label them urgent. k=1 may be a good starting point. Or, time permitting, a validation procedure can be done to select k.

I assume the thesis of HuggingFace was something like:

 Model training is hard and takes lots of infrastructure. Infrastructure is costly and push button neural network training is not yet democratized with models of scale. Models are large with - in a growning number of cases and domains beyond NLP, billions of parameters.

For most of us data scientists and machine learners, the days training of models from scratch (i.e. determining the "best" way to randomly initialize parameters), are over. Noadays, warm-start learning is what we should expect with complex data. It's now a question of which warm-start technique to employ at a given use-case.