* AWS has built out so many products and services that it’s impossible to begin to discuss them in a single article or even a book. Many of them were amazing innovations when they first appeared and the hits keep coming
* Sometimes the competitors not only match AWS for commodity products, but they actually do a better job. These advantages often appear when the competitors link their cloud to parts of the computer ecosystem that they already dominate. If you want to use .NET code, you’ll find it just a bit easier on Microsoft Azure. If you want to use Google’s G Suite of web-based office productivity tools, it’s no surprise that they’re well-integrated with Google Cloud Platform.
* **1 - Neutrality**
  * Microsoft Office dominates many business spaces around the world and Google’s G Suite handles most of the others. It’s common to find that the various parts of the AWS cloud like Alexa for Business work well with both worlds. Microsoft’s Visual Studio has many devotees and so does Eclipse. AWS doesn’t play favourites and has an integration toolkit for each of them.
  * Amazon is not afraid of embracing standards and bringing them inside its big tent. If you run Microsoft SQL Server or Oracle Database, Amazon will provide what you need and won’t force you to rewrite your code to use its own proprietary storage model.
  * It’s easy to find the products of ostensible competitors running smoothly in the AWS cloud. The company’s breadth and depth is a result of being unafraid of reaching into many corners of the computing world and excellent at bringing those corners into the cloud.
* **2 - Full-service options**
  * Lately Amazon has been adding built-out services that target certain niches—like a customer service call centre, in the case of Amazon Connect.
  * They’ve already got plenty of tools for call centres, Internet of Things, mobile app support, business productivity, and, for those with their own network of orbiting satellites, a full-function “Ground Station as a Service
* **3 - Container focus**
  * All of the cloud companies understand the attractiveness of containers like Docker, but Amazon is pushing further by building a special, stripped-down version of Linux called Bottlerocketthat has just enough code to keep the machine running but not much more. Teams running microservices can choose it and quit worrying about extra cruft like FTP servers sitting around in the background. Amazon also intends to embrace containers even more by skipping over the traditional packages for security and feature upgrades.
* **4 - AWS Lambda**
  * AWS Lambda started as a cute idea, a kind of simple shell script that could glue together all of the operations in the cloud. Users quickly turned to Lambda’s serverless functions to handle occasional computing tasks because it’s so much more efficient than dedicating a machine for work that arrives sporadically.
  * Eventually people realised that Lambda could be ideal for more complicated background processing, especially the kind that would run sporadically. If a server is idling more than it’s working, switching to the serverless model could save a dramatic amount of money.
  * AWS noticed and expanded the maximum RAM for Lambda functions to 3GB and maximum running time to 15 minutes.
  * If your processing is sporadic, Lambda could be the cheapest way to host some significant jobs in the cloud. And the use cases will only continue to grow. AWS Lambda functions could already manipulate most parts of the Amazon cloud and they’re infiltrating what’s left. Amazon probably won’t stop until every part of the AWS cloud will answer to the serverless commands.
* **5 - Broad AI platform**
  *  They begin with basic tools like SageMaker for training models to respond to your data. These tools have attracted plenty of developers and that may be why the sales literature brags that “85 per cent of TensorFlow projects in the cloud run on AWS.”
  * The basic training, though, is just the beginning because AWS also offers a wide range of tools aimed at particular industries. Amazon Comprehend Medicalplows through unstructured medical texts looking for lifesaving treatments. Amazon Fraud Detection looks for malicious behaviour.
  * Developers new to AI can begin exploring with highly automated options like AutoGluon, a project from the AWS lab that is designed to make it simpler to dive in.
* **6 - 24 terabytes of RAM**
  * If you’re running very big enterprise databases or you just believe that whoever dies with the most RAM wins, some of the new high-memory machines from Amazon are just what you need. Up to 24 terabytes of RAM can be yours in just a few clicks.
* **7 - Distributed MySQL or PostgreSQL**
  * To the programmer, Amazon Aurora looks just like either MySQL or PostgreSQL. You choose the syntax and, underneath the covers, Aurora will store the data in a fast, SSD-based, virtualised storage layer. That alone is a clever idea that lets the programmers use their favourite open source version of SQL.
  * **8 - Burst models**
    * Amazon recognises that not all cloud machines are grinding through endless streams of data, all day and into the night. Many machines like web servers have periods of high demand followed by a bit of a lull.
    * Many of the EC2 machines like the T3 line are designed to be burstable, which means you have some access to extra CPU when you need it. If your average load is lower than a baseline, then CPU load spikes don’t cost any more. If your web content goes viral and the spikes turn into a sustained load, well, AWS applies a surcharge.
  * **EC2 Spot Instances**
    * If you want a new instance and you want it now, AWS offers a list price. But if you want to spend as little as possible, and the job isn’t urgent, you can put in a bid in AWS’ spot market where the prices drift up and down based upon demand.
    * Yes, it’s a bit of a pain to make sure you’ve got a high enough bid, but if you’re willing to put in the time you can rest assured that you’re saving money by getting the market clearing price. The other cloud providers offer discounts for heavy usage, but AWS lets the market find the true bottom. 
* **11 - Browser-based development**
  * While AWS continues to support the kind of command-line development that is still favoured by many developers, it is also exploring the ways of turning your browser into the IDE for the AWS cloud. AWS purchased Cloud9, the browser-based code editor, and put it in a constellation of tools for managing the deployment of all of the code you write with it.
  * When you build your Lambda functions, you can do it right in the browser without downloading anything. There are also a number of so-called “no code” options like the GraphQL API builder that lets you build your API with a few clicks. Soon you’ll be able to do pretty much everything in the same browser you use to watch cat videos.
