---
layout: post
title:  "Near duplicate detection"
thumbnail: /assets/images/kafka-logo.png
date:   2016-06-20 11:16:15 +0200
post_author: Mario Alberich
categories: modelling
---
Twitter is full of duplicated or near-duplicated content (ND for short from now onwards).  Flooding a user's candidate tweet list with a bunch of items that have (almost) the same content can only lead to a bad user experience.

## So what's a near-duplicate
For sure you can imagine two text fragments that can be considered a duplicate one of another, by comparing its content and checking whether it's exactly the same.  There are some minor details that are trivial for a human but very important for a machine, for instance case sensitiviy (are uppercase and lowercase considered the same?), character sets depending on the language, or punctuation among others. In this situation, a duplicate text as we're considering it right now, is a text with the same content and structure, whichever the semantic meaning that involves.

## How much duplicate is a near-duplicate

This is an important point for the project. We've got both tweets (very short text fragments) and URL that got referenced from the tweet (potentially very long texts).

## Storing all the tweets is very costly

You may think that tweets are short, and this allows us to store all of them to store them all, but this is not true.

...Remember, we're receiving ab. 70 tweets per second. We can assume that half of them are filtered out before checking its duplicity. But even though this reduction, the amount is fairly big.

Moreover, the word frequency usage is very sparse, and if we try to look for a naive approach, this leads us to a huge array, where each tweet is a row, and each column is a word. You can imagine that this array is almost full of zeros, that's why the common approach is to go for a [sparse matrix](https://en.wikipedia.org/wiki/Sparse_matrix) representation of the documents. What leads to the concept of [vectorization of the documents](https://en.wikipedia.org/wiki/Vector_space_model).

This would be a good approach, but for sure there are more sophisticated ways that find a trade-off between speed and accuracy.

## Solution: Minhashing

Luckily there's a technique named [MinHash](https://en.wikipedia.org/wiki/MinHash) which, in short, allows to compress the amount of information of a tweet text in order to compare it.  When the tweet gets represented into this hashed code, it's possible to calculate de difference between two elements by calculating its [Jaccard similarity](https://en.wikipedia.org/wiki/Jaccard_index).

In order to perform such calculations, the library [datasketch](https://github.com/ekzhu/datasketch) will be used. More on this in further posts, when we can go deeper in the implementation stage.

## Time sensitivity of the near-duplicates

If you're a Twitter user, you may notice that there's a big volatility on what's trending today and tomorrow. So we can assume that there's a greater probability that we find duplicates today than tomorrow, and way greater than the next week.

Probably we'll run out of time before we can implement such improvement to the ND filtering, but it's worth noting that it would improve even a bit more the process, and of course it would keep the array of hashes under weight control.