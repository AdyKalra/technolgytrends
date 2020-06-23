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
![Containers](https://user-images.githubusercontent.com/8856857/85359727-65edf880-b55a-11ea-8252-489581280a1a.jpg) 
Figure 1: Containers 
* Containers run on the OS, so no hypervisor (virtualization) is necessary (though the OS itself may be running on a hypervisor).  Containers are much smaller than a VM, typically by a factor of 1,000 (MB vs GB), partly because they don’t need to include the OS. Using containers allows denser packing of applications than VMs.  Unlike VMs, containers are portable between clouds or between clouds and on-premise servers. This helps alleviate Cloud Service Provider (CSP) lock-in, though an application may still be locked-in to a CSP, if it uses CSPspecific services. Containers also start much faster than a VM (seconds vs. minutes), partly because the OS doesn’t need to boot. 

## Conceptual Model 
* The following conceptual model shows some of the most important concepts described in this paper along with their relationships. It should help to clarify these relationships. When reading text along an arrow, follow the direction of the arrow. So, a DevSecOps Ecosystem contains one or more software factories, and each software factory contains one or more pipelines. The diagram also shows that each software factory contains only one CI/CD Orchestrator, and that many software factories use DCAR. 

![Conceptual Model](https://user-images.githubusercontent.com/8856857/85359791-9b92e180-b55a-11ea-9482-fd2d8db84942.jpg)

## DevSecOps Lifecycle 
* The DevSecOps software lifecycle phases are illustrated in Figure 3. There are nine phases: plan, develop, build, test, release, deliver, deploy, operate, and monitor. Security is embedded within each phase.
![Lifecycle](https://user-images.githubusercontent.com/8856857/85360008-499e8b80-b55b-11ea-82fd-8a8597f47e3c.jpg)
 The DevSecOps lifecycle is adaptable and has many feedback loops for continuous improvement.

## DevSecOps Pillars 
* DevSecOps are supported by four pillars: organization, process, technology, and governance, as illustrated in Figure 4. 
![Pillars](https://user-images.githubusercontent.com/8856857/85360142-a7cb6e80-b55b-11ea-9b9f-03c1ae8a5f72.jpg)
For each DoD organization, the practice of DevSecOps starts with buy-in of the DevSecOps philosophy by senior leaders within the organization. This leads to a change to the organizational culture, along with the development of new collaborative processes, technologies and tools to automate the process and to apply consistent governance. A project must advance in all four areas to be successful. 
### Organization 
* The organization should embrace the following philosophies and ideas and incorporate them into their daily activities and software lifecycle management processes. 
   *  Change the organizational culture to take a holistic view and share the responsibility of software development, security and operations. Train staff with DevSecOps concepts and new technologies. Gradually gain buy-in from all stakeholders. 
   * Break down organizational silos. Increase the team communication and collaboration in all phases of the software lifecycle.
   * Actionable security and quality assurance (QA) information, such as security alerts or QA reports, must be automatically available to the teams at each software lifecycle phase to make collaborative actions possible
   * Build a culture of safety by sharing after-action reports on both positive and negative events across the entire organization. Teams should use both success and failure as learning opportunities to improve the system design, harden the implementation, and enhance the incident response capability as part of the DevSecOps practice. 
   * Make many small, incremental changes instead of fewer large changes. The scope of smaller changes is more limited and thus easier to manage. 
   * Embrace feedback and user driven change to respond to new, emerging, and unforeseen requirements. 
   * Plan and budget for continuous code refactoring to ensure constant buy down of accumulated technical debt. 
 ### Process 
 * Depending on the mission environment, system complexity, system architecture, software design choices, risk tolerance level, and system maturity level, each program’s software lifecycle has its own unique management processes.  
   * For example, suppose a mature web application software system has adopted a microservices design. Its development, pre-production, and production environment are on the same cloud. The test procedures are fully automated. This system could have a process flow to automate the develop, build, test, secure, and delivery tasks to push updates into production quickly without human intervention. 
   *  On the other hand, a complex mission critical embedded system, such as a weapons system, may have a different process that requires some tests that cannot be fully automated. The software lifecycle process for that system will be significantly different from the process for the web application system. 
*  To adopt a DevSecOps process successfully, implement it in multiple, iterative phases. Start small with some tasks that are easy to automate, then gradually build up the DevSecOps capability and adjust the processes to match. Figure 5 illustrates this concept; it shows that a software system can start with a Continuous Build pipeline, which only automates the build process after the developer commits code. Over time, it can then progress to Continuous Integration, Continuous Delivery, Continuous Deployment, Continuous Operation, and finally Continuous Monitoring, to achieve the full closed loop of DevSecOps. A program could start with a suitable process and then grow progressively from there. The process improvement is frequent, and it responds to feedback to improve both the application and the process itself. 
![CI](https://user-images.githubusercontent.com/8856857/85362089-ef082e00-b560-11ea-8226-714f3717c10f.jpg)
* There is no “one size fits all” solution for process design. Each software team has its own unique requirements and constraints. Below is a list of some best practices to guide the process design: 
1. The process design is a collective effort from multidisciplinary teams. 
2. Most of the processes should be automatable via tools and technologies.  
3. The DevSecOps lifecycle is an iterative closed loop. Start small and build it up progressively to strive for continuous improvement. Set up human intervention at the control gates when necessary, depending on the maturity level of the process and the team’s confidence level in the automation. Start with more human intervention and gradually decrease it as possible. 
4. AO should consider automating the Authority to Operate (ATO) process as much as possible. 
### Technology 
* Many DevSecOps tools automate many tasks in the software lifecycle without human involvement. Other DevSecOps tools, such as collaboration and communication tools, facilitate and stimulate human interaction to improve productivity. Some DevSecOps tools aim to help an activity at a specific lifecycle phase. 
   *  For example, an Integrated Development Environment (IDE) DevSecOps plug-in for develop phase, or a static application security test tool for the build phase. Most tools assist a particular set of activities. The tags added to artifacts in the artifact repository help guarantee that the same set of artifacts move together along a pipeline. 
* Section 4 will introduce a variety of DevSecOps tools.  The instantiation of the DevSecOps environments can be orchestrated from configuration files instead of setting up one component at a time manually. The infrastructure configuration files, the DevSecOps tool configuration scripts, and the application run-time configuration scripts are referred to as Infrastructure as Code (IaC). Taking the same approach as IaC, security teams program security policies directly into configuration code, as well as implement security compliance checking and auditing as code, which are referred as Security as Code (SaC). 
* Both IaC and SaC are treated as software and go through the rigorous software development processes including design, development, version control, peer review, static analysis, and test. Technologies and tools play a key role in DevSecOps practice to shorten the software lifecycle and increase efficiency. They not only enable software production automation as part of a software factory, but also allow operations and security process orchestration. 
### Governance 
* Governance actively assesses and manages the risks associated with the mission program throughout the lifecycle. 
* Governance activities do not stop after ATO but continue throughout the software lifecycle, including operations and monitoring. DevSecOps can facilitate and automate many governance activities. 
#### Management Structure 
* The management objective of DevSecOps must be both “top-down” and “bottom-up” to balance larger strategic goals. 
   * Studies (e.g., [8]) have shown that senior leader buy-in is crucial for success. 
   * But buy-in at the staff level is also important to engender a sense of ownership, to encourage the appropriate implementation of processes related to governance, and to enable team members to support continuous process improvement. Continuous process improvement – seeking opportunities to simplify and automate whenever and wherever possible – is essential for governance to keep pace with a rapidly changing world
* Early DevSecOps efforts in the DoD, such as [9] have leveraged and adopted commercial best practices. That document identifies Five Fundamental Principles of Next Generation Governance (NGG): 
1. **Run IT with Mission Discipline:** Tie requirements back to your organization’s mission. Every action should be aligned to the mission. If they are not, then an evaluation should be performed with Continuous Process Improvement to address how to tie actions to missions. 
2. **Invest in Automation:** Automate everything possible, including actions, business processes, decisions, approvals, documentation, and more. Automation, including designs, interfaces, functional and security tests, and their related documentation, create the Artifacts of Record that provide the body of evidence required by the Risk Management Framework (RMF) and for historical audits when needed. 
3. **Embrace Adaptability:** Accept that change can be required at any time, and all options are available to achieve it. Fail fast, fail small, and fail forward. An example of failing forward is when a developer finds that a release does not work. Then instead of restoring the server to its pre-deployment state with the previous software, the developer’s change should be discrete enough that they can fix it and address the issue through a newer release. 
4. **Promote Transparency:** Offer open access across the organization to view the activities occurring within the automated process and to view the auto-generated Artifacts of Record. Transparency generates an environment for sharing ideas and developing solutions comprised of Subject Matter Experts (SMEs) or leads from across the enterprise in the form of cross-functional teams to avoid the “silo effect.” When composed of all representative stakeholders, the team possesses the skills needed to build a mission system and the collective ingenuity necessary to overcome all encountered challenges. 
5. **Inherent Accountability:** Push down or delegate responsibility to the lowest level: 
* Strategic: This is related to the Change Control Board (CCB) or Technical Review Board (TRB); it involves “Big Change” unstructured decisions. These infrequent and high-risk decisions have the potential to shape the strategy and mission of an organization. 
* Operational: (Various Scrum) Cross-cutting, semi-structured decisions. In these frequent and high-risk decisions, a series of small, interconnected decisions are made by different groups as part of a collaborative, end-to-end decision process. 
* Tactical: (Global Enterprise Partners (GEP)/Product Owner/Developers Activities) Delegated, structured decisions. These frequent and low-risk decisions are effectively handled by an individual or working team, with limited input from others. These 5 principles are summarized in Figure 6, which is from [9]. 
