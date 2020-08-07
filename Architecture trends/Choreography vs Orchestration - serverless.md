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

#### Cons
* End-to-end monitoring and reporting are difficult.
* Difficult to implement timeouts.
* The order flow is not explicitly modelled and exists only as an emergent property of what system does. As such, it’s only captured in the mental model of someone who understands the system end-to-end.
* From a business point-of-view, it also begs the question “are these really separate processes? Or are they different steps within one process?”.
* For business-critical workflows like this, wouldn’t you want someone or some team to take ownership of and be responsible for it? When something goes wrong and you lose millions by the hour, do you want a room full of people looking at each other because no-one understands the process end-to-end?
* And if there are few people in the company understands how this critical flow works, then it creates an existential risk to the business if these people ever left the company.

## The Orchestration approach

* To implement the orchestration approach, I will probably use something like Step Functions and model the order flow as a state machine.

![StepFns](https://theburningmonk.com/wp-content/uploads/2020/08/img_5f2c8f59acae6.png)

* It’s also worth remembering that, although we no longer need to use events to trigger the next step of the order flow, those events are still useful artefacts on their own. So we should publish those same events from Task states in the state machine. For example, after the Notify User state notifies the user via SES, the Task should also publish the user_notified event.

* This means we can still decouple the order flow from other business units that wish to build features on top of events related to an order. The aforementioned promo-code service can still rely on the order_completed event as before.

![EventBridge](https://theburningmonk.com/wp-content/uploads/2020/08/img_5f2c8f702b299.png)\

#### Pros
* End-to-end monitoring and reporting are trivial since Step Functions gives you built-in visualization and audit histories.
* Easy to implement timeout?—?e.g. for a restaurant to accept an order, or for the total duration of the order.
* Business logic is in one place, and it’s easy to maintain and manage.
* The order flow is modelled and source controlled. You can literally see it in the Step Functions console.

#### Cons
* Have to learn yet another AWS service.
* At $25 per million state transitions (which counts Start and End by the way), Step Functions is a pricey service.
* If Step Functions is down, then no orders can be processed. Although the same might be said about Lambda, EventBridge, or any services that are critical to the working of this order flow.

## The hybrid approach
* Within a bounded context, I have a specific set of responsibilities that are aligned with a business area. And there are hopefully a small number of components that they can all fit inside my head at the same time. Since they all work together to achieve some specific business capability such as processing payments, they form a highly cohesive unit. And since I own everything within this microservice’s bounded context, I’m free to change and reorganize things so long I don’t break my contract with external services.

* I often see workflows within a bounded context being choreographed through messages in SQS/SNS/EventBridge.

* Generally speaking, I think that’s a bad idea.

![LC](https://theburningmonk.com/wp-content/uploads/2020/08/img_5f2c8f92e868d.png)

* I love using events to integrate different services together in a loosely-coupled way. But I think it’s a bad idea when it’s done inside the same bounded context because the workflow doesn’t exist as a standalone concept that is explicitly captured and source controlled.

* In these choreographed workflows, the workflow only exists as the sum of loosely connected functions. As we discussed above with the food delivery example, this makes them very difficult to reason about and debug. And there’s no easy way to implement even simple things like workflow level timeouts, or even task level tasks for that matter (e.g. timeout the order if the restaurant doesn’t accept or reject the order within 10 minutes).

* If this is what you have today, you should consider moving these workflows to Step Functions instead.

* But, between bounded contexts, I’ll publish and subscribe to events through SNS/EventBridge/Kinesis, etc. This is so that different parts of the larger system can stay loosely coupled and only build on each other’s events and can evolve and fail independently.

![hybrid](https://theburningmonk.com/wp-content/uploads/2020/08/img_5f2c8faa706cc.png)

### Summary

* Orchestration and choreography don’t have to be mutually exclusive. Whenever I’m introducing state changes inside a state machine (such as changing the status of an order from pending to processed), I’ll publish those state changes as events. Other services can listen and react to these state changes, and bringing choreography into the picture.

* Let me leave you with my rule-of-thumb when it comes to implementing business workflows: use orchestration within the bounded context of a microservice, but use choreography between bounded-contexts.

![Source](https://theburningmonk.com/2020/08/choreography-vs-orchestration-in-the-land-of-serverless/)
