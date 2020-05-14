* The main task of a dead-letter queue is **handling message failure.** A dead-letter queue lets you set aside and isolate messages that can’t be processed correctly to determine why their processing didn’t succeed. Setting up a dead-letter queue allows you to do the following:
  * Configure an alarm for any messages delivered to a dead-letter queue.
  * Examine logs for exceptions that might have caused messages to be delivered to a dead-letter queue.
  * Analyze the contents of messages delivered to a dead-letter queue to diagnose software or the producer’s or consumer’s hardware issues.
  * Determine whether you have given your consumer sufficient time to process messages.

* In message queueing the dead letter queue is a service implementation to store messages that meet one or more of the following criteria:
  * **Message that is sent to a queue that does not exist.**
  * **Queue length limit exceeded.**
  * Message length limit exceeded. 
  * Message is rejected by another queue exchange.
  
* Do use dead-letter queues with standard queues. You should always take advantage of dead-letter queues when your applications don’t depend on ordering. Dead-letter queues can help you troubleshoot incorrect message transmission operations.

* Do use dead-letter queues to decrease the number of messages and to reduce the possibility of exposing your system to poison-pill messages (messages that can be received but can’t be processed).

![DLQ](https://d2908q01vomqb2.cloudfront.net/1b6453892473a467d07372d45eb05abc2031647a/2019/10/28/SNS-DLQ-1-1024x576.png)
