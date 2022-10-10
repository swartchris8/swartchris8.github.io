---
layout: post
title: "Crunch Conf -- Weak Supervision Workshop"
categories:
  - Posts
tags:
  - NLP
last_modified_at: 2022-10-05T10:55:00-00:00
---

I had the pleasure of running a workshop on Weak Supervision at Crunch Conference in Budapest on 5/10/2022. Let me share a summary of the workshop here:

With simple and efficient out-of-the-box machine learning APIs finetuning and deploying machine learning models has never been easier.
For many companies the larger challenge is understanding the goal posts of machine learning projects and the lack of labelled data.
Weak supervision can help with labelling data more efficiently or finetune your models on noisy labelled data.

![Weak supervision](/assets/weak_supervision_slide.png)

The workshop used `skweak` a `spacy` based weak supervision library to demonstarte how to use labelling functions to generate noisy labelled data.
`skweak` uses labelling functions to generate noisy labels for example:

```python
from skweak.base import SpanAggregator

class MoneyDetector(SpanAggregator):
    def __init__(self):
        super(MoneyDetector, self).__init__("money_detector")

    def find_spans(self, doc):
        for tok in doc[1:]:
            if tok.text[0].isdigit() and tok.nbor(-1).is_currency:
                yield tok.i-1, tok.i+1, "MONEY"

money_detector = MoneyDetector()
```

This labelling function extracts any digits that are preceeded by a currency.

![Money detector](/assets/tall_giraffe_money.png)

`skweak` allows you to combine multiple labelling functions using `spacy` attributes or other methods of choice.

Using labelling functions has a number of advantages:
1. 💪 larger coverage, a single labelling function can cover many samples
2. 🤓 involving experts, domain expert annotation is expensive, domain expert labelling functions are more economical due to coverage
3. 🌬️ adopting to changing domains, labelling functions and data assets can be adapated to changing domains

[Workshop Slides](https://docs.google.com/presentation/d/1mTF9JvwBwVj27e9pKP7sQ7gOpb343YaeGr0Y0G7A9i0/edit?usp=sharing)

[Example Kaggle Notebook applying skweak to smoker not smoker detection](https://www.kaggle.com/code/chrisswartml/smoker-not-smoker)
you will need to verify your phone number and set the Internet connection setting on Kaggle to run the notebook

[skweak documentation](https://github.com/NorskRegnesentral/skweak/wiki/Step-1:-Labelling-functions)