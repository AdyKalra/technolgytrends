* Implement an API gateway that is the single entry point for all clients. The API gateway handles requests in one of two ways. Some requests are simply proxied/routed to the appropriate service. It handles other requests by fanning out to multiple services.
* The API gateway might also implement security, e.g. verify that the client is authorized to perform the request

* NGINX, Kong, Tyk, Ambassador, AWS API gateway

![APIG](https://microservices.io/i/apigateway.jpg)

### Variation: Backends for frontends
* A variation of this pattern is the Backends for frontends pattern. It defines a separate API gateway for each kind of client.
![BFF](https://microservices.io/i/bffe.png)

### Resulting context
* Using an API gateway has the following benefits:
  * Insulates the clients from how the application is partitioned into microservices
  * Insulates the clients from the problem of determining the locations of service instances
  * Provides the optimal API for each client
  * Reduces the number of requests/roundtrips. For example, the API gateway enables clients to retrieve data from multiple services with a single round-trip. Fewer requests also means less overhead and improves the user experience. An API gateway is essential for mobile applications.
  * Simplifies the client by moving logic for calling multiple services from the client to API gateway
  * Translates from a “standard” public web-friendly API protocol to whatever protocols are used internally

* The API gateway pattern has some drawbacks:
  * Increased complexity - the API gateway is yet another moving part that must be developed, deployed and managed
  * Increased response time due to the additional network hop through the API gateway - however, for most applications the cost of an extra roundtrip is insignificant.
Issues:

How implement the API gateway? An event-driven/reactive approach is best if it must scale to scale to handle high loads. On the JVM, NIO-based libraries such as Netty, Spring Reactor, etc. make sense. NodeJS is another option.

### Scenarios where API Gateways are applicable.

* **Reverse Proxy** — This is the single most important reason why most projects adopt a gateway sort of a solution. Any mature project, which has opened its APIs to the outside world would avoid exposing its back-end URLs for security reasons and abstracting the complexity of back-end services to client applications. This also gives a single point of entry to all clients accessing back-end APIs.
* **Load balancing** — Gateways can route a single incoming URL to multiple back-end destinations. This is often useful in micro-services architecture when you want to scale up your application for high-availability or even other-wise if you are running some sort of cluster server setup.
* **Authentication and Authorization** — Gateways should be able to successfully authenticate and allow only trusted clients to access APIs and also able to provide some sort of authorization layer using something like RBACs.
* **IP Listing** — Allow or Block certain IP addresses to pass through. Provides an additional layer of security to your ecosystem, useful when you discover a malicious set of addresses trying to bring down your application by using DDoS sort of attacks.
* **Analytics** — Provide a way to log usage and other useful metrics related to API calls. Should be able to disintegrate the API usages made per client for possible monetization.
* **Rate-Limiting** — Ability to throttle API calls, for example, you only want to allow 10000 calls per minute for all consumers or 1000 calls per month for a particular consumer.
* **Transformation** — Ability to transform either request and responses(including header and body) before forwarding them further.
* **Versioning** — An option to use different versions of API at the same time or possibly provide a slow rollout of API in form of Canary release or Blue/Green deployments
* **Circuit Breaker** — Useful with micro-services architecture pattern to avoid disruption in service
* **WebSocket support** — Many dynamic and real-time capabilities can be addressed by using WebSockets, providing a WebSocket interface to end clients can really reduce overheads of multiple HTTP calls for frequent data transfers
* **gRPC support** — Google’s gRPC promises to further reduce load by making use of HTTP/2, can be used efficiently for inter-communication between services. I would recommend this is something you should definitely add to your list of requirements to make your solution future proof
* **Caching** — Will further reduce the network bandwidth and round trip time consumption and improve performance if frequently requested data can be cached
* **Documentation** — If you plan to expose your APIs to developers outside of your organization, then you must think about using API documentation such as Swagger or OpenAPI.


* Amazon API Gateway is an AWS service for **creating, publishing, maintaining, monitoring, and securing REST, HTTP, and WebSocket APIs at any scale.**
* An API Gateway is a **server that is the single entry point into the system**. ... The API Gateway is **responsible for request routing, composition, and protocol translation.** All requests from clients first go through the API Gateway. It then routes requests to the appropriate microservice

### Input validation
* One of the most crucial security principles is never trusting user input. So you probably have some code validating user input at the beginning of the Lambda function. **Instead of invoking the Lambda function to validate user input and return errors, we can validate the input using API Gateway in the first place and avoid unnecessary Lambda invocation.**
  * First, we need to define the model of our desired user input so that API Gateway can use it to do the validation.
  * Next, we need to bind the model to the endpoint we want to do the validation.

### Getting record from DynamoDB
* Querying record from DynamoDB should be one of the most common API use cases. 
* API Gateway can help us translate query string from user input into DynamoDB query. And translate the result into our desire format to the user.
  * Step 1: Create an IAM role
  * Step 2: Require query string parameters from users
  * Step 3: Transform user input into DynamoDB API call
  * Step 4: Transform query result to the API response
### Costs
* For many web applications, most of the traffic is read traffic. If we implement them in API Gateway, we can save the cost of those unnecessary Lambda invocations.

### Concurrency
* You may notice that API Gateway gives you 5000 burst concurrency. However, if every API call ends up in a Lambda function, this concurrency becomes 1000 because Lambda only gives you this amount of concurrency.

* By lifting those simple API calls (especially the read traffics) away from Lambda, we can reserve the precious Lambda concurrency to more complex tasks.

### Can AWS API Gateway Act as a Load Balancer?
* Yes and costs more
* API Gateway can manage and balance out network traffic just as a Load Balancer, just in a different way. Instead of distributing requests evenly to a set of backend resources (e.g. a cluster of servers), an API Gateway can be configured to direct requests to specific resources based on the endpoints being requested.
* It plays an important role in microservices architectures, for example. Multiple services can be connected to the Gateway and mapped to particular HTTP endpoint representations. The Gateway is responsible for routing each request, on-demand, to the appropriate backend service.

![API gateway](https://d1.awsstatic.com/serverless/New-API-GW-Diagram.c9fc9835d2a9aa00ef90d0ddc4c6402a2536de0d.png)


### Nginx
* Nginx has been one of the best choices for L7 proxy, load-balancing and creating a single point entry for your back-end applications for quite some time now. It has already been used and tested in many different production environments and has replaced many existing hardware load-balancers with very low footprint and reducing a lot of cost to companies. Lot of CDNs use Nginx as their engine for caching data at edge locations.
* The biggest advantage of using Nginx as a gateway is its ability to range from simple to complex features, allowing you to cherry-pick only the required features as you progress. For example, if you only need load-balancing and reverse-proxy, to begin with, Nginx does this very easily with minimal overheads and you can eventually upgrade to other features as your product matures. You can also start with a full blown API gateway using their commercial offering, NGINX Plus, even though it is possible to achieve this with its open source offering using its wide range of available plugins.
* Nginx is known for its small footprint and ability to meet high performance with low latency. You also get a lot of 3rd party custom Nginx plugins which can cover a wide range of custom scenarios, and of course, you could always seek help from a huge network of its developer community in case you are stuck somewhere. The only possible cons that you might encounter while working with Nginx is the configuration might be a little difficult to get hang of until and unless you have got your hands dirty working with it, you will have to go over few pages of their documentation till you can claim your mastery over it.
### Kong
* Kong is an Nginx and OpenResty based API gateway plus Service Mesh which caters for most of our requirements listed above. It was quite an easy install following the provided docker installation instructions.
* Kong architecture is quite simple to understand and is made up of a few components…
* Kong base-module which wraps OpenResty and Nginx and is the engine which does the actual work
* Database layer with choice of Cassandra or Postgres to store all the configuration so it can be retrieved easily in case of failures
* Dashboard which provides User-Interface for API administration and viewing analytics (part of the enterprise offering only, though kong provides REST APIs for managing services, upstream APIs and its consumers )
* Kong has both Open-source and Enterprise versions of its implementation, both work very well with sub-millisecond latency as it is powered by nginx itself. Imagine using Nginx for your gateway operations but with REST APIs and database layer for managing configurations easily.
* Kong comes with a variety of plugins, which can cater for most of your crosscutting concerns ranging from access controls, security, caching to documentation. It also lets you write and use custom plugins using Lua language. Kong open-source is a good start to get familiar with their stack. Though it does not come with a Web-UI dashboard, there are few open source dashboards available which help you manage its configuration, otherwise if you are quite comfortable with REST you can work with their admin APIs directly.
* Kong can also be deployed as Kubernetes Ingress and supports gRPC and Websockets proxy. Kong’s advantage is its underlying engine is made up of lightweight yet powerful Nginx + OpenResty engine, which in itself can be built as a full-fledged API gateway. You can think of Kong as an auto-shift version of Nginx. A possible disadvantage of their implementation is not all the features come out-of-box, rather has to be manually configured by activating each of its respective plugins, which might need initial setup time and resources, but then this might not really a big hurdle for a lot of mature engineering teams.
### Tyk
* Tyk is another open-source gateway which promises excellent performance and is created in Go programming language. Tyk offers multiple features which are part of our requirements list and beyond. Tyk’s web dashboard is one of the best in class and lets you control almost all aspects of API configuration provides excellent analytics of API usages.
* Tyk has a rich feature set along with nice Web-UI dashboard making it a good choice for projects having a complicated API management scheme. What makes Tyk stand out is it includes API dashboard, analytics, security, versioning, developer portal, rate-limiting and other gateway features out-of-box for free if you only intend to use this for non-commercial purpose. However, for commercial usage, you will need to buy their commercial license which also includes support.
* Tyk can be really a good fit for projects looking for these features out-of-box from day one and are ready to spend for it(i.e you are planning to use it for commercial purpose), rather than explore options such as Nginx and Kong which can take little bit of your developers time to get all the required features working. Where Tyk falls short in comparison to the previous two implementations, are ease of installation and cost. Tyk has too many components which do not make it that easy to install and manage on-premise. It also has a cloud and hybrid installation options which decreases installation and management overheads, but then it comes with its own pricing and increases your project costs.
### Ambassador
* Ambassador is an open-source, Kubernetes native microservices gateway built on top of Envoy. It can be used as Kubernetes Ingress and load balancer and is built to publish and test microservices easily and rapidly on top on Kubernetes environment.
* Ambassador is very lightweight and all of its states is stored in Kubernetes, so there is no need for a database. Ambassador was built keeping the developer in mind, so all of its operations and concepts are more developer-centric, for example - the most recommended technique for adding a route on Ambassador is via annotations on Kubernetes services yamls. Its free version comes with features such as versioning, gRPC, and WebSockets support, Authentication, Rate-Limiting and Integration with Istio to work as Service Mesh, whereas features such as OAuth, single sign-on, JWT authentication, access control policies, and filtering are part of its paid version called Ambassador Pro.
* Its advantages are its ability to serve large traffic with low footprint and minimal setup configuration on Kubernetes environments, whereas where it lacks is not being as feature rich in comparison to previously discussed gateways as it is missing out-of-box dashboard and integration with analytics which will require some setup.
### Amazon API Gateway
* Amazon API gateway is an AWS cloud offering of managed API management which lets you create, publish and manage APIs in a matter of few clicks. You can currently expose REST or WebSocket endpoint, import new APIs using Swagger or Open API, Route your URL to various back-ends including AWS EC2, AWS lambda or even your in premise endpoints. The cost of routing million APIs through the gateway is very low and predictable as there is fixed pricing model for a given number of requests (though you should be careful about costs incurred due to external data transfers).
* AWS API gateway requires no setup as it is all managed, you can quickly create or route APIs in few clicks, secure them using SSL, provide Authentication and Authorization, create API Keys for external clients of your APIs, manage versioning of your APIs and also generate client SDKs if you wish to do so. AWS API gateway really packs a punch with its offering, making it really easy to setup an API gateway in a matter of few minutes. So if you are already on AWS or planning to go to AWS, you must really think about using this gateway as your first choice unless you have some mandatory feature requirements that it cannot fulfill as of yet. The obvious disadvantage being that you might get locked in with AWS service and this dependency might make your migration task to some other framework difficult at a later point in time.

![APIG all](https://miro.medium.com/max/700/1*0m4LXv5VZAl2sDzQT-jXGA.png)
