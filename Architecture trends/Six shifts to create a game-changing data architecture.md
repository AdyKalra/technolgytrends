# Six shifts to create a game-changing data architecture
* We have observed six foundational shifts companies are making to their data-architecture blueprints that enable more rapid delivery of new capabilities and vastly simplify existing architectural approaches (exhibit). They touch nearly all data activities, including acquisition, processing, storage, analysis, and exposure. 

![Data-architecture-exhibit](https://www.mckinsey.com/~/media/McKinsey/Business%20Functions/McKinsey%20Digital/Our%20Insights/How%20to%20build%20a%20data%20architecture%20to%20drive%20innovation%20today%20and%20tomorrow/SVG-Data-architecture-exhibit.svgz)

## From on-premise to cloud-based data platforms
* Cloud is probably the most disruptive driver of a radically new data-architecture approach, as it offers companies a way to rapidly scale AI tools and capabilities for competitive advantage. Major global cloud providers such as Amazon (with Amazon Web Services), Google (with the Google Cloud Platform), and Microsoft (with Microsoft Azure) have revolutionized the way organizations of all sizes source, deploy, and run data infrastructure, platforms, and applications at scale.
    * One utility-services company, for example, combined a cloud-based data platform with container technology, which holds microservices such as searching billing data or adding new properties to the account, to modularize application capabilities. This enabled the company to deploy new self-service capabilities to approximately 100,000 business customers in days rather than months, deliver large amounts of real-time inventory and transaction data to end users for analytics, and reduce costs by “buffering” transactions in the cloud rather than on more expensive on-premise legacy systems.

### Enabling concepts and components

* **Serverless data platforms**, such as Amazon S3 and Google BigQuery, allow organizations to build and operate data-centric applications with infinite scale without the hassle of installing and configuring solutions or managing workloads. Such offerings can lower the expertise required, speed deployment from several weeks to as little as a few minutes, and require virtually no operational overhead.

* **Containerized data solutions using Kubernetes** (which are available via cloud providers as well as open source and can be integrated and deployed quickly) enable companies to decouple and automate deployment of additional compute power and data-storage systems. This capability is particularly valuable in ensuring that data platforms with more complicated setups, such as those required to retain data from one application session to another and those with intricate backup and recovery requirements, can scale to meet demand.

## From batch to real-time data processing

* The costs of real-time data messaging and streaming capabilities have decreased significantly, paving the way for mainstream use. These technologies enable a host of new business applications: transportation companies, for instance, can inform customers as their taxi approaches with accurate-to-the-second arrival predictions; insurance companies can analyze real-time behavioral data from smart devices to individualize rates; and manufacturers can predict infrastructure issues based on real-time sensor data.

* Real-time streaming functions, such as a subscription mechanism, allow data consumers, including data marts and data-driven employees, to **subscribe to “topics”** so they can obtain a constant feed of the transactions they need. **A common data lake typically serves as the “brain” for such services, retaining all granular transactions.**

### Enabliing concepts and components

* **Messaging platforms** such as Apache Kafka provide **fully scalable, durable, and fault-tolerant publish/subscribe services that can process and store millions of messages every second for immediate or later consumption.** This allows for support of real-time use cases, bypassing existing batch-based solutions, and a much lighter footprint (and cost base) than traditional enterprise messaging queues.
* **Streaming processing and analytics solutions** such as **Apache Kafka Streaming, Apache Flume, Apache Storm, and Apache Spark** Streaming allow for direct analysis of messages in real time. This analysis can be **rule based or involve advanced analytics to extract events or signals from the data.** Often, analysis integrates historic data to compare patterns, which is especially vital in recommendation and prediction engines.
* **Alerting platforms such as Graphite or Splunk** can trigger business actions to users, such as notifying sales representatives if they’re not meeting their daily sales targets, or integrate these actions into existing processes that may run in enterprise resource planning (ERP) or customer relationship management (CRM) systems.

### 
