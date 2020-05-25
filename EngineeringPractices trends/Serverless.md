## Serverless 
* The term 'serverless' is somewhat misleading, as there are still servers providing these backend services, but all of the server space and infrastructure concerns are handled by the vendor. Serverless means that the developers can do their work without having to worry about servers at all. - **managed services**

### Typical Serverless architecture in web

![Typical Serverless](https://miro.medium.com/max/3780/1*JxDFqhb95iPclzr2FJcQAQ.png)

* A block represents a typical and clearly delimited **domain or technical feature** that could be found in most serverless architectures. They don’t necessarily represent micro-services, or stacks in CloudFormation lingo

#### The Serverless Framework
* It does most of the basic Infrastructure as Code (IaC) heavy lifting (on top of CloudFormation). 
* Define a Lambda reacting to a HTTP event, the Serverless Framework will automatically deploy the related API Gateway resource and corresponding route along with the new Lambda.
* And when we are reaching the framework limits, and want a more complex service configuration, we can simply add some CloudFormation.

#### Fine-grained lambda functions…
* A Lambda is a function. It has one job and does it well. Our front-end needs to retrieve a list of items? Make a Lambda for it. We need to send a confirmation email after a user was registered? Make another Lambda for it. 
* Of course some specific code (like data entities) can be factorised and shared in a dedicated utilities folder, but pay a very close attention to this code, because any change will impact all related Lambdas and as Lambdas can be tested and deployed independently, we may miss something.

#### Split in Micro-services…
* To not have teams stomping on each other, to not have a huge package.json and serverless.yml (CloudFormation has a 200 resources limit), a crazy long CloudFormation deploy time, in order to find ourselves better in our codebase and to enforce clear responsibilities between our Lambdas: we define boundaries splitting our project in Micro-Services. 
* In our mono-repository: one micro-service = one CloudFormation stack = one serverless.yml + package.json. In addition, a micro-service masters its own data entities not shared with the other micro-services.

#### …communicating in an Event-driven manner
* Those micro-services need to be fully independent, if one is down, or if we are making breaking changes in another, the impact on the rest of the system should be as limited as possible. 
* To help with that, Lambdas communicate with one another only through **EventBridge, a serverless event bus.** 
![EventBridge](https://miro.medium.com/max/1000/1*qXOIVaIRcFFdSjyPBrIO3A.png)

#### Frontend (development)
* Our shiny serverless backend has somehow to feed a frontend. To ease our frontend development coupled to AWS, we take advantage of Amplify.**Amplify** is several things: a CLI tool, an IaC tool, an SDK and a set of UI components. We leverage the frontend JS SDK to make integration with resources (e.g. Cognito for authentication) deployed via other IaC tools (like the Serverless Framework) faster.
![Frontend](https://miro.medium.com/max/1000/1*mwsSyS9ne7IieUzfAMGBLg.png)

#### Website hosting
* Most of today’s websites are **Single Page Applications (SPA)**, which are fully featured dynamic applications packaged in one set of static files downloaded by the user’s browser at first URL access. 
* In an AWS environment, we host those files on S3 (a file storage) exposed through **CloudFront (Content Delivery Network (CDN)).**
* That being said, the trend is clearly leaning toward Server(less) Side Rendering (SSR) websites like Next.js. To set-up a SSR website in serverless we take advantage of **Lambda@Edge within CloudFront.** This allows us to do server-side rendering with Lambdas as close as possible to our end users. 
![hosting](https://miro.medium.com/max/1000/1*Pgzx2ChyyC4dBGtmcBNoYw.png)

#### Domain and certificate
* For our website we want something better than the raw auto-generated S3 URL, to do that we generate and bind our certificates to **CloudFront with Certificate Manager**, and manage our domains with **Route 53.**
![certificate](https://miro.medium.com/max/1000/1*yIf5M_YTOHwWD-nsnq8p_Q.png)

#### Business API
* Now, our website has to get in touch with a back-end to retrieve and push data. To do so we use **API Gateway to handle the HTTP connections and routes, synchronously triggering a Lambda for each route.** 
* Our Lambdas contain our business logic communicating with DynamoDB in order to store and consume data.
* As said above, we are event-driven, which means that we quickly reply to our user, and behind the scene continue to treat the request asynchronously. **DynamoDB for instance exposes streams which can asynchronously trigger a Lambda to react on any data change. Most serverless services have a similar capability.**
![asynchronously](https://miro.medium.com/max/1000/1*7C77e77K3XkBj4UhZ1aWvg.png)

#### Asynchronous tasks
* Our architecture is event-driven, so a lot of our Lambdas are asynchronous and **triggered by EventBridge events, S3 events, DynamoDB Streams**, etc. 
* We could for instance have an asynchronous Lambda responsible for dispatching a welcome email on a successful sign-up.
* Failure handling is critical in a distributed asynchronous system. So for async Lambdas, we use their **Dead Letter Queue (DLQ)** and pass the final failure message first to **Simple Notification Service (SNS)** then passing it to **Simple Queue Service (SQS)**. We have to do that for now because it’s not yet possible to attach SQS directly to a Lambda DLQ.
![Asynchronous](https://miro.medium.com/max/1000/1*8elWex3BkrLYQM5CfF5FxQ.png)

#### Back-end to front-end push
* With asynchronous operations, the frontend can no longer just display a loader while waiting for an XHR response to come. 
* We need pending states and data push from the backend. To do so we take advantage of the **WebSocket API of API Gateway**, which keeps the WebSocket connection alive for us and only triggers our Lambdas on messages. 
![Backend to frontend push](https://miro.medium.com/max/1000/1*HjOkVtx6PlyfH62YAf-NuA.png)

#### File upload
* Instead of handling the file upload stream from a **Lambda, which might get costly,** S3 offers the possibility for Lambdas to generate a signed (secured) upload URL that will be used by our front-end to directly upload the file to S3. 
* As most AWS services, the nice part is that another asynchronous Lambda can listen to a S3 file change event to handle any subsequent operations.
![File upload](https://miro.medium.com/max/1000/1*4mWb2t6Sg46hofoLjYAcSg.png)

#### Users and authentication
* **Cognito** has everything we need: authentication, user management, access control and external identity provider integration. Although known for being a tad complicated to use, it can do so much for us. And as usual, it has a dedicated SDK to have Lambdas interact with it, and can dispatch events to trigger Lambdas.
* In our example, we illustrate the possibility to bind native Cognito authorizers to our API Gateway routes. We also exposed a Lambda to refresh authentication tokens and another Lambda to retrieve a list of users.
![authentication](https://miro.medium.com/max/1000/1*wJqmHXUIeDaSP6DmVVZQTw.png)

#### State machine
* In some situations, our logic and data flow might get quite complicated. **Instead of operating this flow manually directly inside our Lambdas, hence having a hard time following and structuring what is happening,**
* AWS has a service just for us: **Step Functions.**
* We declare our state machine through CloudFormation: every subsequent steps and states, every expected or unexpected results, and attach to those steps some native actions (like wait or choice) or a Lambda (among several integrations). 
* We can then see our machine run live and visually (with logs) through the AWS interface. At each of those steps we can define retry and failure handling. 
* To give a more concrete example, let’s say we want to send an email campaign with a SaaS and make sure that this campaign has been sent:
  - Step 1 - Lambda: asks the SaaS to send an email campaign and retrieves a campaign id
  - Step 2 - Task Token Lambda: gets a callback token from the Step Function, links it to the campaign id, then waits for a callback from the SaaS
  - Step 3 (outside the flow) - Lambda: called by a hook from the SaaS on campaign status change (pending, archived, failed, success), resumes the flow with the campaign status using the associated callback token
  - Step 4 - Choice: based on status, if the campaign is not yet successful, back to step two
- Step 5 (final) - Lambda: on campaign sent, updates our users
![state machine](https://miro.medium.com/max/1000/1*uHskJ3OHAQ6X4FrYZ0xdiw.png)

#### Security
* **Identity & Access Management (IAM)** is here to help us manage with fine granularity any AWS access, whether they are developers, CI/CD pipelines or AWS services calling each other. 
* Regarding very sensitive data, like a SaaS api key, we safely store it in the **Parameter Store of Systems Manager**. And request them from inside our Serverless and CloudFormation files, or even from within our code with the associated SDK. It’s useful to mention that Secrets Manager does a similar job. And Key Management Service (KMS) is here to help us manage our encryption keys.
![Security](https://miro.medium.com/max/1000/1*exbgMDtrlsW4dxm0hwxT-A.png)

#### Monitoring
* **Cloudwatch** is the de facto monitoring service. All AWS services have basic automatic metrics and logs sent to CloudWatch to give us some basic informations. We can go much further than that: send custom metrics and logs, create dashboards, trigger alarms on thresholds, make complex queries to dig through the data and display it in custom graphs.
* We are still on the lookout for other options. **X-Ray** for instance, whose objective is to track requests end-to-end through our entire distributed system, then represent it in a very visual and dynamic way. Only that at the moment this tracking gets lost because some services like EventBridge (which is central in our architecture) are not yet supported. 
* Another service, **ServiceLens**, builds on top of X-Ray and CloudWatch, and looks terrific. There are also some promising external (to AWS) solutions like Thundra, Epsagon or Lumigo, but we did not have the chance to fully try them yet.
![Monitoring](https://miro.medium.com/max/1000/1*zHJt35_dyHBwKyqY5OBsfw.png)
