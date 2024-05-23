---
layout: post
title: "Talk Summary - RAG for a medical company: the technical and product challenges by Noe Achache"
categories:
  - Posts
tags:
  - ML
  - NLP
last_modified_at: 2024-05-22T10:21:30-05:00
---

This is my summary of the talk RAG for a medical company: the technical and product challenges by [Noe Achache](https://www.linkedin.com/in/noe-achache/) delivered at PyData Berlin 2024.

### Product background

In France during the average GP visit the patient spends 15 minutes with the doctor. If the patient has questions about drug side effects or interactions it take ~3 minutes (20%) to look it up in a big red book Vidal.

Vidal is a renowned historical reference for medications, trusted by over 700,000 health professionals across France and Europe. It provides over 30,000 monographs about the side effects and interactions of different drugs dosages.

**Product Discovery questions**

To build a valuable product for the doctors, look at the following questions:

| Value       | Does the doctor perceive the benefit in using it?   |
| ----------- | --------------------------------------------------- |
| Usability   | Will doctors be able to use it?                     |
| Feasibility | Can we build and maintain this product?             |
| Viability   | Is this solution viable from a business standpoint? |

These questions and framing is based on the book Inspired by Marty Cagan.

Focusing on usability, the goal is to make the solution work for doctors.

Assumptions:

1. AI never 100% reliable → cite sources
2. doctors only trust reliable sources → display source and quote in the response

### Solution

Example of the content of interactions

<br>
<br>

1. Question: How long should I take 💊 Eliquis?
2. Rephrase question: How long should I take Eliquis?
3. Highlight documents with hits, which can be manually selected:

- [x] Eliquis 5 mg dosage
- [ ] Aspirin
- [ ] etc.

1. Return extractive answer from source document

   GPT 4 answer: **Take Eliquis every hour for 12 hours.**

   Relevant source:

   “Eliquis is a common treatment for malaria.

   Eliquis 5 mg should be taken once an hour for 12 hours.”

<br>
<br>

❌ Initial approach was just use ChatGPT, this failed due to no source.

Medical advice is high trust.

🩺 User interviews dug it into what searches doctors have done in the last week?

Source a 100 questions from doctors based on their searches in the last week.

This 100 question dataset is the core evaluation set.

The initial approach also performs very poor on the evaluation data set:

👌 OK - answer accepted by doctor

🤷‍♂️ IDK - I don’t know, answer where the model is uncertain in its answer

😵 KO - knocked out, answer is wrong

![Initial evaluation](/assets/rag/rag-initial.png)

### Chunking challenges

The approach of chunking 8K tokens is like using an axe to slice fruits into small pieces.

The pieces of fruit (vector embeddings) you get are too big and often mixed together which means it’s harder to find the fruit you are looking for (query vector).

Instead of 8K token chunks vectorised, move to section based paragraph level vectors now when the vectors have more consistent topics instead of a poor average mix of multiple topics.

This led to a substantial improvement in performance:

![Paragraph vector evaluation](/assets/rag/rag-smaller-vectors.png)

Performance is still not good enough how to reduce the red slice of the pie?

A business stakeholder looking at the prompt results in the playground had an idea:

Include the International Nonproprietary Name (INN) of the drugs as well

This allowed finding generic and molecule names with the same vector as the INN.

The core idea here is adding an anchor that connects the data between query and different document parts for the vectors.

Instead of using an API to link to the INN id, just use ChatGPT to generate it for quick prototyping.

This was a huge improvement:

![Using ID in reframed questions](/assets/rag/rag-reframe-qustions.png)

Finally tweaking the prompts a bit more led to no wrong answers:

![Final evaluation](/assets/rag//rag-final-gpt4.png)

This is the arch of the final solution:

![Solution arch](/assets/rag/rag-arch.png)

### Trying Mixtral vs GPT

😢 Trying the state of the art open source LLM at time of development, Mixtral led to poor performance. OS LLMs not there yet vs GPT4

![Mixtral eval](/assets/rag/rag-mixtral.png)

### Architecture notes

Chat interface implement with Chainlit for quick chatbot UI.

Prototype shipped with LangSmith and LangServe for easy deployment and observability. We have very similar capabilities to the ones demoed in honeycomb.
💡 One thing missing from our honeycomb solution is with LangSmith they have a **1 click button to export a trace context to an interactive prompt playground**. This could be good to implement, for debugging and allowing more prompt collab.

### Improvement opportunities

Some usability learnings, discovered during development:

How does the tool choose the docs? I want to select them → make them selectable

Monograph is too long, don’t see where the info comes from → highlight source section

Open usability challenges

1. Oh I need to ask a question?
2. Dr feels attacked by rephrasing the question

Need more automatic evaluations:

1. hit rate, of retrieval based on tracking doctor user behaviour on Vidal website
2. Auto score with LLM as a judge
