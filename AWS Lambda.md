* AWS Lambda is a **serverless compute service that runs your code in response to events and automatically manages the underlying compute resources for you**. You can use AWS Lambda to extend other AWS services with custom logic, or create your own back-end services that operate at AWS scale, performance, and security.
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
  
![How it works](https://d1.awsstatic.com/product-marketing/Lambda/Diagrams/product-page-diagram_Lambda-HowItWorks.68a0bcacfcf46fccf04b97f16b686ea44494303f.png)

![Lambda Use case](https://d1.awsstatic.com/product-marketing/Lambda/Diagrams/product-page-diagram_Lambda-IoTBackends.3440c7f50a9b73e6a084a242d44009dc0fbe5fab.png)

![Lambda working](https://image.slidesharecdn.com/awslambda-event-drivencodeinthecloud-tew-150618172126-lva1-app6891/95/a-walk-in-the-cloud-with-aws-lambda-10-638.jpg?cb=1434648341)
