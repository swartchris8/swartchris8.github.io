\---

layout: post

title: "Musing about why spacy vocabulary size improves NER"

categories:

 \- Musings

tags:

 \- bionlp

last_modified_at: 2020-10-04T20:59:27-05:00

\---



I was reading the scispacy paper and came across the below performance of the small and large model on a specific biomedical task:
[![enter image description here][1]][1]

The only difference between the models is:
1. Larger model has a larger vocabulary than small model
2. Larger model has word vectors

As far as I know word vectors are only used for similarity operations. Hashed embeddings from the vocabulary are used to initialise the vectors using a CNN to train them for NER.

So then I was wondering why would a larger vocabulary improve performance?

My naive answer would be that the more words are out of vocabulary the harder it is to learn an entity. So if you have a cancer type classification task and all anatomy parts are out of your vocabulary it will be harder to distinguish them for the model


[1]: https://i.stack.imgur.com/mMqsU.png