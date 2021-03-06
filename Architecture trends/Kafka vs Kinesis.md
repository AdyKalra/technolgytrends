| |Apache Kafka |	Amazon Kinesis |
|:-:  |:-:  |:-:  |
| Concepts |	Kafka Streams |	Kinesis Analytics | 
|Stream of records| container	|Topic	Stream|
|Data Stored in...	|Kafka Partition|	Kinesis Shard|
|Unique ID of a record|	Offset number|	Sequence number|
|Ordering under...|	Partition level	|Shard level|
|Features	||	
|SDK Support|	Kafka SDK supports Java	|AWS SDK supports Android, Java, Go, .NET|
|Configuration & Features	|More control on configuration and better performance	|Number of days/shards can only be configured|
|Reliability	|The replication factor can be configured	|Kinesis writes synchronously to 3 different machines/data-centers|
|Performance	|Kafka wins	|Kinesis writes each message synchronously to 3 different machines|
|Data Retention|	Configurable	|7 days at max|
|Log Compaction	|Supported	|Not supported|
|Processing Events	|More than 1000s of events/sec|	Almost 1000s of events/sec|
|Producer Throughput|	Kafka Wins	|Kinesis is a bit slower than Kafka|
|Ops		||
|Setup|	Weeks	|A couple of hours|
|Configuration Store	|Apache Zookeeper	|Amazon DynamoDB|
|Checkpointing	|Offsets stored in a special topic|	DynamoDB|
|Incident Risk/Maintenance	|More In Kafka	|Amazon takes care|
|Human Costs	|Require human support for installing and managing their clusters, and also accounting for requirements such as high availability, durability, and recovery	|Kinesis is just about paying and use|

![kinesis-vs-kafka](https://www.softkraft.co/uploads/aws-kinesis-vs-kafka-which-to-choose.png)

# Decision Points to Choose Apache Kafka vs Amazon Kinesis
* Choosing the streaming data solution is not always straightforward. Making a decision on which streaming platform to use is based on the metrics you want to achieve and the business use case. Following are some metrics and decision points to compare whether to choose Apache Kafka or Amazon Kinesis as a data streaming solution:

## Setup, Management, and Administration
* Apache Kafka takes days to weeks to setup a full-fledge production ready environment, based on the expertise you have in your team. As an open-source distributed system, it requires its own cluster, a high number of nodes (brokers), replications and partitions for fault tolerance and high availability of your system.  Setting up a Kafka cluster would require learning (if there is no prior experience in setting up and managing Kafka Cluster) and distributed systems engineering practice and capabilities for cluster management, provisioning, auto-scaling, load-balancing, configuration management, a lot of distributed DevOps etc.

* On the other hand, Kinesis is comparatively easier to setup than Apache Kafka and may take a maximum of couple of hours to setup a production ready stream processing solution. Since it is a managed-service, AWS manages the infrastructure, storage, networking, and configurations needed to stream data on your behalf. On top of that, Amazon Kinesis takes care of provisioning, deployment, on-going maintenance of hardware, software or other services of data streams for you. Additionally, Kinesis producer and consumers can also be created and are able to interact with the Kinesis broker from outside AWS by means of Kinesis APIs and Amazon Web Service (AWS) SDKs.

## Performance Tuning – Throughput, Latency, Durability, and Availability
* Tuning Apache Kafka for optimal throughput and latency require tuning of Kafka producers and Kafka consumers. Producers can be tuned for number of bytes of data to collect before sending it to the broker and consumers can be configured to efficiently consume the data by configuring replication factor and a ratio of number of consumers for a topic to number of partitions.
  *  In addition, server side configurations e.g., replication factor and number of partitions  play an important role in achieving top performance by means of parallelism. To guarantee that messages that have been committed should not be lost – i.e., to achieve durability, the data can be configured to persist until you run out of the disk space. The distributed nature of the Kafka framework is designed to be fault-tolerant. For high availability, Kafka  needs to be configured to recover from failures as soon as possible.
  
* In contrast, Amazon Kinesis is a managed service and does not give a free hand for system configuration. The high availability of the system is the responsibility of AWS. Kinesis ensures availability and durability of data by synchronously replicating data across three availability zones. However in comparison to Kafka, Kinesis only lets you configure number of days per shards for the retention period, and that too for not more than 7 days. The throughput of a Kinesis stream is configurable to increase by increasing the number of shards with in a datastream.

### Human Costs and Machine Costs
* Setting-up and maintaining Kafka often requires significant technical resources, which comes with man hours billing for setup and 24/7 ongoing operational burden of managing your own infrastructure. Moreover, there are costs associated to dedicated hardware, however these costs can be controlled or lowered by investing more human time (and costs) for optimizing the machines for their utilization to full capacity.

* Amazon’s model for Kinesis is pay-as-you-go. It works  on the principle that there are no upfront costs for setting-up but amount to be paid depends upon the rendered services. For example, Kinesis pricing is based on two core dimensions: 1) number of shards needed for the required throughput and 2) a Payload Unit i.e., size of data producer is transmitting to the kinesis data streams. Therefore, saving the companies from bearing the time and monetary expenses for infrastructure building and its constant maintenance. Moreover, the Kinesis costs are reduced normally with time automatically based on how much your workload is typical to the Amazon.

### Incident Risk Management
* As long as a really good monitoring system is in place for Kafka that is capable of on-time alerting of any failures and a 24/7 team of DevOps taking care of potential failures and recovery, there is a less risk of incidence. The main decision point here is whether you can afford outages and loss of data if you do not have a 24/7 monitoring, alerting, and DevOps team to recover from the failure. With Kinesis – as a managed-service,  Amazon itself takes care of the high-availability of the system so these are less likely to occur.
