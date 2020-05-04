* Amazon Simple Notification Service **(SNS) is a highly available, durable, secure, fully managed pub/sub messaging service that enables you to decouple microservices, distributed systems, and serverless applications**. ... Additionally, SNS can be used to **fan out notifications to end users using mobile push, SMS, and email.**
* Amazon Simple Queue Service **(SQS) is a fully managed message queuing service that enables you to decouple and scale microservices, distributed systems, and serverless applications**
* SQS is distributed queuing system. ... Polling inherently introduces some latency in message delivery in SQS unlike SNS where messages are immediately pushed to subscribers
*  (Amazon SNS) is a web service that **coordinates and manages the delivery or sending of messages to subscribing endpoints or clients.** In Amazon SNS, there are **two types of clients — publishers and subscribers — also referred to as producers and consumers.**
* With the SNS free tier, your first million push notifications (publishes and deliveries) are free every month. 
* Create a new SNS topic in the AWS SNS dashboard page.
  * Click Topics.
  * Click Create topic.
  * Enter a topic name and a display name.
  * Click Create topic.
* Amazon SNS and AWS Lambda are integrated so **you can invoke Lambda functions with Amazon SNS notifications. When a message is published to an SNS topic that has a Lambda function subscribed to it, the Lambda function is invoked with the payload of the published message.**

![sns to sqs](https://d2908q01vomqb2.cloudfront.net/1b6453892473a467d07372d45eb05abc2031647a/2017/11/20/introducing_sns_message_filtering_image_1.png)
