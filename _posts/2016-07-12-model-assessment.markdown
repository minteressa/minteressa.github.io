---
layout: post
title: Model assessment
date: '2016-07-12 21:16:15 +0200'
categories: project
published: true
---
M'interessa project is, in fact, an information retrieval solution, a binary classification. So, information retrieval metrics must be used in order to assess the model of the project.

If the different document groups generated after an information retrieval process are...

_tp_ = true positive, relevant documents that are retrieved

_tn_ = true negatives, not relevant documents that are not retrived

_fp_ = false positives, not relevant documents that are retrieved

_fn_ = false negatives, relevant documents that are not retrived

...the definitions of the the several information retrieval indicators used to assess that process are as follows:

### Precision

Precision is the fraction of retrieved documents that are relevant. It takes a value between 0 and 1.

_Precision = tp / (tp + fp)_

### Recall

Recall is the fraction of relevant documents retrieved from the total amount of relevant documents. It takes a value between 0 and 1.

_Recall = tp / (tp + fn)_

### Accuracy

Accuracy is the proportion of true results among the total of documents. It takes a value between 0 and 1.

_Accuracy = (tp + tn) / (tp + tn + fp + fn)_

### F-measure (or F1 score)

This measure is a combination between Precision and Recall, an harmonic mean between both metrics. It takes a value between 0 and 1.

_F = 2 x ((Precision x Recall) / (Precision + Recall))_

_F = 2tp / (2tp + fp + fn)_

### ROC (Receiver Operating Characteristic)

It takes a value between 0 and 1.

### References:

1. Precision and recall. _Wikipedia, the free encyclopedia_. <[https://en.wikipedia.org/wiki/Precision_and_recall](https://en.wikipedia.org/wiki/Precision_and_recall)>. [Retrieved on 12th July 2016].
2. Receiver operating characteristic. _Wikipedia, the free encyclopedia_. <[https://en.wikipedia.org/wiki/Receiver_operating_characteristic](https://en.wikipedia.org/wiki/Receiver_operating_characteristic)>. [Retrieved on 12th July 2016].
