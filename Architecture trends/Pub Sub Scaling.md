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

### Judging Performance of a Messaging Service

* A messaging service like Pub/Sub can be judged on its performance in three aspects: scalability, availability, and latency. These three factors are often at odds with each other, requiring compromises on one to improve the other two.

* The terms "scalability," “availability,” and “latency” can refer to different properties of a system, so the following sections describe how they are defined in Pub/Sub.

#### Scalability
* A scalable service should be able to handle increases in load without noticeable degradation of latency or availability. "Load" can refer to various dimensions of usage in Pub/Sub:
  * Number of topics
  * Number of publishers
  * Number of subscriptions
  * Number of subscribers
  * Number of messages 
  * Size of messages
  * Rate of messages (throughput) published or consumed
  * Size of backlog on any given subscription

### Availability
* In a distributed system, the types and severity of problems can vary greatly. A system’s availability is measured on how well it deals with different types of issues, gracefully failing over in a way that is unnoticeable to end users. Failures can occur in hardware (e.g., disk drives not working or network connectivity problems), in software, and due to load. Failure due to load could happen when a sudden increase in traffic in the service (or in other software components running on the same hardware or in software dependencies) results in resource scarcity. Availability can also degrade due to human error, where one makes mistakes in building or deploying software or configurations.
