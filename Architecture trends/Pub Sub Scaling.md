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

### Latency
* Latency is a time-based measure of the performance of a system. A service generally wants to minimize latency wherever possible. For Pub/Sub, the two most important latency metrics are:
 * The amount of time it takes to acknowledge a published message.
 * The amount of time it takes to deliver a published message to a subscriber.
 
### Pub/Sub is divided into two primary parts: 
* the data plane, which handles moving messages between publishers and subscribers, and the control plane, which handles the assignment of publishers and subscribers to servers on the data plane. The servers in the data plane are called forwarders, and the servers in the control plane are called routers. When publishers and subscribers are connected to their assigned forwarders, they do not need any information from the routers (as long as those forwarders remain accessible). Therefore, it is possible to upgrade the control plane of Pub/Sub without affecting any clients that are already connected and sending or receiving messages.

### Data Plane - The Life of a Message
* The data plane receives messages from publishers and sends them to clients. Perhaps the best way of understanding Pub/Sub’s data plane is by looking at the life of a message, from the moment it is received by the service to the moment it is no longer present in the service. Let us trace the steps of processing a message. For the purposes of this section, we assume that the topic on which the message is published has at least one subscription attached to it. In general, a message goes through these steps:
1. A publisher sends a message.
2. The message is written to storage.
3. Pub/Sub sends an acknowledgement to the publisher that it has received the message and guarantees its delivery to all attached subscriptions.
4. At the same time as writing the message to storage, Pub/Sub delivers it to subscribers.
5. Subscribers send an acknowledgement to Pub/Sub that they have processed the message.
6. Once at least one subscriber for each subscription has acknowledged the message, Pub/Sub deletes the message from storage.

![pub](https://user-images.githubusercontent.com/8856857/93427768-baa6d280-f901-11ea-804d-9d3c7c9a7af9.png)
![sub](https://user-images.githubusercontent.com/8856857/93427863-df02af00-f901-11ea-89d5-72b8dc966223.png)
![glossary](https://user-images.githubusercontent.com/8856857/93427930-f80b6000-f901-11ea-877d-4c67d569f48f.png)
