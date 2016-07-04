---
layout: post
title: 'Kafkian: or how we deploy and set-up our Kafka broker'
thumbnail: /assets/images/kafka-logo.png
date: '2016-07-04 15:00:00 +0200'
post_author: Ruben Berenguel
categories: infrastructure
published: true
---

## What is Apache Kafka?
**Apache Kafka** is an industry standard solution for creating real-time data pipelines involving several subsystems. It is a queing system based on a publish-subscribe (*PubSub*) model, where *producers* publish messages to a topic (or several topics) and *consumers* subscribe to topics.<!–break–> Each topic is similar to a queue, hence consumers remove messages from the queue. It comes with built-in replication, and offers high scalability. As such, in general we talk about interacting with a Kafka *cluster*.

A Kafka cluster has one or several *Kafka brokers* -- or in other words, Kafka instances -- and at least one instance of Apache Zookeeper. Zookeeper keeps track of how many messages have been consumed from each topic as well as electing a *leader* among the Kafka brokers. The leader broker, as we can expect, is the primary reference in case one of the other brokers fail, and is used as ground truth when there are conflicts.

An interesting property about Kafka, is that it offers *exactly once* (EO) message passing as long as there is only one consumer for each topic. When managing queues, EO is the holy grail, since it is better than either ALO (at least once) or AMO (at most once). In most cases, though, we will need either more than one consumer per topic or a parallel process to deal with messages from a topic, breaking the EO guarantee. Then we need to ensure other invariants, which in our case would be *processed at least once* and *stored at most once*.

Kafka is written in Scala, actively maintained (the most recent version, 0.10 was released ~~check~~) and there are libraries to interact with it in most mainstream languages. In our case, we have several producers (in Python and Scala) and consumers (all in Python).

## Story about our setup

The [first piece we developed](https://github.com/rberenguel/pgds-kafka-backend) that needed to be tied to a Kafka cluster was a producer (written in Scala) that uses Twitter's API to generate a constant stream of tweets into the topic *tweets*. To do so, we used [this docker image](https://github.com/wurstmeister/kafka-docker), which uses `docker-compose` to link together one or more Kafka brokers and a Zookeeper instance. With this machine up, we can develop locally, getting the Scala code to interact with the localhost Kafka. We checked, and a nice stream of tweets entered Kafka and a test consumer in Python could subscribe and show them. All well and good?

When consumers connect to a Kafka broker for the first time, the broker will reply with its *advertised host name*, i.e. the IP/server name it assumes it is on, which is set as a configuration parameter before starting the broker. For the local setup, running Kafka in Docker and the producer in another console with Scala, this can be `localhost` or 127.0.0.1 and everything matches up nicely. But in a final setup we want to run the producer and Kafka (and ideally all producers and consumers) as a set of docker machines we can start with just 

```bash
docker-compose up
```

In this scenario, if the whole setup can be defined as a 'simple' compose file, it means that we can move on to separate instances for each subsystem easily if needed.

With this goal in mind, we set a docker image with the correct version of Scala and modified the compose file to add this image, linking it to Kafka... And nothing worked: the producer could not run and connecting an external (not from within the Docker images but from outside) consumer showed no messages. 

Long story short, first Scala could not correctly process the alias used by the link in compose -- had to upgrade to a compose 2.0 file to make sure DNS setup in Docker was working correctly -- then the advertised host name (which was the alias `kafka`) did not match anything in the 'external' machine -- this was fixed just by modifying `/etc/hosts`. 

In retrospect it seems easy, but during the process we learnt about how [docker manages its networks](https://docs.docker.com/v1.11/engine/userguide/networking/dockernetworks/), [how links work](https://docs.docker.com/v1.11/compose/link-env-deprecated/) and how the [ambassador pattern](https://docs.docker.com/engine/admin/ambassador_pattern_linking/) could be used in these cases.
