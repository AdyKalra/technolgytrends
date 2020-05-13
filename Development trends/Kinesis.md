* **Amazon Kinesis** is a managed, scalable, cloud-based service that allows real-time processing of streaming large amount of data per second. ... It is used to capture, store, and process data from large, distributed streams such as event logs and social media feeds.
* **Kinesis Analytics allows you to perform SQL like queries on data. Kafka Streaming allows you to perform functional aggregations and mutations.** Kafka is more flexible than Kinesis but you have to manage your own clusters, and requires some dedicated DevOps resources to keep it going

* **Shard** A shard is a uniquely identified sequence of data records in a stream. A stream is composed of one or more shards, each of which provides a fixed unit of capacity.
  * By default, each account can provision 10 shards per region. You can use the Kinesis Data Streams Limits form to request more than 10 shards within a single region.
  
* The main difference between SQS and Kinesis is that the first is a FIFO queue, whereas the latter is a real time stream that allows processing data posted with minimal delay.

* What is the difference between Kinesis stream and Kinesis firehose?
There are a couple major differences I'm aware of. One, **Firehose is fully managed (i.e. scales automatically) whereas Streams is manually managed. Second, Firehose only goes to S3 or RedShift, whereas Streams can go to other services**. ... Kinesis Streams on the other hand can store the data for up to 7 days.

![Kinesis Architecture](https://www.softkraft.co/uploads/aws-kinesis-architecture.png)
