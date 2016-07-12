---
layout: post
title: Model assessment
date: '2016-07-12 21:16:15 +0200'
categories: project
published: true
---
M'interessa project is, in fact, an information retrieval solution. So, information retrieval metrics must be used in order to assess the model of the project.

tp = true positive, relevant documents that are retrieved
tn = true negatives, not relevant documents that are not retrived
fp = false positives, not relevant documents that are retrieved
fn = false negatives, relevant documents that are not retrived

### Precision

Precision is the fraction of retrieved documents that are relevant.

Precision = tp / (tp + fp)

### Recall

Recall is the fraction of relevant documents retrieved from the total amount of relevant documents.

Recall = tp / (tp + fn)

### Accuracy

Accuracy = (tp + tn) / (tp + tn + fp + fn)

### F-measure (or F1 score)

This measure is a combination between Precision and Recall, an harmonic mean between both metrics.

F = 2 x ((Precision x Recall) / (Precision + Recall)) = 2tp / (2tp + fp + fn)

### ROC

Also knonw as Receiver Operating Characteristic

References:

1. Precision and recall. 'Wikipedia, the free encyclopedia'. <[https://en.wikipedia.org/wiki/Precision_and_recall](https://en.wikipedia.org/wiki/Precision_and_recall)>. [Retrieved on 12th July 2016].
2. Receiver operating characteristic. 'Wikipedia, the free encyclopedia'. <[https://en.wikipedia.org/wiki/Receiver_operating_characteristic](https://en.wikipedia.org/wiki/Receiver_operating_characteristic)>. [Retrieved on 12th July 2016].
