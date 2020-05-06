* Amazon DynamoDB is a **fully managed proprietary NoSQL database service that supports key-value and document data structures and is offered by Amazon.com**
* DynamoDB is cheaper if you have large throughput value or you will end up paying for services you are not using. RDS, on the other hand, provides database at the similar cost that is needed to create a number of tables in DynamoDB.
* DynamoDB is **aligned with the values of Serverless applications: automatic scaling according to your application load, pay-per-what-you-use pricing, easy to get started with, and no servers to manage.** This makes DynamoDB a very popular choice for Serverless applications running in AWS.
* **DynamoDB Streams** captures a time-ordered sequence of item-level modifications in any DynamoDB table and stores this information in a log for up to 24 hours. ... **A DynamoDB stream is an ordered flow of information about changes to items in a DynamoDB table.**
* **Shards in DynamoDB streams are collections of stream records.** Each stream record represents a single data modification in the DynamoDB table to which the stream belongs.

![DDB](https://raw.githubusercontent.com/cdk-patterns/serverless/master/img/building-enterprise-architecture.jpg)
