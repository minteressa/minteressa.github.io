---
layout: post
title: ETL from Kafka logs
date: '2016-07-01 16:01:15 +0200'
post_author: Mario Alberich
categories: project
published: true
---
## Objective
The main objective is to fetch the data from Kafka and perform some (more or less sophisticaded) filters over the gathered tweets in order to:<!–break–>

* Remove tweets from non-supported languages
* Remove tweets that don't include at least one URL.
* Remove duplicate tweets (although keeping record of the replied items).

How are we dealing with it? Let's see...

## Architectural landscape

<img class="img-responsive pull-right" width="40%" src="/assets/images/kafka-logo.jpg" alt="{{ post.title }}"/>So by now we've got a Scala script that gathers tweets and stores them into a Kafka instance, under the topic `raw_tweets`.  This is where the tweets are stored for the time that Kafka is getting configured to (7 days as default, but probably we'll configure it to store for less time).

So now we should fetch each stored tweet, and process it.  But we don't want to perform a monotlythic operation, but a more modular one, and leverage over Kafka's features to get it done.

## Workflow + new topics

Then, what is getting done by now is as follows:
* A script gathers the `raw_tweets` and checks whether the tweet includes at least one URL. If so, the tweet is sent to the `url_tweets` topic.
* From `url_tweets` topic, another script checks if the tweet is written
* When the tweet has enough information, we need to check whether this is a (near-)duplicate from a previous one.

There's a specific blog post regarding the [Near-duplicate detection](near-duplicate-detection) of tweets (ND for short from now onwards). By now, let's focus on the way that all this gets handled.

So each worker on the ETL process, there's a topic from which consume, and a topic to which produce new filtered items. All this creates a pipeline that reaches a point where only the "valid" tweets arrive. We'll see whether we get some data that backs up the need of such filtering process, but this will be at the end of the project.

So the data cleaning pipeline waits for a good schema, but more or less it is:

* Scala script sends the tweet to the "raw_tweet" topic on Kafka.
* url-filter node listens on "raw_tweets" topic, and sends the valid URLs to "url_tweets"
* lang-filter node listens on "url_tweets" and forwards the tweets in a valid language to their corresponding topics:
** english: "es_tweets"
** spanish: "en_tweets"
* Two near-duplicate detectors (one for each language) listens on the "es_tweets"/"en_tweets", If the tweet is considered unique enough, it's sent to the "unique_tweets"

Plase note that the ND detection is language-specific. Although a priori it will make the filtering process more accurate, it remains to be confirmed for the case of tweets.

So after we process all the data, we get a clean tweet, and this needs to be enriched. We'll leave this topic for another post, though.

## From the if...then to probabilistic filtering

One of the interesting points of the ETL process above is the process how the tweets can be filtered in/out. The URL filtering is performed by simple programmatic sequence control (if..then, plainly stated), and so does the language filter, by simply checking the language attribute provided by twitter.

That said, should we trust the language provided by Twitter? Is it possible that the language provided is english but the text is in German, Korean, or another language? We can't be sure of that.  And this leads to a second type of filters, based on probabilistic rules.

In the case of the language, we could get the text of the tweet and check whether the word frequency in those tweets are more usual in one language or another, and thus infer which language is actually the user writing the tweet on.

As with many other features of the pipeline, we're running out of time and thus we'll be unable to implement a solution for that... But it was worth to mention.
