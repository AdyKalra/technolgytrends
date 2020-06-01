## Infrastructure as Code
* Although infrastructure as code is a relatively old technique, it has become vitally important in the modern cloud era where the **act of setting up infrastructure has become the passing of configuration instructions to a cloud platform.**
* When we say "as code" we mean that all the good practices we've learned in the software world should be applied to infrastructure. Using source control, adhering to the DRY principle, modularization, maintainability, and using automated testing and deployment are all critical practices. 
* Those of us with a deep software and infrastructure background need to empathize with and support colleagues who do not. Saying "treat infrastructure like code" isn't enough; we need to ensure the hard-won learnings from the software world are also applied consistently throughout the infrastructure realm.
* Examples of infrastructure-as-code tools include AWS CloudFormation, Red Hat Ansible, Chef, Puppet, SaltStack and HashiCorp Terraform. **Some tools rely on a domain-specific language (DSL), while others use a standard template format, such as YAML and JSON.**
  * Codify everything.
  * Document as little as possible.
  * Maintain version control.
  * Continuously test, integrate, and deploy.
  * Make your infrastructure code modular.
  * Make your infrastructure immutable (when possible)
  
* **Immutable infrastructure** is an approach to managing services and software deployments on IT resources wherein components are replaced rather than changed.
  * What if this application had state? What if this app was writing to its local disk and it had data that mattered to the application. Here what we said is, we create a new machine, delete that machine, including its data, including its disk. That clearly doesn't work.
  * To make this effective, what you generally need to do is externalize the data. Instead of it being on box with the same application, maybe I use an external database that's shared. 

### The benefits of Infrastructure-as-Code
* There are several benefits of using IaC over a CLI/SDK approach:
 * Standardised components mean there are fewer (or only one) ways of specifying a particular higher-level concept (e.g. an API Gateway route that's handled by a Lambda function). This can typically be achieved with minimal (usually declarative) code.
 * IaC templates are parameterisable to allow for differences between environments.
 * IaC tools allow for dependency chains between cloud resources to be built into them and many can determine these dependencies automatically for you.
 * Most IaC tools have pre-deployment checks built into them to prevent misconfigurations.
 * Many IaC tools provide transactional deployments of groups of resources (stacks), allowing deployments to be more atomic.
 * IaC deployments are typically incremental and idempotent — they calculate the changes between the deployed resource set and the IaC configuration file and only deploy the necessary changes.
 * Stack-based deployments enable quicker teardown of environments.
 * Many IaC tools execute the deployment steps cloudside as a hosted service and not on a developer's workstation or centralised build machine. So you don't need to worry about a build machine dying mid-deploy.
 * IaC templates for serverless apps are valuable from an earlier stage of the development lifecycle (as soon as a developer is setting up their personal dev environment) and are not just for when the app is being deployed to test, staging or production environments.

