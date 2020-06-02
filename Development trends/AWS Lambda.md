* AWS Lambda is a **serverless compute service that runs your code in response to events and automatically manages the underlying compute resources for you**. You can use AWS Lambda to extend other AWS services with custom logic, or create your own back-end services
that operate at AWS scale, performance, and security.
* Two of the reasons why Lambdas are so attractive are their **auto-scale (in & out) capability and their pay-per-use pricing model**
* [Lambda on slideshare](https://www.slideshare.net/AmazonWebServices/a-walk-in-the-cloud-with-aws-lambda)
* AWS Lambda is a **compute service that lets you run code without provisioning or managing servers**. AWS Lambda **executes your code only when needed and scales automatically**, from a few requests per day to thousands per second. You pay only for the compute time you consume - there is no charge when your code is not running.
* AWS Lambda functions execute in a container (sandbox) that isolates them from other functions and provides the resources, such as memory, specified in the function's configuration.
*  For most periodic or very light workloads, **Lambda is dramatically less expensive than even the smallest EC2 instances. Focus on the memory and execution time that a typical transaction in your app will need** to relate a given instance size to the break-even Lambda cost.
* AWS Lambda functions can be configured to **run up to 15 minutes per execution. You can set the timeout to any value between 1 second and 15 minutes.
* **How long does AWS Lambda stay warm? approximately 5 minutes**
  * Non-VPC functions are kept warm for approximately 5 minutes whereas VPC-based functions are kept warm for 15 minutes. Set your schedule for invocations accordingly. There is no need to ping your functions more often than the minimum warm time.
* Minimizing the Frequency of Cold Starts
  * Don't invoke the function more often than once every five minutes.
  * Invoke the function directly with Amazon CloudWatch Events.
  * Pass in a test payload when running the warming.
  * Create handler logic that doesn't run all function logic when it is running the warming.
  
 ## Lambda Best Practices
 ### Testing
 * Really strong stance against using local mocking libraries. Plain and simple, local mocking libraries are a bad idea. Using those libraries for building local tests can be great for experimentation, but once you rely on those, then you have created more complex testing setups. If you are calling an API, it is likely just returning JSON. Instead of using a library, simulate that JSON statically, test against it, and then you know the response is always the same and it isn’t going to change because of some update to localstack or some other local mocking library.
* Integration tests are also important with serverless applications, given the different connectivity pieces and services communicating with each other. But it’s also possible to simulate complex workflows locally using functional tests. In most cases, we just need to know: **“If this Lambda function receives this event, does it do what it’s supposed to do?”** That is relatively easy with functional tests, which is testing how a bigger part of the application responds to the system around it without actually running the entire system around it. The most important takeaway is to design and build your applications so that they can be easily tested.

### Mythbusting Cold Starts
* Another thing we discuss is that the vast majority of our Lambda functions now run asynchronously, so the user isn’t waiting on a response. In these cases, cold starts generally don’t matter at all. 
* Also if all you’ve ever used Lambda for is synchronous APIs, then you’re missing about 95% of what Lambda is about.

### The Caveats around Provisioned Concurrency
*  it took an extra 1.5-2 minutes to deploy a single provisioned concurrency Lambda function, and an extra four minutes to deploy a function set to 50. It’s also rather expensive. With Lambda functions, you only pay when they are used, but with provisioned concurrency, you’re always paying a flat fee plus execution time, so you have to be very aware of the economics.
* There’s also the added benefit of using provisioned concurrency to pre-warm a pool of Lambda functions if you are anticipating a big traffic spike.

### When to use (or not use) Custom Runtimes
* Mike also points out that if you use your own custom runtime, then you also have to maintain it. Updates happen automatically with AWS’s standard Java runtimes, but with something custom, you’ll likely need to do some testing when the underlying environment is updated.

### Multi-Module, Multi-Function Lambda Applications that Share Code
* Really interesting solution to create multi-module, multi-function serverless Java applications. Mike offers a scenario: if you have 10 different types of requests, consider having 10 different Lambda functions. This way, each Lambda function can follow the principle of least privilege and only access the things it needs. Plus, you can reduce cold starts because you’re only loading up the code and the libraries that each Lambda function actually needs – and that makes a difference.

![How it works](https://d1.awsstatic.com/product-marketing/Lambda/Diagrams/product-page-diagram_Lambda-HowItWorks.68a0bcacfcf46fccf04b97f16b686ea44494303f.png)

![UC](https://d1.awsstatic.com/product-marketing/Lambda/Diagrams/product-page-diagram_Lambda-WebApplications%202.c7f8cf38e12cb1daae9965ca048e10d676094dc1.png)

![Lambda Use case](https://d1.awsstatic.com/product-marketing/Lambda/Diagrams/product-page-diagram_Lambda-IoTBackends.3440c7f50a9b73e6a084a242d44009dc0fbe5fab.png)

![Lambda working](https://image.slidesharecdn.com/awslambda-event-drivencodeinthecloud-tew-150618172126-lva1-app6891/95/a-walk-in-the-cloud-with-aws-lambda-10-638.jpg?cb=1434648341)
