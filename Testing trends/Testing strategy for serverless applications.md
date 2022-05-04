[Source](https://theburningmonk.com/2022/05/my-testing-strategy-for-serverless-applications/)

As a consultant, I have helped a lot of clients with their architecture and built a couple of serverless applications for clients from scratch. And the no. 1 question I get about serverless is around testing.

“How should I test these cloud-hosted functions?”

“Should I use local simulators?”

“How do I run these in my CI/CD pipeline?”

In this post, let me share my thoughts and my approach to testing serverless applications.

Run tests locally against deployed AWS resources

There’s a lot of value in testing your code locally so you can catch problems without having to wait for a full deployment cycle and get that all-important fast feedback loop. But don’t bother with simulating AWS locally, it takes too much effort to set up and I find the result is too brittle (breaks easily) and hard to maintain.

Anecdotally, I have seen many teams spend weeks trying to get localstack running and then waste even more time whenever it breaks in mysterious ways…

Oh, and from time to time, you get weird errors in your tests because of subtle behaviour differences between localstack and the real AWS service. You can easily lose hours or days of development time when these happen.

Instead, I think it’s much better to use temporary environments (e.g. for each feature, or even each commit). This is something that I had written about a while back. Have a read of this post to see some of the benefits of using temporary environments as part of your workflow.

And remember, with serverless components you only pay for what you use, so these environments are essentially free!

In my workflow, when starting a new feature, I would create a temp environment by running the command sls deploy -s my-feature using the Serverless framework. This provisions a temporary environment in AWS in a dev account I share with other developers in the team, but the resources are dedicated to this particular feature.

I can then write tests that execute my function code locally against the real AWS services such as DynamoDB tables. As I make changes to my code, I can execute the tests to make sure they’re working before I deploy the changes to the AWS account. In fact, if you’re using jest and using VS Code as your IDE, you can even install the jest runner plugin for VS Code so the relevant tests are executed as and when you make code changes.

The only time you would need to redeploy the CloudFormation stack is when you make certain infrastructure changes, such as adding new DynamoDB tables or adding a new index to an existing DynamoDB table. This is because your code depends on these AWS resources existing in your AWS account to work. These deployments also help verify that your infrastructure code works correctly.

These “integration tests” (or “sociable tests” as Martin Fowler calls them) test your code against real AWS services and catch integration problems as well as business logic errors quickly and give you fast feedback for code changes.



But what about unit tests that use mocks and stubs?

Unit tests, or not

I generally think “unit tests” (what Martin Fowler calls “solitary tests”) don’t have a great return on investment and I only write these if I have genuinely complex business logic. Most of my Lambda functions are IO heavy and perform simple data transformations and these can be sufficiently tested by the integration tests.

However, when I’m dealing with complex biz logic, I would encapsulate them into modules and write unit tests for them and make sure these tests don’t deal with any external dependencies. They work exclusively with domain objects. And yes, I do use mocks and stubs in these tests so I can exercise the desired code paths.

End-to-end tests

Once I have good confidence that my code works, I would write end-to-end tests to check the whole system works (without the frontend) by testing the system from its external-facing interface, which can be a REST API, an EventBridge bus, or a Kinesis data stream, or whatever.

These end-to-end tests would catch problems outside of my code – configurations, IAM permissions, etc. And a lot of the time, I write tests in such a way that I can reuse the same test case for both integration and end-to-end tests so they’re not as labour intensive to produce and maintain. If you’re using a contract-first approach and designing your APIs with their consumers (e.g. the web and mobile teams) then it might be a good idea to write these end-to-end tests before you start writing the Lambda functions.

If I’m building APIs then these end-to-end tests would call the deployed API and check the response. For data pipelines, they would push events into an EventBridge bus and wait for the expected side-effect (e.g. data written to a DynamoDB table).

Again, using temporary environments really helps here. You don’t have to worry about pushing events to shared event buses that trigger lots of other stuff that you don’t intend to (like other people’s Lambda functions).

If the side-effect you’re looking for is “an event is published to Kinesis/EventBridge/SNS” then it can be tricky to detect these. Check out this old post of mine to see a few ways to do this.

CI/CD pipeline

As part of the CI/CD pipeline, I would create a temporary environment and run the integration and end-to-end tests against it. Then I would delete the environment after the tests. There’s no need to clean up test data from shared environments. If the tests passed, then I can proceed to deploy the application to the real AWS environments.

Testing honeycomb

This approach is broadly in line with and inspired by the testing honeycomb, and I have been very happy with it. It gives me the feedback speed for small code changes and the confidence I need to operate complex applications with lots of moving parts (and therefore configurations!)



Testing in production

Of course, testing doesn’t stop there!

There is a whole school of “testing in production” which includes observability, canary testing, smoke testing, load testing, chaos experiments and much more. You don’t need to do all of them, but having good observability in your application is a must.

My go-to solution is Lumigo and I use it in all of my projects. It takes only a few mins to set up, there’s no need for manual instrumentation and it gives me everything I need to troubleshoot issues that I haven’t seen before.

And I love the built-in dashboard, it’s designed by serverless users for serverless users. I can see at a glance all the important information about my application and quickly identify functions that require further inspection, e.g.

Lambda functions with a high error rate.
Lambda functions with a high percentage of cold starts.
Dependencies (services that I call from my Lambda function) that have a high tail latency and would therefore affect my application’s performance.


I can also identify functions with a high tail latency (likely affected by poor-performing dependencies above) and drill into individual invocations and figure out the root cause.



It’s been an invaluable tool for me and a big part of how I’m able to stay productive and resolve client issues on a timely basis. If you’re working with Lambda then you owe it to yourself and your team to check it out. I promise you, it will be a game-changer for you.
