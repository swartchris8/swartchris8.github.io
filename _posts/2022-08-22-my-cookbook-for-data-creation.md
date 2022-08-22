---
layout: post
title: "My cookbook for data creation"
categories:
  - Posts
tags:
  - nlp
  - ml
last_modified_at: 2022-08-22T22:38:27-05:00
---

Last Friday I had the pleasure of [speaking with Alexey Georgev on DataTalks.club about Dataset creation](https://www.youtube.com/watch?v=QggWydGrWoo).
I am sharing my data creation process here,
so you don't need to watch me talk for an hour.

My road to successful data creation
1. define success in business terms
2. map the data with stakeholders for buy in
3. rapid prototype from data to deployment
4. iterate on dataset creation

Techniques to get more data bang for buck:
1. weak supervision
2. active learning

Considerations around dataset creation:
1. in-house vs crowdsourcing

Tool recommendations

## My cookbook for data creation

### Defining success in business terms

**A good dataset is one that creates business value.** Making sure stakeholders, domain experts, and engineers
are on the same page is hard.  I find sharing a mock of the model and data 
can really help move stakeholders understand what's possible. Sharing an
initial annotations with stakeholders can give
quick feedback around conceptual errors and reduce the risk of overhyping
the project.

![Figure 3 from the paper](/assets/ml_hype_train_wreck.jpg)

### Map the data with stakeholders for buy in

**I show the data to stakeholders as a user interview.** I am looking to see
how usable is the data and strengthen my conceptual understanding of the
business problem. It's a successful interview if I know more about how 
experts understanding of the problems. So for example for Comtura to 
model sales processes, whenever I hear the importance of qualification
I would link that with qualification methodologies. 

I like having 2 mindmaps
one with the expert's conceptual view and one view around how can these
expert concepts be modelled. For example maybe I will model sales
qualification as a span classification problem where some spans are related
to sales qualification, maybe instead I model it as a paragraph level
document classification problem.

### Rapid prototype from data to deployment

Perfect is the enemy of done. As a data scientist there are so many 
interesting ways a model could be improved. If you think your model is 
feasible then there's no need for further improvements until it hits 
production. Speeding up the data -> model -> business value flow is essential
otherwise how do you know if your data is creating business value?

### Iterate on dataset creation

If you feel you are on the right track based on your prototype you can
start refining your dataset creation process based on expert and user 
feedback. I like to have 3 steps in creating a dataset:
1. annotation
2. data review
3. dataset creation feedback

#### Annotation
Creates labelled data

#### Data review
Review the created data qualitatively with a supervisor checking output periodically
and quantitatively with inter annotator agreement and model metrics

#### Dataset creation feedback
I like having an annotation booklet. **The annotation booklet is a living 
document where I keep task defintions, ambigous examples, and past discussions.** 
With periodic feedback sessions where we discuss challenging samples and process
improvement possibilities.

## Techniques to get more data bang for buck

**Weak supervision** is a way to generate weak labels for unlabelled
data programatically. Weak supervision has the most potential to improve 
your dataset creation process. Labelling functions generate weak labels from
unlabelled data. A labelling function can have good signal for 2-3% of your 
data. With such a wide coverage labelling functions can improve performance
a lot. Labelling functions can also be easily explained to domain experts
allowing experts to improve your labelling functions.

**Active learning** is a form of model in the loop annotation where low confidence
samples are annotated to improve model confidence. I have used prodigy in the past
for this. It worked sometimes, sometimes not.

## Considerations

### In-house vs crowdsourcing

For quick prototype or if quality not so important crowdsourcing works well as
you can scale your tasks to a large pool of annotators. I prefer in-house
annotation though as it allows you to build a relationship with annotators.
You can retain the best performing annotators and iterate on your annotation process
way easier with in-house annotation. In my experiece the long term 
cost / sample also favours in-house annotators as crowdsourcing requires
2/3x more levels of review or annotation due to low inter annotator agreeement.

## Tool recommendations

Open source:
I recommend [snorkel](https://www.snorkel.org/) to get started with weak supervision.
[Doccano](https://doccano.github.io/doccano/) and [Label Studio](https://labelstud.io/) are great general annotation interfaces

Paid:
[Prodigy](https://prodi.gy/) is a great annotation tool with active learning support
from the creators of spacy
