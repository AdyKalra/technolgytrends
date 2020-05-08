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

## 
