---
title: "Nlp Classification"
date: 2022-04-13T18:26:21-07:00
draft: true
---

Freeze encoder E weights, train logistic on embeddings from your ticket text data (Approach 1)
Train your model from pre-trained encoder E + logistic classifier (Kevin’s way)
Trained encoder/decoder unsupervised on ticket data and made a new encoder E’
Freeze E’, train logistic on embeddings from ticket (Approach 2?)
Train whole model from E’ + logistic in one step no weights frozen


