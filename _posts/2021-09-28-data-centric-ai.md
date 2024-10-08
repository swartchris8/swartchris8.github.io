---
layout: post
title: "Future of Data-Centric AI - Event Summary"
categories:
  - Article
tags:
  - NLP
last_modified_at: 2021-09-28T23:55:00-00:00
---




Had the pleasure to attend the Future of Data-Centric AI from Snorkel today 

The core ideas of datacentricai:

Data curation is the bottleneck, compute and models are commodities To solve this problem re-weight and combine programmable weak supervision signals

I came across Snorkel a couple of years ago it demonstrated a couple cool ideas around programmable labels:
1. thinking about programmable labels as labelling functions
2. use spacy linguistic features in these functions.
Thinking in terms of noisy functions really helps me conceptualise distant supervision and spacy features are great with text.

Originally [Snorkel was an open source project](https://github.com/snorkel-team/snorkel) for programmatic data labelling.
Today the team is focusing more and more on Snorkel flow, a commercial offering to reduce the cost of data labelling.

As weak supervision is becoming more and more popular there are some interesting open source tools out there for leveraging noisy data:  
[Interactive Model Iteration with Weak Supervision and Pre-Trained Embeddings](https://github.com/HazyResearch/epoxy)  
[Interactive weak supervision](https://github.com/benbo/interactive-weak-supervision)

Hoping to share more about using them in the next couple month!