---
position: 3
layout: page
title: Getting started with the online demo
menu: Demo
permalink: demo.html
---

<a class="btn btn-success" href="[minteressa-online-demo]">Visit the online demo</a>

## Authentication

In order to access to the online application, it's required for you to authenticate on twitter with your account and to allow the "M'interessa" application to access to your timeline and user basic information:


[Screenshot to be included]

After that, you'll be redirected to the webpage, where you'll find a sidebar with a button that will allow you to create the first topic. Click on it to start.

[Screenshot]

It's required to set a title on the topic, as this will be the label that will allow you to find the topic on the sidebar.  Then you can choose whether the tweets that you have in your timeline or that you searched are relevant or not.

[Screenshot timeline/search boxes]

As you can see, the tweets include two buttons: green (to select as relevant) and red (to discard).  Choose them for each tweet on the list.  When you've finished all the list, you can either repeat the process (in the case of search, as the timeline always returns the same tweets) by performing more searches and adding more tweets to the list of relevant items.

When you're done, click on the button "Ready" and access to the stream tab of the topic. From now on, the new tweets that a priori seem to be relevant will appear and you'll have to mark them as relevant or discarded, the same way you did on the first stage.

## Evolution of the model accuracy

Meanwhile you're selecting and discarding tweets, the system is evaluating your responses and trying to get an idea of the line that separates the good and the bad ones.  At this poing there's not a clear idea of how much time and tweets will it take to get a trained model for your topic, as it involves many internal and external factors, like:

* The consistency of the chosen topic. Narrower topics may be easier (in terms of modeling) to get an accurate response, but can take longer because of a lack of samples.
* niche or mainstream topic. A mainstream topic may be easier to train because there are more tweets, but at first probably there will be shown more unrelevant tweets.
* Timeframed topics, like events or other

As you can see there's a lot of options. However, you can help the model to be trained faster by following some basic guidelines:
* Be strict if there's plenty of tweets, and relax a bit your criteria if too few tweets are selected. The point is that getting to a minimum amount of tweets will help the model to train faster.
* If there are two topics with very different dynamics,
* If there's a hashtag very tied to the topic, use it. At first you'll receive a lot of tweets with such hashtag, but if you are able to diversify the amount of hashtags of the selected tweets, then' you'll give enough diversity to
* If the topic that you've chosen is totally new for you, try to get some auxiliary help from sources like Wikipedia or similar to be sure when a tweet may be of interest. Discarding the right tweets specially during the beginning of the training may cause a bias that may take time to correct.
* Up to some point your knowledge about the matter may evolve while learning from the information on the tweets. This may lead to changes in your criteria for tweet selection. Don't worry, only try to be patient with the model until it catches the change and adapts to you.

At the end, it's a matter of balance: set a decently narrow topic, try to be sure what you're choosing, and try to be consistent on the scope.

And last but not least... Thanks for testing! :)

[minteresa-online-demo][https://github.com/m_interessa]