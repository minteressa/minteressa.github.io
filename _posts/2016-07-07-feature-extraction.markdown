---
layout: post
title: Feature extraction
date: '2016-07-07 23:16:15 +0200'
categories: project
published: true
---
The features extracted from each tweet and used in the model are based on the API reference page about the Tweet objects ([https://dev.twitter.com/overview/api/tweets](https://dev.twitter.com/overview/api/tweets)), we’ve got the following attributes into each Tweet:

- contributors: List of Contributor objects showing the users that are allowed to contribute into such account.
- coordinates: 
- text:
- retweet_count:
- truncated:
- ..

To all that features we have added some new:

1. Only-text tweet: processed version of the original tweet (attribute text in the tweet model) that was been cleaned out of entities and stopwords.
2. Only-hashtag: textualized version of the hashtags, concatenated with a space separation between them, and without the hash (#) sign.
3. Only-text tweet vector: a vectorized version of nf_tweet_text. The variable will exist only as an object.
4. Only-hashtag tweet vector: a vectorized version of nf_tweet_hashtags.  The variable will exist only as an object (the vectorized variables).
5. Tweet vector: Vectorized representation of the words’ frequency into the documents (tweets), after removing hashtags, urls and mentions.
6. Language: inferred tweet language based on its content by analyzing the text and evaluating the proximity against each language corpus. We’ll not take into account the language provided by the Tweet itself.
7. Number of Hashtags: amount of hashtags into the tweet.
8. Number of Mentions: amount of twitter accounts mentioned into the tweet.
9. Number of URLs: amount of twitter urls referenced into the tweet.
10. Position of first entity into the tweet: relative position of the first entity (whether url, hashtag or mention) into the text of the tweet, counting from the end of the tweet. This way the sooner the mention, the bigger the value (first character = 1).
11. Position of first hashtag/url/mention into the tweet: for each of the entity types that will be treated, we get the first appearance into the tweet.
12. String length proportion of hashtags: number of characters used by hashtags / total tweet characters
13. String length proportion of mentions: number of characters used by mentions / total tweet characters
14: String length proportion of URLs: number of characters used by URLs / total tweet characters
15. Timestamp: the numeric timestamp (Unix Epoch) of the tweet, which should allow to perform calculations of distance between tweets in terms of seconds.
16. Country: the country code, converted into one-hot encoding at some point of the feature generation.
17. User (one-hot encoding): the internal identifier of the user, as a one-hot encoded feature.
18. Retweet Count: how many retweets did this tweet receive. This value is suposed to be updated regularly as the retweets come after having gathered the original tweet.
19. Nearduplicate Count:how many duplicates or near-duplicates have been detected.  Those are tweets whose content is (almost) the same as the original one, but they are not explicit retweets nor does include any explicit reference to the original tweet.