---
layout: post
title: "Musing about why spacy vocabulary size improves NER"
categories:
- Musings
tags:
- bionlp
last_modified_at: 2020-10-15T14:59:27-05:00
---



I was reading the [scispacy paper](https://arxiv.org/pdf/1902.07669.pdf) and came across the below performance of the small and large model on a specific biomedical task:
[![enter image description here][1]][1]

The only difference between the models is:
1. Larger model has a larger vocabulary than small model
2. Larger model has word vectors

Previously I thought spacy NER does not use word vectors but when they are available they do use them

I was wondering how spacy vocabulary size could impact NER performance:

My naive answer would be that the more words are out of vocabulary the harder it is to learn an entity. So if you have a cancer type classification task and all anatomy parts are out of your vocabulary it will be harder to distinguish them for the model. Why do you think vocabulary size impacts NER performance?


[1]: https://i.stack.imgur.com/mMqsU.png
