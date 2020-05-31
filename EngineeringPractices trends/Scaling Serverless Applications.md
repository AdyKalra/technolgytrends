# Best practices for organizing larger serverless applications
* Well-designed serverless applications are **decoupled**, **stateless**, and **use minimal code**.

## Organizing your code repositories
* Many serverless applications begin as monolithic applications. 
  * This can occur either because a simple application has grown more complex over time, 
  * or because developers are following existing development practices. 
  * A monolithic application is represented by a single AWS Lambda function performing multiple tasks, and a mono-repo is a single repository containing the entire application logic.

* Using frameworks such as the AWS **Serverless Application Model (SAM)** or the Serverless Framework can make it easier to group common pieces of functionality into smaller services. Each of these can have a separate code repository. 
  * For SAM, the **template.yaml** file **contains all the resources and function definitions needed for an application.** 
  * Consequently, breaking an application into microservices with separate templates is a simple way to split repos and resource groups.
  ![SAM](https://d2908q01vomqb2.cloudfront.net/1b6453892473a467d07372d45eb05abc2031647a/2020/05/13/bp1-1024x285.png)
  
## Using AWS services instead of code libraries
* AWS services are important building blocks for your serverless applications. These can frequently provide greater scale, performance, and reliability than bundled code packages with similar functionality.
  * For example, many web applications that are migrated to Lambda use web frameworks like Flask (for Python) or Express (for Node.js). Both packages support routing and separate user contexts that are well suited if the application is running on a web server. Using these packages in Lambda functions results in architectures like this:
![NonAWS](https://d2908q01vomqb2.cloudfront.net/1b6453892473a467d07372d45eb05abc2031647a/2020/05/13/bp2.png)
* API Gateway is also capable of validating parameters, reducing the need for checking parameters with custom code. It can also provide protection against unauthorized access, and a range of other features more suited to be handled at the service level. When using API Gateway this way, the new architecture looks like this:
![API Gateway](https://d2908q01vomqb2.cloudfront.net/1b6453892473a467d07372d45eb05abc2031647a/2020/05/13/bp3.png)

### Similarly, you should usually avoid performing workflow orchestrations within Lambda functions.
![workflow orchestrations](https://d2908q01vomqb2.cloudfront.net/1b6453892473a467d07372d45eb05abc2031647a/2020/05/13/bp4.png)

* A better approach is to use **AWS Step Functions**, which can represent complex workflows as JSON definitions in the application’s SAM template. This service reduces the amount of custom code required, and enables long-lived workflows
![Step Functions](https://d2908q01vomqb2.cloudfront.net/1b6453892473a467d07372d45eb05abc2031647a/2020/05/13/bp5.png)

### Using multiple AWS accounts for development teams
* First, it is highly recommended to use more than one AWS account. Using AWS Organizations, you can centrally manage the billing, compliance, and security of these accounts. You can attach policies to groups of accounts to avoid custom scripts and manual processes. * One simple approach is to provide each developer with an AWS account, and then use separate accounts for a beta deployment stage and production:
![accounts](https://d2908q01vomqb2.cloudfront.net/1b6453892473a467d07372d45eb05abc2031647a/2020/05/13/bp6-1024x235.png)

  * The developer accounts can contains copies of production resources and provide the developer with admin-level permissions to these resources. 
  * Each developer has their own set of limits for the account, so their usage does not impact your production environment. 
  * Individual developers can deploy CloudFormation stacks and SAM templates into these accounts with minimal risk to production assets.
  * This approach allows developers to test Lambda functions locally on their development machines against live cloud resources in their individual accounts. 
  * It can help create a robust unit testing process, and developers can then push code to a repository like AWS CodeCommit when ready.
  * By integrating with AWS Secrets Manager, you can store different sets of secrets in each environment and eliminate any need for credentials stored in code. 
    * As code is promoted from developer account through to the beta and production accounts, the correct set of credentials is automatically used. You do not need to share environment-level credentials with individual developers.

### Managing feature releases in serverless applications
* As you implement CI/CD pipelines for your production serverless applications, it is best practice to favor safe deployments over entire application upgrades. Unlike traditional software deployments, serverless applications are a combination of custom code in Lambda functions and AWS service configurations.

  * **A feature release may consist of a version change in a Lambda function.**
  * It may have a different endpoint in API Gateway, or use a new resource such as a DynamoDB table. 
  * Access to the deployed feature may be controlled via user configuration and feature toggles, depending upon the application. 
  * AWS SAM has AWS CodeDeploy built-in, which allows you to configure canary deployments in the YAML configuration:
