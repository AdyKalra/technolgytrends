## Secrets as a service

```Humans and machines use secrets throughout the value stream of building and operating software. The build pipelines need secrets to interface with secure infrastructures such as container registries, the applications use API keys as secrets to get access to business capabilities, and the service-to-service communications are secured using certificates and keys as secrets. You can set and retrieve these secrets in different ways.```

We've long cautioned developers about using source code management for storing secrets. We've recommended [decoupling secret management from source code](https://www.thoughtworks.com/radar/techniques/decoupling-secret-management-from-source-code) and using tools such as``` [git-secrets](https://www.thoughtworks.com/radar/tools/git-secrets) and [Talisman](https://www.thoughtworks.com/radar/tools/talisman) to avoid storing secrets in the source code. 

We've been using``` **secrets as a service** ```as a default technique for storing and accessing secrets. With this technique you can use tools such as [Vault](https://www.thoughtworks.com/radar/tools/hashicorp-vault) or [AWS Key Management Service (KMS)](https://aws.amazon.com/kms/) to read/write secrets over an HTTPS endpoint with fine-grained levels of access control. 

Secrets as a service uses external identity providers such as [AWS IAM](https://aws.amazon.com/iam/) to identify the actors who request access to secrets. Actors authenticate themselves with the secrets service. For this process to work, it's important to automate bootstrapping the identity of the actors, services and applications. Platforms based on [SPIFFE](https://www.thoughtworks.com/radar/platforms/spiffe) have improved the automation of assigning identities to services
