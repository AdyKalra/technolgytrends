# Serverless Microservice Patterns for AWS

### Very important distinction between synchronous and asynchronous communication

* **Synchronous Communication**
Services can be invoked by other services and must **wait for a reply**. This is considered a blocking request, because the invoking service cannot finish executing until a response is received.
* **Asynchronous Communication**
This is a **non-blocking request**. A service can invoke (or trigger) another service directly or it can use another type of communication channel to **queue information.** The service typically only needs to wait for confirmation (ack) that the request was sent.

# Patterns
* **A large black arrow represents an asynchronous request. The two smaller black arrows represents a synchronous request.**

## The Simple Web Service
* most basic of patterns you’re likely to see with serverless applications. 
* The Simple Web Service fronts a Lambda function with an API Gateway. 
* I’ve shown **DynamoDB as the database here because it scales nicely with the high concurrency capabilities of Lambda.**

![Simple Web Service](https://www.jeremydaly.com/wp-content/uploads/2018/08/simple-web-service-1200x196.png)

## The Scalable Webhook
* If you’re building a webhook, the traffic can often be unpredictable. 
* This is fine for Lambda, but if you’re using a **“less-scalable” backend like RDS**, you might just run into some bottlenecks. 
* There are ways to manage this, but now that Lambda supports SQS triggers, we can **throttle our workloads by queuing the requests and then using a throttled (low concurrency) Lambda function to work through our queue.** 
* Under most circumstances, your throughput should be near real time. If there is some heavy load for a period of time, you might experience some small delays as the throttled Lambda chews through the messages. 
* SQS triggers for Lambda functions now work correctly with throttling, so it is no longer necessary to manage your own redrive policy.
![Scalable Webhook](https://www.jeremydaly.com/wp-content/uploads/2018/08/scalable-webhook-1200x416.png)

## The Gatekeeper
* This is a variation on the Simple Web Service pattern. 
* Using API Gateway’s **“Lambda Authorizers”**, you can connect a Lambda function that processes the Authorization header and returns an IAM policy. 
* API Gateway then uses that policy to determine if it is valid for the resource and either routes the request, or rejects it. 
* API Gateway caches the IAM policy for a period of time, so you could also classify this as the **“Valet Key” pattern.** 
* As I point out in the diagram below, Lambda Authorizers are microservices in their own right. Your “Authorization Service” could have multiple interfaces into it to add/remove users, update permissions, and so forth.

![Gatekeeper](https://www.jeremydaly.com/wp-content/uploads/2018/08/gatekeeper-1200x445.png)

## The Internal API
* The Internal API pattern is essentially **a web service without an API Gateway frontend.** 
* If you are building a microservice that only needs to be accessed from within your AWS infrastructure, **you can use the AWS SDK and access Lambda’s HTTP API directly.** 
* If you use an InvocationType of RequestResponse, then a synchronous request will be sent to the destination Lambda function and the calling script (or function) will wait for a response. 
* Some people say that functions calling other functions is an anti-pattern, but I disagree. 
* HTTP calls from within microservices are a standard (and often necessary) practice.
* Whether you’re calling DynamoDB (http-based), an external API (http-based) or another internal microservice (http-based), your service will most likely have to wait for HTTP response data to achieve its directive.

![Internal API](https://www.jeremydaly.com/wp-content/uploads/2018/08/internal-api-1200x196.png)

## The Internal Handoff
* Like the Internal API, the Internal Handoff pattern uses the AWS SDK to access Lambda’s HTTP API. 
* However, in this scenario we’re using an InvocationType of Event, which disconnects as soon as we get an ack indicating the request was successfully submitted. 
* The Lambda function is now receiving an **asynchronous event**, so it will automatically utilize the built-in retry mechanism. This means two things, 
  * 1) it is possible for the event to be processed more than once, so we should be sure that our events are idempotent. And 
  * 2) Since we disconnected from our calling function, we need to be sure to capture failures so that we can analyze and potentially replay them. 
* Attaching a **Dead Letter Queue (DLQ) to asynchronous Lambda functions is always a good idea.** I like to use an SQS Queue and monitor the queue size with CloudWatch Metrics. That way I can get an alert if the failure queue reaches a certain threshold.

![Internal Handoff](https://www.jeremydaly.com/wp-content/uploads/2018/08/internal-handoff-1200x391.png)

## The Aggregator
* Speaking of internal API calls, the Aggregator is another common microservice pattern. 
* The Lambda function in the diagram below makes three synchronous calls to three separate microservices. 
* We would assume that each microservice would be using something like the Internal API pattern and would return data to the caller. The microservices below could also be external services, like third-party APIs. 
* **The Lambda function then aggregates all the responses and returns a combined response to the client on the other side of the API Gateway.**

![Aggregator](https://www.jeremydaly.com/wp-content/uploads/2018/08/aggregator-1200x298.png)


## The Notifier
* I’ve had this debate with many people, but I consider an SNS topic (Simple Notification Service) to be its own microservice pattern. 
* A important attribute of microservices is to have a “well-defined API” in order for other services and systems to communicate with them. 
* SNS (and for that matter, SQS and Kinesis) have standardized APIs accessible through the AWS SDK. 
* If the microservice is for internal use, a standalone SNS topic makes for an extremely useful microservice. 
  * For example, if you have multiple billing services (e.g. one for products, one for subscriptions, and one for services), then it’s highly likely that several services need to be notified when a new billing record is generated. 
  * The aforementioned services can post an event to the “Billing Notifier” service that then distributes the event to subscribed services. We want to keep our microservices decoupled, so dependent services (like an invoicing service, a payment processing service, etc.) are responsible for subscribing to the “Billing Notifier” service on their own. As new services are added that need this data, they can subscribe as well.

![Notifier](https://www.jeremydaly.com/wp-content/uploads/2018/08/notifier-1200x175.png)

## The FIFOer
* AWS announced support for SQS FIFO queues as Lambda event sources, which makes this pattern no longer necessary. Read the full announcement here.

![FIFOer](https://www.jeremydaly.com/wp-content/uploads/2018/08/fifoer-1200x496.png)

## The “They Say I’m A Streamer”
* Another somewhat complex pattern is the continuous stream processor. 
* This is very useful for capturing clickstreams, IoT data, etc. 
* In the scenario below, I’m using API Gateway as a Kinesis proxy. This uses the “AWS Service” integration type that API Gateway provides.
* You could use any number of services to pipe data to a Kinesis stream, so this is just one example. 
* Kinesis will distribute data to however many shards we’ve configured 
* and then we can use Kinesis Firehose to aggregate the data to S3 and bulk load it into Redshift. There are other ways to accomplish this, but surprisingly, this will end up being cheaper when you get to higher levels of scale (vs SNS for example).

![They Say I’m A Streamer](https://www.jeremydaly.com/wp-content/uploads/2018/08/they-say-im-a-streamer-1200x322.png)

## The Strangler
* The Strangler is another popular pattern that let’s you incrementally replace pieces of an application with new or updated services. Typically you would create some sort of a “Strangler Facade” to route your requests, but API Gateway can actually do this for us using “AWS Service” and “HTTP” integration types. For example, an existing API (front-ended by an Elastic Load Balancer) can be routed through API Gateway using an “HTTP” integration. You can have all requests default to your legacy API, and then direct specific routes to new serverless service as you add them.

![Strangler](https://www.jeremydaly.com/wp-content/uploads/2018/08/strangler-1200x303.png)

## The State Machine
* It is often the case that Serverless architectures will need to provide some sort of **orchestration.**
 * AWS **Step Functions are, without a doubt, the best way to handle orchestration within your AWS serverless applications.** 
 * State Machines are great for coordinating several tasks and ensuring that they properly complete by implementing retries, wait timers, and rollbacks. 
 * However, they are **exclusively asynchronous**, which means you can’t wait for the result of a Step Function and then respond back to a synchronous request.
 * AWS advocates using Step Functions for orchestrating entire workflows, i.e. coordinating multiple microservices. I think this works for certain asynchronous patterns, but it will definitely not work for services that need to provide a synchronous response to clients. I personally like to encapsulate step functions within a microservice, reducing code complexity and adding resiliency, but still keeping my services decoupled.

![State Machine](https://www.jeremydaly.com/wp-content/uploads/2018/08/state-machine-1200x391.png)

## The Router
* The State Machine pattern is powerful because it provides us with simple tools to manage complexity, parallelism, error handling and more. However, Step Functions are not free and you’re likely to rack up some huge bills if you use them for everything.
* **For less complex orchestrations where we’re less concerned about state transitions**, we can handle them using the Router pattern.
 * In the example below, an asynchronous call to a Lambda function is determining which task type should be used to process the request. **This is essentially a glorified switch statement**, but it could also add some additional context and data enrichment if need be. 
 * Note that the main Lambda function is only invoking one of the three possible tasks here. As I mentioned before, asynchronous Lambdas should have a DLQ to catch failed invocations for replays, including the three “Task Type” Lambdas below. The tasks then do their jobs (whatever that may be). Here we’re simply writing to DynamoDB tables.

![Router](https://www.jeremydaly.com/wp-content/uploads/2018/08/router-1200x469.png)

## The Robust API
*

![Robust API]()

## The Frugal Consumer
*

![Frugal Consumer]()

## The Read Heavy Reporting Engine
*

![Read Heavy Reporting Engine]()

## The Fan-Out/Fan-In
*

![Fan-Out/Fan-In]()

## The Eventually Consistent
*

![Eventually Consistent]()

## The Distributed Trigger
*

![Distributed Trigger]()

## The Circuit Breaker
*

![Circuit Breaker]()

## 
*

![]()

## 
*

![]()
