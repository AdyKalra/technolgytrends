### Infrastructure as Code
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
