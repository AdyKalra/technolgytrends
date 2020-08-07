## Choreography vs Orchestration in the land of serverless

* Choreography and Orchestration are two modes of interaction in a microservices architecture.

### Orchestration
* In orchestration, there is a controller (the ‘orchestrator’) that controls the interaction between services. It dictates the control flow of the business logic and is responsible for making sure that everything happens on cue. This follows the request-response paradigm.

### Choreography
* In choreography, every service works independently. There are no hard dependencies between them, and they are loosely coupled only through shared events. Each service listens for events that it’s interested in and does its own thing. This follows the event-driven paradigm.

* As always, neither is necessarily better than the other. Depending on the context, one might be more appropriate than the other. And since Lambda itself is inherently event-driven, the choreography approach has become very popular in the serverless community. I’m a huge fan of this approach and have built many event-driven systems using services such as EventBridge, SNS and Kinesis.

### When it’s not a good idea and when you should consider the orchestration approach instead.

**The TL;DR is that, when it comes to implementing workflows, you should prefer orchestration within the bounded context of a microservice, but prefer choreography between bounded contexts.**

## The Choreography approach

* Imagine you’re building a food ordering service where customers can order takeaways from their favourite restaurants. A typical order flow might involve the following five steps.

![food](https://theburningmonk.com/wp-content/uploads/2020/08/img_5f2c8f21d0a62.png)

* We can model these five steps as events:
  * order_placed
  * restaurant_notified
  * order_accepted
  * user_notified
  * order_completed

* With these events, we can implement the order flow using an event-driven approach.

![arch](https://theburningmonk.com/wp-content/uploads/2020/08/img_5f2c8f2e548a8-1536x967.png)

1. A customer places an order.
2. place-order function publishes an order_placed event.
3. notify-restaurant function is triggered by the order_placed event.
4. notify-restaurant function sends a message to the restaurant via SNS.
5. notify-restaurant function publishes a restaurant_notified event.
6. The restaurant receives the new order notification in its mobile app.
7. The restaurant clicks Accept Order in the app, which calls the orders API.
8. accept-order function publishes an order_accepted event.
9. notify-user function is triggered by the order_accepted event.
10. notify-user function sends an order confirmation email to the customer.
11. notify-user function publishes a user_notified event.
12. The customer sees the order confirmation and is eagerly waiting for the food to arrive.
13. The restaurant delivers the food to the customer.
14. The restaurant clicks the Complete Order in the app to confirm order has been delivered. This calls the orders API.
15. complete-order function publishes an order_completed event.

* Every function acted completely independently. None of them had the notion of the overall order flow, they each only cared about:

  * What events they are interested in.
  * What they should do.
  * What events they should publish when they complete their task.

#### Pros
* Each step of the flow can be changed independently.
* Each step of the flow can be scaled independently.
* No single point of failure.
* Other systems can build on these events?—?e.g. a promo-code service might be interested in the order_completed event and send out discount vouchers to the customer.
* The events are useful artefacts on their own, and can be fed into a data lake to generate business intelligence reports.
