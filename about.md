---
position: 1
layout: page
title: About
permalink: about.html
---

## What's the need that tries to fulfill this project?

### Avoid the noise...

Each second, Twitter publishes around [7k tweets](http://www.internetlivestats.com/twitter-statistics/). It's not possible for a single person to follow all this amount of conversation, and even a 100-fold amount of tweets would require full atention along all the day, leaving no time for processing all the information received.

Moreover, those tweets may include a lot of noise for any individual, no matter whether this noise is caused by fake information, spam, automated bots or a combination of them. But it can also be possible that the published tweet, even if it's reasonably trustable, may not be relevant for our informational needs.

### ...While finding the relevant tweets

What we try to perform on this project is to build a personalized model for a given topic, chosen by the user. The model starts from a basic set of *seed tweets* selected by the user.  Those tweets can be retrieved either from its twitter timeline or from a search performed over the published tweets.

## How are we dealing with it?

### Training, cross-validation and testing on-the-fly

So far, the model starts to learn by storing the human selections (each tweet is marked as relevant or not). The learning is performed progressively, trying to get as much accuracy as possible and then trying to show only the most relevant tweets. After the model gets a fairly good internal accuracy (the model predicts from the beginning, but not filtering out tweets), it starts to filter out tweets while still keeps learning from the incoming tweet stream.

So you can see that there's an analogy for the three stages before:
* The model starts by learning the selected tweets, which means that it's creating the labeled set. This is where the model training starts.
* When the model is comparing its own prediction to the user selection, the process being done is a cross-validation.
* when the model is not learning anymore but the

After some point (provided by the model internal metrics, or perhaps from the user), the model will be supposed to be *mature* enough to be selecting the tweets while not learning at the same pace as before.

### Batch learning vs. Online learning

Although what was explained above was a bit of the *classical* approach in Machine Learning, we think that this model can be brought further by using or implementing some kind of [online learning algorithm (Online machine learning)](#). This would have the following advantages:
* The feedback to the user is faster in terms of tweets that need to be processed before the model starts to predict.
* It's more adaptative, meaning that the model can update itself along the time (which is very good for humans!).
* As far as there's no need to use the whole dataset at once, the required amount of memory to perform such calculations drops significantly, depending on the block size.

Online learning has a major drawback, though: not all the current machine learning algorithms can be used in an online learning fashion, or perhaps their implementations are not effective enough. This is one of the points to review along the project.

### Information sources

On one hand, we'll connect to the public version of the [Twitter Stream API][twitter-stream-sample-api], and retrieve up to the 1% of the overall generated tweets (~70 tweets/sec).  Those tweets and the web pages that are linked from them will be used to traing and test the model.

At first it was expected to include more information sources, like RSS feeds or similar, but given the time contraints and that the Twitter source by itself includes a lot of challenges, we've limited the scope of the project.

[online-learning-algorithm]: https://en.wikipedia.org/wiki/Online_machine_learning
[twitter-stream-sample-api]: https://dev.twitter.com/streaming/reference/get/statuses/sample