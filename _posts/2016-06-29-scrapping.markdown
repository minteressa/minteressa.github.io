---
layout: post
title: Scrapping the web from twitter
date: '2016-06-29 09:16:15 +0200'
categories: project
published: true
---
### Objectives
The main objective is to analyze the web pages mentioned by the tweet to determine if they are interesting for the user.

Secondary objectives:

* Identify type of pages could be more interesting
* Identify type of conten could be more interesting
* Have a preview of the page to easily identify it.

### Features
Each tweet has 1 or n url referenced. That url takes to a web page wich have several features. From each page we have extracted the following features:


From the content:

* All the images and their attributes
* All the links and their attributies. Also categorized by:

  * Social networks:
  
    * Twitter
    * Facebook
    * Reddit 
    * Meneame
    
  * Internal / External

Metadata:

* Whis name
* Whois organization
* Whois City
* Hostname
* Url Params
* Content Type
* Description
* Content language
* Abstract
* Topic
* Subject
* Generator
* copyright
* Title
* Author
* Schema Present?



### Troubleshooting

Extract the metadata from  whe web pages is relatively easy.  The most difficult is to access to the content due the actual dynamic web pages and the responsive design. Old pages rere a simple html content wich is easy to parse. But actual webs are difficult to process "the content"
There has been tests different packages for it **custom regexp processing** , **BeautifulSoup**, **requests** but none provide a reliable clean result. as far as there are a lot of code embedded in the text.

We wanted a thumbnail of the web sites. For that we used phantomJs wich provides us to make a snapshoot of the web pages.



### Procedure

1. The tweets come forom a Kafka pipe. 
2. The process looks form referenced urls
3. The referenceds URL are scrapped as described
4. The information is stored in a mongodb 
5. We make a photo of the web page
6. We rerturn the tweet to a kafka pipe
