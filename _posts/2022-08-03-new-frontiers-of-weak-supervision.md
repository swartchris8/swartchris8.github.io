---
layout: post
title: "Data Centric AI: New Frontiers of Weak Supervision"
categories:
  - Posts
tags:
  - nlp
  - ml
last_modified_at: 2022-08-03T20:59:27-05:00
---

Today I am sharing the key ideas from listening to SnorkelAI's Data Centric AI Panel Discussion: Exploring New Frontiers of Weak Supervision with:
- Frederic Sala, Assistant Professor at University of Wisconsin, Research Scientist at Snorkel
- Stephen Bach, Assistant Professor at Brown University, Research Scientist at Snorkel
- Jason Fries CS, Research Scientist at Stanford,  Biomedical, Research Electronic Health Records
- Fait Poms, Senior applied research scientist Snorkel

**What is weak supervision?**
Aggregate labels and rules with much lower effort than explicit labelling

**How are large language models playing out in weak supervision?**

Foundation models aka large language models have changed the landscape of NLP and weak supervision.

They are very important as they allow you to finetune and adapt these foundation models to your tasks. The foundation models also have some general knowledge based on all of the data they have exposed to.


**New frontiers of weak supervision**

On the output side new techniques to make weak supervision work for diverse tasks such as regressions, image segmentation. 


On the input side weak supervision to different modalities of data: from taxes through images to audio. Finding a good primitive for images or audio is challenging. Foundation models have been helpful to help this.

There's also a lot of opportunity to extract extra signal from multimodal data.

For example Electronic Healthcare Records are structured and unstructured multimodel input that define and describe phenomena about human health. Very challenging to build models on hand labelled individual elements of such data as it's so diverse. Potentially finding the right primitives to represent this could bring a break through using better foundational models and helping doctors model Electronic Healthcare Records.

**Prompting**

Prompting adapt large language models for different tasks

Express what we want the model to do in natural language. For example: input maybe put as a question "What topic is this news article about?" Then use the answer from that as a signal.

This is different from the past where in machine learning we were learning a vector representation of the true label. In a way this is a way to query and access the domain knowledge of these foundational models.

Very exciting as it seems to complement weak supervision very well. Interesting preprint work ([Language Models in the Loop: Incorporating Prompting into Weak Supervision](https://arxiv.org/abs/2205.02318)) with the idea can we use prompting to create weak supervision signals. For example: for a spam classifier: does this message ask about prescription drugs? does this message ask you to do something?

Prompting gives another language to construct tasks. Foundation models have lots of domain knowledge which can be extracted by prompting, weak supervision comes on top of this to tweak the output and fix potential mistakes.

Natural language prompting can be shockingly effective in Poms' experience with a customer recently.

Exciting about prompting functions is the domain expert does not need to work with primitives and allows the domain experts to use way more intuitive text queries.

In practice prompting can be quite useful when working on a task or problem which is not common and where foundation models may not generalise well. Prompting can help you adapt to a particular problem domain. 

Finetuning foundation models can be expensive and models can also forget what they have learned already. Prompting can be an interface to learn new things.