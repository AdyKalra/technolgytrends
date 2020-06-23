# DoD Enterprise DevSecOps Reference Design 
## Executive Summary 
* Legacy software acquisition and development practices in the DoD do not provide the agility to deploy new software “at the speed of operations”. In addition, security is often an afterthought, not built in from the beginning of the lifecycle of the application and underlying infrastructure. 
* DevSecOps is the industry best practice for rapid, secure software development. DevSecOps is an **organizational software engineering culture** and practice that aims at unifying software development (Dev), security (Sec) and operations (Ops). The main characteristic of DevSecOps is to automate, monitor, and apply security at all phases of the **software lifecycle: plan, develop, build, test, release, deliver, deploy, operate, and monitor.**  
* In DevSecOps, testing and security are shifted to the left through automated unit, functional, integration, and security testing - this is a key DevSecOps differentiator since security and functional capabilities are tested and built simultaneously. 
* The benefits of adopting DevSecOps include: 
    * Mean-time to production: the average time it takes from when new software features are required until they are running in production. 
    * **Lead Time** Average lead-time: how long it takes for a new requirement to be delivered and deployed. 
    * Deployment speed: how fast a new version of the application can be deployed into the production environment. 
    * **Deployment frequency**: how often a new release can be deployed into the production environment. 
    * **Change Fail Rate** Production failure rate: how often software fails during production. 
    * **MTTR** Mean-time to recovery: how long it takes applications in the production stage to recover from failure. 
* In addition, DevSecOps practice enables: 
    * Fully automated risk characterization, monitoring, and mitigation across the application lifecycle. 
    * Software updates and patching at a pace that allows the addressing of security vulnerabilities and code weaknesses. 
## Purpose
* The main purpose of this document is to provide a logical description of the key design components and processes to provide a repeatable reference design that can be used to instantiate a DoD DevSecOps software factory. 
* The target audiences for this document include: 
   * DoD Enterprise DevSecOps capability providers who build DoD Enterprise DevSecOps hardened containers and provide a DevSecOps hardened container access service 
   * DoD organization DevSecOps teams who manage (instantiate and maintain) DevSecOps software factories and associated pipelines for its programs 
   * DoD program application teams who use DevSecOps software factories to develop, secure, and operate mission applications 
   * Authorizing Officials (AOs) 
* The DoD Enterprise DevSecOps reference design leverages a set of hardened DevSecOps tools and deployment templates that enable DevSecOps teams to select the appropriate template for the program application capability to be developed.  For example, these templates will be specialized around a specific programming language or around different types of capabilities such as web application, transactional, big data, or artificial intelligence (AI) capabilities. 
* A program selects a DevSecOps template and toolset; the program then uses these to instantiate a DevSecOps software factory and the associated pipelines that enable Continuous Integration and Continuous Delivery (CI/CD) of the mission application. 
## Assumptions and Principles 
### Assumptions
* For most organizations, deploying to a certified and monitored cloud environment will become their preferred solution technically and culturally. 
* Rapidly changing technology dictates designing the DevSecOps pipelines and patterns for flexibility as new development capabilities enter/exit the commercial product market. 
* The DoD Enterprise DevSecOps software factory is designed to avoid vendor lock-in and leverage Open Container Initiative (OCI) compliant containers and Cloud Native Computing Foundation (CNCF) certified Kubernetes to orchestrate and manage the containers. 
* The government must balance open source integration risks vs. using pre-integrated Commercial Off-The-Shelf (COTS) products that have vendor “cost of exit” and vendor insider risks. 
* It must be possible to host a DevSecOps software factory in any DoD general-purpose cloud environment, as well as in disconnected and classified environments.  
* The DevSecOps architecture must have the capability to scale to any type of operational requirement needing a software solution, including: Business systems o Command and Control systems o Embedded and Weapon systems o Intelligence analysis systems o Autonomous systems o Assisted human operations 
### Principles 
* There are several key principles to implementing a successful DevSecOps approach: 
   *  Remove bottlenecks (including human ones) and manual actions. 
   *  Automate as much of the development and deployment activities as possible. 
   *  Adopt common tools from planning and requirements through deployment and operations. 
   *  Leverage agile software principles and favor small, incremental, frequent updates over larger, more sporadic releases. 
   *  Apply the cross-functional skill sets of Development, Cybersecurity, and Operations throughout the software lifecycle, embracing a continuous monitoring approach in parallel instead of waiting to apply each skill set sequentially. 
   *  Security risks of the underlying infrastructure must be measured and quantified, so that the total risks and impacts to software applications are understood. 
   *  Deploy immutable infrastructure, such as containers. The concept of immutable infrastructure is an IT strategy in which deployed components are replaced in their entirety, rather than being updated in place. Deploying immutable infrastructure requires standardization and emulation of common infrastructure components to achieve consistent and predictable results. 
## Key Terms 
### DevSecOps Ecosystem 
* A collection of tools and process workflows created and executed on the tools to support all the activities throughout the full DevSecOps lifecycle.  The process workflows may be fully automated, semiautomated, or manual. 
### Software Factory 
* A software assembly plant that contains multiple pipelines, which are equipped with a set of tools, process workflows, scripts, and environments, to produce a set of software deployable artifacts with minimal human intervention. It automates the activities in the develop, build, test, release, and deliver phases. The software factory supports multitenancy. 
### CI/CD Pipeline 
* The set of tools and the associated process workflows to achieve continuous integration and continuous delivery with build, test, security, and release delivery activities, which are steered by a CI/CD orchestrator and automated as much as practice allows. 
### CI/CD Pipeline Instance 
* A single process workflow and the tools to execute the workflow for a specific software language and application type for a project. As much of the pipeline process is automated as is practicable. 
### Environment 
* Sets a runtime boundary for the software component to be deployed and executed. Typical environments include development, integration, test, pre-production, and production. 
### Software Factory Artifact Repository 
* A local repository tied to the software factory. It stores artifacts pulled from DoD Centralized Artifact Repository (DCAR) as well as locally developed artifacts to be used in DevSecOps processes. The artifacts include, but are not limited to, virtual machine (VM) images, container images, binary executables, archives, and documentation. It supports multi-tenancy. Note that programs may have a single artifact repository and use tags to distinguish the content types. It is also possible to have separate artifact repositories to store local artifacts and released artifacts. 
### Code 
Software instructions for a computer, written in a programming language. These instructions may be in the form of either human-readable source code, or machine code, which is source code that has been compiled into machine executable instructions. 
### Containers 
* A standard unit of software that packages up code and all its dependencies, down to, but not including the Operating System (OS). It is a lightweight, standalone, executable package of software that includes everything needed to run an application except the OS: code, runtime, system tools, system libraries and settings. Several containers can run in the same OS without conflicting with one another.  
![Containers]() 
Figure 1: Containers 
* Containers run on the OS, so no hypervisor (virtualization) is necessary (though the OS itself may be running on a hypervisor).  Containers are much smaller than a VM, typically by a factor of 1,000 (MB vs GB), partly because they don’t need to include the OS. Using containers allows denser packing of applications than VMs.  Unlike VMs, containers are portable between clouds or between clouds and on-premise servers. This helps alleviate Cloud Service Provider (CSP) lock-in, though an application may still be locked-in to a CSP, if it uses CSPspecific services. Containers also start much faster than a VM (seconds vs. minutes), partly because the OS doesn’t need to boot. 
