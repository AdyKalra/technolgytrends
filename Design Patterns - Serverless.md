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
* 
