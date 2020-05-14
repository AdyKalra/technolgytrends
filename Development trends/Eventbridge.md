* Amazon EventBridge is a **serverless event bus that makes it easy to connect applications together using data from your own applications, integrated Software-as-a-Service (SaaS) applications, and AWS services.**
  * EventBridge delivers a stream of **real-time data from event sources, such as Zendesk, Datadog, or Pagerduty, and routes that data to targets like AWS Lambda.**
  * You can **set up routing rules to determine where to send your data** to build application architectures that react in real time to all of your data sources. 
  * EventBridge makes it easy to** build event-driven applications because it takes care of event ingestion and delivery, security, authorization, and error handling for you.**
  * As your applications become more interconnected through events, you need to spend more effort to find events and understand their structure in order to write code to react to those events. 
    * The Amazon EventBridge schema registry stores event structure - or schema - in a shared central location and maps those schemas to code for Java, Python, and Typescript so it’s easy to use events as objects in your code. 
    * You can connect to and interact with the schema registry from the AWS Management Console, APIs, or the SDK Toolkits for Jetbrains (Intellij, PyCharm, Webstorm, Rider) and VS Code.
    
 ![EventBridge](https://d1.awsstatic.com/asset-repository/product-page-diagram-EventBridge_How-it-works_GA@2x.400d9a43a0a23ab2770bde727234395ab369e838.png)
