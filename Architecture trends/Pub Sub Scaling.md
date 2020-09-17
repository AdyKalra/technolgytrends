# Pub Sub Scaling

## Overview
* Pub/Sub is an asynchronous messaging service designed to be highly reliable and scalable. The service is built on a core Google infrastructure component that many Google products have relied upon for over a decade. Google products including Ads, Search and Gmail use this infrastructure to send over 500 million messages per second, totaling over 1TB/s of data. 

* Pub/Sub is a publish/subscribe (Pub/Sub) service: a messaging service where the senders of messages are **decoupled from the receivers of messages**. There are several key concepts in a Pub/Sub service:

  * Message: the data that moves through the service.

  * Topic: a named entity that represents a feed of messages.

  * Subscription: a named entity that represents an interest in receiving messages on a particular topic.

  * Publisher (also called a producer): creates messages and sends (publishes) them to the messaging service on a specified topic.

  * Subscriber (also called a consumer): receives messages on a specified subscription.

The following diagram shows the basic flow of messages through Pub/Sub:
![wp_flow](https://cloud.google.com/pubsub/images/wp_flow.svg)
* In this scenario, there are two publishers publishing messages on a single topic. There are two subscriptions to the topic. The first subscription has two subscribers, meaning messages will be load-balanced across them, with each subscriber receiving a subset of the messages. The second subscription has one subscriber that will receive all of the messages. The bold letters represent messages. Message A comes from Publisher 1 and is sent to Subscriber 2 via Subscription 1, and to Subscriber 3 via Subscription 2. Message B comes from Publisher 2 and is sent to Subscriber 1 via Subscription 1 and to Subscriber 3 via Subscription 2.
