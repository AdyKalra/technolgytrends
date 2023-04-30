
## Infrastructure-as-apps 
It builds on infrastructure-as-code to a logical endpoint by bringing in principles of GitOps management. The term is something that was coined in 2021 to describe an existing movement to bring infrastructure into the same lifecycle control as applications under GitOps. 

** Examples of Infra-as-apps tools include Argo CD, Crossplane, Cluster API, Cello, or even SchemaHero for databases and the list is always growing.

### Some of the benefits of infra-as-apps include

* Dramatically easier infrastructure management
* Better security
* Easier onboarding and resource provisioning for devs
* Faster mean time to recover (MTTR)
* Ironclad auditability
* Better cost management
* Cross-cloud and easier migration

**Infra-as-apps = IaC + GitOps! **
- Treating your infrastructure like an application and managing them with GitOps is totally possible with infra-as-apps.

### Infra-as-apps is a game-changer
Managing infrastructure has long been treated differently from the applications they run. There is a common division of labor between infrastructure and applications. Updates to applications are more frequent and often get more attention from CI/CD. The underlying infrastructure is often left in a set once and forget model. Automating infrastructure in a fully-GitOps compliant way is difficult so it is left behind and treated differently than the application layer.

Now all infrastructure doesn’t just get treated like code, it is actually monitored like apps via GitOps operators. This has implications across the entire development process.

https://codefresh.io/blog/infrastructure-as-apps-the-gitops-future-of-infra-as-code/

Infrastructure-as-apps is really a term meant to distinguish for the confusion that exists around GitOps and Infra-as-Code. It goes beyond infra-as-code to fully implement GitOps at every level. GitOps requires an operator to constantly monitor the actual state and compare it to the desired state. Most infrastructure-as-code implementations stop at a classic CI/CD approach that merely pushes changes and is oblivious to how successfully plans were applied, or if someone has made changes to production manually.

Infra-As-Apps on the other hand would view manual changes to infrastructure as a divergence from the desired state as set in git. Attackers would find changes to infra much more difficult if they’re always reverted automatically. Likewise, developers will find provisioning resources much easier, and operations teams will find changes much more predictable and the clarity of usage much easier to understand when implementing Infrastructure-as-apps.

