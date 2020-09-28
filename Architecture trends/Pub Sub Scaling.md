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

### Real world scenario

#### Tennis Australia's challenges
* The Australian Open’s worldwide audience engage with the event via every digital medium and format imaginable. Tennis Australia positions itself to its global sponsors and partners as the primary source for live scores, streaming videos, profile information, schedules and live commentary: millions of users receiving billions of realtime messages.

* Whilst most people’s devices support **WebSockets, given the sheer quantity of visitors and fans across the globe, Tennis Australia needed to ensure that the lowest common denominator device was supported without WebSocket support.**

* Secondly, it’s very difficult to accurately predict the minute-to-minute demand that a multiple-round tournament like the open generates. Tennis Australia needed a partner who could guarantee uninterrupted performance as demand for the services spiked wildly and quickly. Losing users through poor data delivery was not an option for them. Their advertising revenue was entirely dependent on continuous data delivery for its sponsors and partners.

#### The Ably Solution
* Only Ably could provide a solution that ensured redundancy across multiple regions. Client devices are intelligently routed to alternative data centres without relying on intervention by engineers or the domain name systems typically needed to route around faults.

* We provided live 24/7 support throughout the Open and actively monitored performance and capacity in case any pre-emptive action was needed — happily, it wasn’t!

* To guarantee performance scalability, Tennis Australia relied on Ably to ensure the latest match scores were made available to a new website visitor the moment the page loaded. This was achieved by looking back at the history of published events for that scoreboard using Ably’s history API.

* Ably’s client library SDKs provided cross-platform support for all visitor devices and browsers regardless of whether they had modern support for WebSockets. **The client library SDKs gracefully fall-back to lowest common denominator transports like HTTP streaming, XHR and JSONP where necessary ensuring all visitors were delivered a realtime experience.**

* As you have seen, there’s a lot involved when implementing support for the WebSocket protocol, not just in terms of client and server implementation details, but also with respect to **fallback transports, or broader concerns, such as authentication and authorization, guaranteed message delivery, reliable message ordering, or historical message retention.**

#### Problem 1: Theoretically limitless and often unpredictable number of bettors receiving live updates
* Most often a stream of events arrive at the app developer’s servers from a sports data provider (such as Opta or Sportradar), some business logic is applied, and the data then needs to be pushed to every device participating in that game.

* For example, when a goal is scored, you may want every user of your service to receive that update within **200 milliseconds anywhere on earth.** The challenge typically is that you want that **target latency** to be met when you have just one or millions of users, without changing your architecture as the volumes increase.

### Pattern 1# — Pub/Sub
* This pattern is hardly new, it’s been around since 1987, yet it’s still a good way to approach asynchronous realtime data distribution. The pattern involves two roles, Pub represents the publisher, Sub represents the subscriber. The pattern specifies that the publisher (your server typically) publishes messages without any knowledge of how many subscribers there are. And subscribers register to receive message without any knowledge of the publishers. This ensures the two roles are intentionally decoupled with a middleware broker responsible for receiving messages and fanning out the messages to the subscribers.

#### How does this help?
* It ensures your apps scale to theoretically limitless subscribers without any changes to the design of your system, thus keeping your stack simple whilst giving you the scale you need. The middleware broker is responsible for providing scale. If you chose a middleware solution that has proven scale, then by adopting the pub/sub pattern, as you scale only one component needs to address that need in a predictable way.
**
* At Ably, our customers use Ably’s Pub/Sub feature as the middleware broker which provides limitless scale. Channels are used to provide **topic filtering** such as one channel for each game or player. As Ably’s system is elastic by design and Ably’s roundtrip latencies globally are circa 60ms, developers trust us to look after the scale issues.

#### Problem 2: Data synchronization
### Problem 1 describes how data, as messages, is distributed to devices, but it does not address how you keep the game data in sync consistently with all devices.

* For example, your app may need to maintain live league tables or penalty stats. As every event occurs during the match, your app needs to reflect that change in real time both in the UI and also within the local storage. The challenge is one of data integrity and bandwidth. If you publish the entire set of events for each penalty issued, it could be hugely inefficient and will result in significant bandwidth load on your users’ devices. Perhaps more importantly this could impair the user experience for people on slower connections or with expensive bandwidth. If however you only send data updates, how do you ensure that the data integrity is maintained i.e. you need all updates arrive reliably and in order?

### Pattern 2.1# — Serial JSON Patches
* JSON Patch is a standard that defines how you can send only the deltas for a JSON object as it mutates. For example, if you had a table of all players with their stats, and only one player’s stats changed following a goal being scored, then the patch may look something like:

[  { "op": "replace", "path": "/player/bob/goals", "value": "1" },]
#### How does this help?
* JSON Patch provides a means to efficiently send deltas for a JSON object thus reducing bandwidth overhead significantly. However, JSON Patch does not provide the complete solution as:

  * You need to obtain the JSON object at the outset
  * The JSON Patches must be applied in the exactly the order they were generated — a missing or out-of-order patch will result in complete loss of data integrity
Ably, uniquely in the realtime messaging industry, offers reliable data delivery uniquely ensuring that data arrives in the correct order and continuity is assured. We also provide a message history (replay) feature providing a means to obtain historical message published on the channel prior to connecting. Finally, we uniquely offer continuous history ensuring developers can reliably obtain history and receive subsequent realtime updates without any missing messages or duplicates.

* A pattern we’ve seen developers use with Ably to solve this problem therefore is:
 * Configure messages to be persisted
 * Publish the original JSON object on the channel, and then subsequently all JSON Patches
 * Clients when connecting then obtain the channel history and subscribe to future JSON patches. The history provides a means to build the JSON object from the initial object plus all the patches, and the attached channel ensures live updates continue to be received in order with integrity.
 * If a client loses continuity on the channel (this may happen if the client is disconnected for more than two minutes), the app simply repeats the previous step.
Note: We are in fact driving forward the development of an open standard Open-SDSP (Open Streaming Data Sync Protocol) to help solve these types of synchronization issues. I have previously written thoughts on why this is needed, and how this open standard could benefit the industry.

Pattern 2.2# — CRDT
A CRDT is a conflict-free replicated data type. Unlike JSON Patch, it allows multiple parties to concurrently updates the underlying data object. Each update is then distributed to all other parties, and the algorithm ensures that once all updates are applied by all participating parties, the underlying data object will become eventually consistent, regardless of the order the updates are applied.

CRDTs provide a very sophisticated way to ensure data is consistent, even when there are multiple parties changing the data at the same time. However, in order to provide the eventual consistency guarantees, there are limited data types with specific restrictions.

We find CRDTs are more commonly used in collaborative applications similar to Google Docs, where multiple users can update the content simultaneously. Riak is one of the few database solutions that provides native CRDT support. I will leave it to the reader to consider whether CRDT is appropriate for their use case and how best to implement it.

Problem 3: Upstream game play events
Problem 1 and 2 addresses the issues of scaling downstream data to your devices. However, participating in live events may have an upstream component i.e. users participating by voting or chatting.

Typically this is handled with a simple HTTP request to your servers which in turn run some business logic which may respond synchronously (as part of the response to the HTTP request), or asynchronously (pushed back to the device later as a message).

The problem app developers face are:

Using an HTTP request in a synchronous fashion increases the likelihood that the operation fails in changing network conditions. For as along as the client is waiting for a response, there is a chance the connection state will change and the underlying TCP connection for the HTTP request will be closed. If a request has failed due to a TCP connection, it may need to be retried, but unless the operation is idempotent, it could result in unexpected behaviour for users (such as placing two identical bets).
If there is a sudden spike of activity, perhaps due to an unforeseen change in the match such as a player being taken off, then your servers will need to absorb that load immediately. You need to predict the load in advance of each game and ensure you have sufficient service capacity for the spikes.
HTTP provides no ordering guarantees i.e. a later request may arrive before an earlier request when they are close together.
Pattern 3# — Message queues, serverless architecture and streams
Traditional message queues are designed to provide a message-orientated means to communicate between components of the system, specifically the devices and your servers in this instance. Like the pub/sub middleware, the message queue acts as a broker distributing messages to each consumer. If your messaging middleware is scalable and resilient, then decoupling each component in the system ensures failure or overload in one area of the system will not affect any other part of the system.

Please note, unlike the pub/sub pattern where each message is delivered to all subscribers, message queues typically deliver messages only once to one of the consumers (technically AMQP can only provide an at least once guarantee, however in almost all situations it provides exactly once delivery). Messages typically operate with FIFO (first-in-first-out) ensuring that in spite of any backlog that builds up if consumers cannot keep up, the consumers will always be working on the most oldest messages first.


Diagram illustrating message queues using Ably
How does this help?
By decoupling publishers of data (your devices in this instance) from the consumers of the data (your servers), and introducing a message queue middleware broker, you are building a fault tolerant system. For example:

Huge spikes of activity may slow down the responsiveness for customers as the workers have to work through the backlog of messages to process, but customers will not experience failures.
Where the ordering of events from device to server is important, the message queue is able to provide ordering guarantees. The Ably service too provides reliable ordering, so ordering is maintained from publishing to Ably all the way through to the queue.
Messages from devices are streamed immediately into the queue and the device receives an ACK immediately notifying the device that the message has been received. As a result, if you use Ably for publishing, we can ensure a message is never published twice (i.e. if you publish a message, lose connection before you receive an ACK, and then retry the message once connected, we de-dupe that message).
Note: Ably provides a number services to ensure scale when processing upstream events:

Reactor Serverless Functions allow a stream of events to trigger serverless functions on AWS, Google or Azure who provide the scale you need,
Reactor Message Queues provide a hosted AMQP/STOMP queue to consume realtime data
Reactor Firehose allows realtime data to be streamed into any number of third party streaming or queueing services such as AWS Kinesis, Kafka, AWS SQS, RabbitMQ etc.


[Source](https://www.ably.io/blog/design-patterns-sports-live-events)
