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
