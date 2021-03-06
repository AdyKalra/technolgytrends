> [Preview on the web](https://nicedoc.io/AdyKalra/technolgytrends/blob/master/EngineeringPractices%20trends/DoD%20Enterprise%20DevSecOps%20Reference%20Design.md)

# DoD Enterprise DevSecOps Reference Design 
## [Executive Summary](#executive-summary) 
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
![FiveP](https://user-images.githubusercontent.com/8856857/85362715-81f59800-b562-11ea-820e-8fe6ddae5cd4.png)
#### Authorizing Official 
* For initial standup of a new DevSecOps software factory instance and a production operations environment, the RMF process follows an enterprise level process. The assessment and authorization (A&A) should inherit the certifications and authorizations of the underlying infrastructure (e.g., a DoD cloud provisional authorization) and of the DoD Enterprise Hardened Containers, without having to re-certify them. 
* The program should have a formal Service Level Agreement (SLA) with the underlying infrastructure provider about what services are included and what authorizations can be inherited. This affects the status of applicable assessment procedures and prepares the stage for inheritance into the operations environment and application. 
* Once the instance is authorized and operational, the specialty AO for the functional area or the local AO for the program has cognizance for Continuous Authorization of the environment. Figure 7 illustrates the A&A inheritance. The specialty AO for the functional area or the local AO for the program has cognizance for Continuous Authorization of the mission applications. 
![AA](https://user-images.githubusercontent.com/8856857/85363045-43141200-b563-11ea-8845-1bf24d600436.jpg)
 
## DevSecOps Ecosystem 
* The DevSecOps ecosystem is a collection of tools and the process workflows created and executed on the tools to support all the activities throughout the full DevSecOps lifecycle. As illustrated in Figure 8, the DevSecOps ecosystem is composed of three subsystems: **planning, a software factory, and production operations.** The DevSecOps ecosystem interacts with external enterprise services to get all dependency support, and with enterprise and local AO to gain operation authorization. The DevSecOps administration team is responsible for administrating the ecosystem tools and automating the process workflows. The mission application team focuses on the development, testing, security and operations tasks using the ecosystem. 
![Ecosystem](https://user-images.githubusercontent.com/8856857/85363294-df3e1900-b563-11ea-9ae8-dd06e036e988.jpg)
### Planning 
* The plan phase involves activities that help the **project manage time, cost, quality, risk and issues.** These activities include business-need assessment, project plan creation, feasibility analysis, risk analysis, business requirements gathering, business process creation, system design, DevSecOps design and ecosystem instantiation, etc. 
* The plan phase repeats when DevSecOps the lifecycle recycles. It is a best practice to develop a minimum viable product (MVP) for critical business needs as the first thing to develop. Then get into the feedback loop process as quickly as possible; this is recommended in the Lean Startup methodology [11]. 
* The DevSecOps design creates the DevSecOps processes and control gates, which will guide the automation throughout the lifecycle. DevSecOps ecosystem tools will facilitate process automation and consistent process execution. The DevSecOps planning subsystem supports the activities in the plan phase using a set of communication, collaboration, project management, and change management tools. In this phase, the process workflows are not fully automated. The planning tools assist human interaction and increase team productivity. 
### Software Factory 
* A software factory, illustrated in Figure 9, contains multiple pipelines, which are equipped with a set of tools, process workflows, scripts, and environments, to produce a set of software deployable artifacts with minimal human intervention. It automates the activities in the develop, build, test, release, and deliver phases. 
* The environments that are set up in the software factory should be orchestrated with scripts that include IaC and SaC and which run on various tools. A software factory must be designed for multi-tenancy and automate software production for multiple projects. A DoD organization may need multiple pipelines for different types of software systems, such as web applications or embedded systems. 
![Factory](https://user-images.githubusercontent.com/8856857/85363672-d6017c00-b564-11ea-939e-e84c27d13c62.jpg)
* The factory starts with the development team developing application code and IaC, QA developing test scripts, and the security team developing SaC in their suitable IDEs. The entire Software Factory should leverage OCI compliant containers and DoD Hardened Containers whenever available. 
* Once COTS, Government off the Shelf (GOTS), or newly developed code and scripts are committed into the Software Factory’s code repository, the assembly line automation kicks in. 
* There could be multiple CI pipeline instances as assembly lines. Each is for a specific application subsystem, such as a JavaScript assembly line for a web front-end, a Python or R assembly line for data analytics, or a GoLang assembly line for a backend application. * The CI assembly line guides the subsystem through continuous integration by building the code and incorporating dependencies (such as libraries) from the local artifact repository. 
* In addition, it performs tests in the development and test environments, such as unit tests, static code analysis, functional tests, interface tests, dynamic code analysis, etc. 
* The subsystems that pass CI assembly line control gate policies will move into the pre-production environment for systems integration. * The CD assembly line takes over control from this point. More tests and security scans are performed in this environment, such as performance tests, acceptance test, security compliance scan, etc. The CD assembly line releases and delivers the final product package to the released artifact repository if the control gate policies are met. 
* Developing applications using a DevSecOps software factory provides many benefits: • Improved software product consistency and quality • Shortened time to market and increased productivity • Simplified governance
### Operations 
* In the production environment, the released software is pulled from the released artifact repository and deployed. 
* Operations, operation monitoring, and security monitoring are performed. 
* Production operation tools aim to streamline and automate the deployment, operations, and monitoring activities. Tools should be selected based on system functional requirements and their suitability for the production environment infrastructure. 
#### External Systems 
* The DevSecOps ecosystem itself and program applications depend on some DoD enterprise services to acquire the necessary baseline tools, application dependencies, and security services to operate. 
* **DoD Centralized Artifact Repository (DCAR)** holds the hardened VM images and hardened OCI compliant container images of: DevSecOps tools, container security tools, and common program platform components (e.g. COTS or open source products) that DoD program software teams can utilize as a baseline to facilitate the authorization process. 
* **DoD Common Security Services** are DoD enterprise-level common services that facilitate cybersecurity enforcement and IT management. One security service will perform traffic inspection and filtering to protect the mission enclave and mission applications. Some security service examples include firewalls; Intrusion Detection System (IDS)/Intrusion Prevention System (IPS); malware detection; data loss prevention; host-based security; log/telemetry aggregation and analysis; and Identity, Credential, and Access Management (ICAM). A Cybersecurity Service Provider (CSSP) will provide additional services, including Attack Sensing and Warning (ASW), Forensic Media Analysis (FMA), Assurance Vulnerability Management (AVM), Incident Reporting (IR), Incident Handling Response (IHR), Information Operations Condition (INFOCON), Cyber Protection Condition (CPCON), Malware Notification Protection (MNP), and Network Security Monitoring (NSM).  
## DevSecOps Tools and Activities 
* This section describes both tools for the DevSecOps ecosystem and DevSecOps activities for each phase. Activities and tools are listed in table format. The Baseline column in the tool tables has two values: Minimal Viable Product (MVP) and objective. They indicate whether the tool must be available in the DevSecOps ecosystem MVP as threshold or if the tool is an objective to be reached as the ecosystem matures. Activity tables list a wide range of activities for DevSecOps practice. DoD organizations should define their own processes, choose proper activities, and then select tools suitable for their systems to build software factories and DevSecOps ecosystems. With the DevSecOps maturity progression, the level of activity automation will increase.  
### Planning Tools and Activities 
![Plan1](https://user-images.githubusercontent.com/8856857/85364803-4a3d1f00-b567-11ea-8d69-32751703a6e5.png)
![Plan2](https://user-images.githubusercontent.com/8856857/85364877-79ec2700-b567-11ea-991f-e554131065ff.png)
![Plan3](https://user-images.githubusercontent.com/8856857/85364927-9e480380-b567-11ea-8333-ef77b11ad008.png)
* The activities supported by the plan phase are listed in Table 4. Some activities are suitable at enterprise or program level, such as DevSecOps ecosystem design, project team onboarding planning, and change management planning. Others fit at the project level and are considered continuous in the DevSecOps lifecycle.
![Plan4](https://user-images.githubusercontent.com/8856857/85365087-f67f0580-b567-11ea-81a6-6ead1e2573a1.png)
![Plan5](https://user-images.githubusercontent.com/8856857/85365129-0e568980-b568-11ea-963f-c964c8774e56.png)
![Plan6](https://user-images.githubusercontent.com/8856857/85365175-25957700-b568-11ea-8ebe-18cf5a7282cf.png)
![Plan7](https://user-images.githubusercontent.com/8856857/85365243-4b228080-b568-11ea-989b-020fbeb1907b.png)
### Software Factory Tools and Activities 
* Software factory tools include a CI/CD orchestrator, a set of development tools, and a group of tools in the build, test, release, and deliver phases that are pluggable to the CI/CD orchestrator. 
#### **CI/CD Orchestrator** The CI/CD Orchestrator is the central automation engine of the CI/CD pipeline. 
* It manages pipeline creation, modification, execution, and termination. The DevSecOps team creates a pipeline workflow in the Orchestrator by specifying a set of stages, stage conditions, stage entrance and exit control rules, and stage activities. The Orchestrator automates the pipeline workflow by validating the stage control rules. If all the entrance rules of a stage are met, the Orchestrator will transition the pipeline into that stage and perform the defined activities by coordinating the tools via plugins. If all the exit rules of the current stage are met, the pipeline exits out the current stage and starts to validate the entrance rules of the next stage. 
![Orchestrator](https://user-images.githubusercontent.com/8856857/85365435-b1a79e80-b568-11ea-9715-1b31f4f61f3f.png)
#### Develop 
* The Develop phase uses tools to support the development activities that convert requirements into source code. the source code includes application code, test scripts, Infrastructure as Code, Security as Code, DevSecOps workflow scripts, etc. The development team may rely on a single modern integrated development environment (IDE) for multiple programming language support. 
* The IDE code assistance feature aids developers with code completion, semantic coloring, and library management to improve coding speed and quality. 
* The integrated compiler, interpreter, lint tools, and static code analysis plugins can catch code mistakes and suggest fixes before developers check code into the source code repository.
* Source code peer review or pair programming are other ways to ensure code quality control. All the code generated during development must be committed to the source code repository and thus version controlled. Committed code that breaks the build should be checked in on a branch and not merged into the trunk until it is fixed. 
* The following tables list the components that facilitate code development, along with their inputs and outputs. 
![Develop1](https://user-images.githubusercontent.com/8856857/85365765-588c3a80-b569-11ea-8328-57a274d48741.png)
![Develop2](https://user-images.githubusercontent.com/8856857/85365865-870a1580-b569-11ea-8f5b-a33c1d3ebac0.png)
#### Build 
* The build tools perform the tasks of building and packaging applications, services, and microservices into artifacts. For languages like C++, building starts with compiling and linking. 
   *  The former is the act of turning source code into object code and the latter is the act of combining object code with libraries to create an executable file. 
   *  For Java Virtual Machine (JVM) based languages, building starts with compiling to class files, then building a compressed file such as a jar, war or ear file, which includes some metadata, and may include other files such as icon images. 
   * For interpreted languages, such as Python or JavaScript, there is no need to compile, but lint tools help to check for some potential errors such as syntax errors. 
*  Building should also include generating documentation, such as Javadoc, copying files like libraries or icons to appropriate locations, and creating a distributable file such as a tar or zip file. The build script should also include targets for running automated unit tests. 
* Modern build tools can also be integrated into both an IDE and a source code repository to enable building both during development and after committing. 
* For those applications that use containers, the build stage also includes a containerization tool. The following tables list build-related tools along with their inputs and outputs. 
![Build1](https://user-images.githubusercontent.com/8856857/85366108-07c91180-b56a-11ea-9afc-c58467537410.png)
![Build2](https://user-images.githubusercontent.com/8856857/85366203-3941dd00-b56a-11ea-940c-81b6cc81d7c8.png)
The activities supported by the build phase are listed in Table 9. 
![Build3](https://user-images.githubusercontent.com/8856857/85366320-727a4d00-b56a-11ea-91f8-56f11cfb0ff7.png)
![Build4](https://user-images.githubusercontent.com/8856857/85366349-8756e080-b56a-11ea-96ef-6def55b58406.png)
#### Test 
* Test tools support continuous testing across the software development lifecycle. Test activities may include, but are not limited to, **unit test, functional test, integration test, system test, regression test, acceptance test, performance test,** and variety of security tests. . 
* Mission programs can select their own test activities and merge several tests together based on the nature of their software and environment. 
* All tests start with test development, which develops detailed test procedures, test scenarios, test scripts, and test data. Automated test can be executed by running a set of test scripts or running a set of test scenarios on the specific test tool without human intervention. If full automation is not possible, the highest percentage of automation is desired. 
* It is highly recommended to leverage emulation and simulation to test proper integration between components such as microservices and various sensors/systems, so integration testing can be automated as much as possible. 
* Automation will help achieve high test coverage and make continuous ATO practicable, as well as significantly increase the quality of delivered software.  
* The components involved with the test phase are listed in the following table. 
![Test1](https://user-images.githubusercontent.com/8856857/85366729-490df100-b56b-11ea-82a4-d28ed09904fd.png)
![Test2](https://user-images.githubusercontent.com/8856857/85366781-604cde80-b56b-11ea-8421-fdde5966db3e.png)
![Test3](https://user-images.githubusercontent.com/8856857/85366962-b3269600-b56b-11ea-80d6-a33d660dc753.png)
![Test4](https://user-images.githubusercontent.com/8856857/85367070-e1a47100-b56b-11ea-8d1b-8e3bb0c2a99e.png)
![Test5](https://user-images.githubusercontent.com/8856857/85367129-026cc680-b56c-11ea-93e2-ff47e5f2ca6d.png)
* The activities supported by the test phase are listed in Table 11. These activities happen at different test stages. 
   * Development stage: unit test, SAST discussed in the build phase 
   *  System test stage: DAST or IAST, integration test, system test 
   *  Pre-production stage: manual security test, performance test, regression test, acceptance test, container policy enforcement, and compliance scan Test audit, test deployment, and configuration audit happen at all stages. 
![Test6](https://user-images.githubusercontent.com/8856857/85367309-5c6d8c00-b56c-11ea-9ef2-0e89941e3ed0.png)
![Test7](https://user-images.githubusercontent.com/8856857/85367394-7d35e180-b56c-11ea-98fb-34e3db195528.png)
![Test8](https://user-images.githubusercontent.com/8856857/85367432-8fb01b00-b56c-11ea-9037-0bb1f4fcf98d.png)
![Test9](https://user-images.githubusercontent.com/8856857/85367484-afdfda00-b56c-11ea-98a8-c76b24e47553.png)
#### Release and Deliver 
* In the release and deliver phase, the software artifacts are digitally signed to verify that they have passed build, all tests, and security scans. They are then delivered to the artifact repository. The content of the artifacts depends on the application. It may include, but is not limited to, container images, VM images, binary executables (such as jar, war, ear files), test results, security scan results, and Infrastructure as Code deployment scripts. 
* Artifacts will be tagged with the release tag if GO release decision is made based on the configuration audit results. The artifacts with the release tag are delivered to production.  
![Rel1](https://user-images.githubusercontent.com/8856857/85367658-064d1880-b56d-11ea-9e27-e0ec5e95ee2c.png)
* The mission program could have more than one artifact repository, though more likely there is a centralized one and tags separate artifact types. 
   *  One artifact repository (or set of tags) is used in the build stage to store build results. 
   *  The test deployment activity can fetch the artifacts from the build stage artifact repository to deploy the application into various environments (development, test, or pre-production). 
   *  Another artifact repository (or set of tags) may be used by the production environment, which is the one that the store artifacts stage uses to push the final deliverables to production. 
   *  The production deployment will get all the artifacts from the production artifact repository to deploy the application.  
*  Some mission program application systems have geographically distributed operational regions across the country or even overseas. In order to increase deployment velocity, a remote operational region may have its own local artifact repository that replicates the artifact repository completely or partially. During release, a new artifact is pushed into the artifact repository and then replicated to other regional artifact repositories.
* The activities supported by the release and deliver phase are listed below. 
![Rel2](https://user-images.githubusercontent.com/8856857/85368210-2f21dd80-b56e-11ea-987a-142f911be169.png)
### Production Operation Tools and Activities 
* The production operations tools provide the capability to deploy artifacts, including containers and VM images, to the production environment, and to monitor their operations. For Cloudnative applications, it is recommended to use containers whenever possible over virtual machines due to the baked-in security provided by the Sidecar Container Security Stack. 
#### Deploy 
* The tools used in deploy phase are environment and deployment mode dependent. 
   *  **Virtual Machine deployment**
   *  While it is highly recommended to leverage containers for new system design and development, if the application is deployed as a VM, the virtualization manager in the hosting environment is the key component with which IaC will interface to deploy and configure the application system. 
   * The virtualization manager manages the virtual compute, storage and network resources. 
   * In some hosting environments, such as a general-purpose cloud, the virtualization manager also provides some security capabilities, such as microsegmentation, which creates security zones to isolate VMs from one another and secure them individually. 
  * **Container deployment**
   *  A container manager provides capabilities that check for new versions of containers, deploys the containers to the production environment, and performs post-deployment checkout. 
   * The container manager consists of an OCI-compliant container runtime and a CNCF-certified Kubernetes, which is an orchestration tool for managing microservices or containerized applications across a cluster of nodes. 
   * The nodes could be bare metal servers or VMs. The container manager may be owned by a mission program or provided by the cloud hosting environment. It simplifies container management tasks, such as **instantiation, configuration, scaling, monitoring, and rolling updates.** 
   * The CNCF-certified Kubernetes interacts with the underlying virtualization manager in the cloud environment to ensure each node’s health and performance, and scale it as needed. This scaling includes container scaling within the CNCF-certified Kubernetes cluster, but when running in a cloud, it also includes the ability to auto-scale number of nodes in a cluster by adding or deleting VMs.  
* The following tables list deployment-related tools and their inputs and outputs. 
![Deploy1](https://user-images.githubusercontent.com/8856857/85501613-14f90580-b629-11ea-8b10-9fed8eed59c6.png)
![Deploy2](https://user-images.githubusercontent.com/8856857/85501692-3823b500-b629-11ea-988a-d70e35b97a75.png)
![Deploy3](https://user-images.githubusercontent.com/8856857/85501769-58537400-b629-11ea-98b1-1160fde13192.png)
![Deploy4](https://user-images.githubusercontent.com/8856857/85501889-981a5b80-b629-11ea-870b-6b79eb354fa1.png)

#### Operate 
* The Operate phase uses tools for system **scaling, load balancing, and backup.**  
   * Load balancing monitors resource consumption and demand, and then distributes the workloads across the system resources. 
   * Scaling helps dynamic resource allocation based on demand. Both virtualization manager and CNCF-certified Kubernetes support load balancing and scaling capabilities. CNCF-certified Kubernetes handles the load balancing and scaling at the container level. The virtualization manager works at the VM level. Application deployment must have proper load balancing and scaling policies configured with the virtualization manager or the CNCF-certified Kubernetes based on VM deployment or container deployment respectively. During runtime, the management layer will continuously monitor the resources. If the configured threshold is met (for example if memory or Central Processing Unit (CPU) usage meets a pre-set threshold), then the system triggers the load balancing or scaling action automatically. **Auto-scaling must be able to scale both up and down.**
![Operate1](https://user-images.githubusercontent.com/8856857/85502670-29d69880-b62b-11ea-8587-3584b54853c7.png)
![Operate2](https://user-images.githubusercontent.com/8856857/85502740-4b378480-b62b-11ea-88da-1fcf3fc8f738.png)
      
#### Monitor 
* In the monitor phase, tools are utilized to collect and assess key information about the use of the application to discover trends and identify problem areas. 
* Monitoring **spans the underlying hardware resources, network transport, applications / microservices, containers, interfaces, normal and anomalous endpoint behavior, and security event log analysis.** It also includes behavior and signature-based detection in the runtime environment. All these security capabilities are mapped against the NIST controls and follow NIST Special Publication 800-190 Application Container Security Guide [12] for continuous compliance. 
![Monitor1](https://user-images.githubusercontent.com/8856857/85502935-d153cb00-b62b-11ea-9d32-ccf69bc0566a.png)
![Monitor2](https://user-images.githubusercontent.com/8856857/85502991-ef213000-b62b-11ea-91fa-71fd695ccfe9.png)
![Monitor3](https://user-images.githubusercontent.com/8856857/85503039-09f3a480-b62c-11ea-95c1-371a355152aa.png)
![Monitor4](https://user-images.githubusercontent.com/8856857/85503094-2abbfa00-b62c-11ea-82b7-e7a79997b32d.png)
![Monitor5](https://user-images.githubusercontent.com/8856857/85503147-49ba8c00-b62c-11ea-93b0-ec5adb956006.png)

### Security Tools and Activities Summary 
* Security is not a separate phase of the DevSecOps lifecycle; rather security activities occur in all phases. This DevSecOps security practice facilitates automated risk characterization, monitoring, and mitigation across the application lifecycle. Table 20 summarizes the security activities of all phases.
![Security1](https://user-images.githubusercontent.com/8856857/85503307-afa71380-b62c-11ea-9580-5f0bb858a1ea.png)
![Security2](https://user-images.githubusercontent.com/8856857/85503346-cbaab500-b62c-11ea-8a3d-4467e5e5f5a9.png)

###  Configuration Management Tools and Activities Summary 
* Configuration management plays a key role in DevSecOps practice. It ensures the configuration of a software system’s infrastructure, software components, and functionalities are not only known initially but also knowable and well controlled throughout the DevSecOps lifecycle.  
* Configuration management consists of three sets of activities:  
   *  **Configuration identification:** identify the configuration items. This can be done manually or with assistance from a discovery tool. The configuration items include infrastructure components, COTS or open source software components used in the system, documented software design, features, software code or scripts, artifacts, etc. 
   *  **Configuration control:** control the changes of the configuration items. Each configuration item has its own attributes, such as model number, version, configuration setup, license, etc. The CMDB, source code repository, and artifact repository are tools to track and control the changes. The source code repository is used primarily during development. The other two are used in both development and operations. 
   * **Configuration verification and audit:** verify that the configuration items meet the documented requirements and design. Configuration verification and audit are control gates along a pipeline to control the go/no-go decision to the next phase.
![Config1](https://user-images.githubusercontent.com/8856857/85503536-41168580-b62d-11ea-9d0f-f818fed72293.png)
![Config2](https://user-images.githubusercontent.com/8856857/85503586-5db2bd80-b62d-11ea-86ca-ed890ecc77e1.png)

### Database Management Tools and Activities Summary 
* Databases are commonly used in the DoD software systems. They hold some of the most critical information of an enterprise or a mission and are typically the center piece of the software system. 
* Data security and privacy protection are paramount to enterprises and missions. 
* Relational databases continue to be a prime target for data thieves, and security vulnerabilities are compound by adoption of big data platforms, such as Hadoop, NoSQL databases, and Database as a Service (DBaaS) in the cloud. 
* Here we discuss some database activities throughout the DevSecOps lifecycle to improve database security and operations. In development phases, database design, development, and testing activities generate database artifacts, which are data models, database schema files, trigger definitions, view definition, test data, test data generation scripts, test scripts, etc. 
* These database artifacts must be under configuration management control. During test phase, database functional test is like application code unit test and functional test to validate the schema, triggers, and data compliance. The nonfunctional test includes load testing, stress test, and performance test. The security test focuses on vulnerability scan, user authentication and authorization, unauthorized access to data, data encryption, privilege elevation, SQL injection, and denial of service. 
* During operations, the deployment and operational activities can be automated via database automation tools. The continuous monitoring is achieved using database monitoring tool and security audit tool. 
![DB1](https://user-images.githubusercontent.com/8856857/86082096-52064180-bada-11ea-9ca6-1863be61ca4c.png)

## DoD Enterprise DevSecOps Container Service
* The DoD Enterprise DevSecOps Container Service creates DevSecOps hardened containers and provides hardened container access service to DoD programs to instantiate their own DevSecOps ecosystem. 
![DevSecOps Container Service](https://user-images.githubusercontent.com/8856857/86082240-998ccd80-bada-11ea-8871-4c365a9bcb3d.png)
* Figure 10 illustrates the DoD Enterprise DevSecOps Container Service architecture. It contains a DoD Enterprise DevSecOps Container Factory and a DoD Centralized Artifact Repository (DCAR). The Container Factory takes public container images as input and automates the container hardening process to produce the hardened container images. The DCAR stores the hardened container images and allows DoD programs access these images
### DoD Enterprise DevSecOps Container Factory 
* The Container Factory produces the hardened containers of DevSecOps tools. It is imperative for the Container Factory to automate its hardening process as much as possible. It does this by leveraging CI/CD pipelines in an instance of the software factory specifically configured for hardening of DevSecOps tool containers. 
#### DoD Hardened Containers 
* A DoD hardened container is an Open Container Image (OCI) compliant image that is secured and made compliant with the DoD Container Hardening Security Requirements Guide [6].
* Container images should adhere to the OCI Image Format Specification to ensure portability. Each hardened container includes the “global configuration”, which includes all security hardening configuration. 
* The packaged container is tagged with integrity metadata, such as a digital signature or a digital hash. Tags may be implemented as metadata bound to the object, or as attributes in a file associated with the object. 
* Some configuration values can be changed for local use, such as the DNS location. These “local configuration” values are outside the scope of the integrity tag, and do not “break” the chain of trust for the hardened container.  Artifacts related to the hardened container should include the Information Assurance (IA) controls that the hardened container has successfully addressed, so that users of the container know which controls they can inherit, versus which controls they must address. This capability may not exist in the MVP, but it is an objective that enables reciprocity. 
* The Hardened Container Factory produces following types of containers: 
   * Hardened containers of DevSecOps CI/CD pipeline tools  
   * Sidecar Container Security Stack containers to be used in runtime environments for container security 
   * Common containers (such as OS, database, web servers, etc.) to be used as a program development baseline 
#### Container Hardening Process 
* The Container hardening process, including required documentation, sustainment of the hardened containers, and cybersecurity requirements, is fully described in the DoD Enterprise DevSecOps Initiative Hardening Containers [13]. The basic process is depicted in Figure 11. 
![Hardening](https://user-images.githubusercontent.com/8856857/86082544-60a12880-badb-11ea-9621-65df5c48c0b5.png)
#### Select the Container Base Image
* A base image is a container image that comes from a vendor or an open source community; it is used as the starting point to create a hardened container image. Use the base image without creating forks to enable direct coupling with its updates. The container should be built starting with the respective DoD hardened base OS STIG image.  
#### Harden the Container 
* The Container Factory uses a set of instructions given in [13] to harden the container to mitigate findings and ensure proper DoD compliance. Reuse the instructions as much as possible between versions so that the hardening will be consistent across versions. 
* It is possible that new versions bring new features, which may require additional hardening. The DoD Centralized Container Source Code Repository (DCCSCR) is used to store instruction files to build container images, associated checksums, and various documentation. The source code repository is centrally hosted so hardeners can store their code and leverage a CI/CD pipeline (Container Factory). 
* This is what feeds the container hardening process and DCAR repository. Use the CI/CD orchestration tool; download the DCCSCR folder content into the pipeline and use the Instructions file to build the container. The CI/CD pipeline will then run the required Container Hardening Scanners, scanning the container image. Based on the findings of the Container Hardening Scanners, add instructions to mitigate the findings as needed. Rebuild and rescan until findings are mitigated or accepted. 
#### Store the Hardened Container 
* The DCAR is used to store the hardened containers, associated checksums, and various documentation. This repository will be centrally hosted. Each container will have its own folder in the DCAR. Subfolders should be used for versioning. 
* Store the hardened container and checksum inside the DCAR. It will be tagged as “preproduction” as well until the artifact receives an ATO, in which case it will then be tagged for “production”. 
#### Documentation 
* Content and documentation provided for the hardened container will include: 
   * A description of the container, how to deploy it, the functional capabilities it provides, and its interfaces. 
   * Scripts, including the instructions file for building the container, and related configuration files for deploying and scaling the hardened image or container 
   * Security test results including findings, false positives, and a recommended mitigation plan. 
   * Accepted risks, including a Plan of Action and Milestones (POA&M) for critical and high findings that are not yet resolved. 
   * Change log of significant changes since the last version. 
   * Human-readable licenses for all products are included within the container. COTS license keys will not be included, and they will need to be acquired separately.
   
#### Continuous Engineering 
* The hardened container factory CI/CD pipeline searches for and downloads new base images that are posted by the vendor or in an open source community repository and runs the steps 
* These steps are triggered automatically, as soon as a new image is released into the open source repository. If the build passes all scans, it should automatically store the new container into DCAR, where it will be tagged as “pre-production”. It also automatically notifies the team if a build fails to pass any of the scans.
#### Cybersecurity 
* The hardened containers produced by the factory should meet the related cybersecurity requirements, which include NIST Special Publication (SP) 800-53 [14], NIST SP 800-37 [15], the DoD DISA Security Technical Implementation Guides (STIGs) and Security Requirements Guides (SRGs), and industry best practices. 

### DoD Centralized Artifact Repository 
* The DCAR holds the DoD hardened container images that the DoD Enterprise DevSecOps Container Factory produces. DoD program DevSecOps teams can utilize these to instantiate their own DevSecOps ecosystem and software factory. The DCAR also holds the DoD hardened containers for base operating systems, web servers, application servers, databases, API gateways, message buses, and additional enterprise capabilities for use by DoD program software teams as a program system deployment baseline. Separate hardened container images are created for different versions of base images. 
* DCAR hardened container images are version controlled. These hardened containers, along with security accreditation reciprocity, greatly simplify and speed the process of obtaining an Approval to Connect (ATC) or Authority to Operate (ATO). The DCAR provides the capability to allow DoD programs (including approved DoD contractors) to search, list information about, and download artifacts from the repository for DoD software development on the approved environment.

## DevSecOps Ecosystem Reference Designs 
* This section will discuss two software factory reference designs. 
   * One is based on the DoD Enterprise DevSecOps Container Service offering to create a software factory using DevSecOps tool hardened containers from DCAR. 
   * The other is based on DoD authorized cloud DevSecOps service offerings as provided by a CSP. 
* This section also discusses secure operations for containerized applications in a production environment by leveraging container security tools in the DCAR. 

### Containerized Software Factory 
* A containerized software factory can be instantiated using a set of DevSecOps hardened containers that are offered in the DCAR. These enterprise containers are preconfigured and secured to reduce the certification and accreditation burden and are often available as a predetermined pattern or pipeline that will need limited or no configuration. 
* Figure 12 illustrates a containerized software factory reference design. The software factory is built on an underlying container orchestration layer and a host environment. It produces DoD applications as the product. These applications use different sets of hardened containers from the DCAR than the ones used to create the software factory. DoD programs may have already implemented a DevSecOps platform. One of the pain points is sustaining that platform. It is highly recommended that, as incremental updates are made to the existing platform, the program migrates capabilities to the DoD Enterprise DevSecOps hardened containers. For those cases where a DoD Enterprise hardened container is not available, or requires a custom policy, the program in conjunction with the DoD Enterprise DevSecOps program office is encouraged to create, sustain, and deliver the hardened container to the DCAR. 
![RefDesign](https://user-images.githubusercontent.com/8856857/86083146-d0fc7980-badc-11ea-830d-77c54927c79e.png)

### Hosting Environment 
* The reference design does not restrict the software factory hosting environment, which could be DoD-approved Cloud Service Providers, DoD data centers or even on-premises servers. The hosting environment provides compute, storage, and network resources in either physical or virtual form. 
### Container Orchestration 
* In order to support containerized software factory tools, the underlying container orchestration must use CNCF certified Kubernetes and support OCI compliant containers. CNCF-certified Kubernetes orchestrates containers, interacts with underlying hosting environment resources, and coordinates clusters of nodes at scale in development, testing and pre-production in an efficient manner. There are two options for the container orchestration layer as illustrated in Figure 13. 
![PlatformOptions](https://user-images.githubusercontent.com/8856857/86083273-1f117d00-badd-11ea-8180-81e2f61b4ad8.png)
* In Option A, it is the mission program’s responsibility to build and maintain the container orchestration layer (CNCF-certified Kubernetes) using COTS solutions. The container orchestration layer can be deployed on top of a DoD authorized cloud environment, a DoD data center, or on bare metal servers. The container orchestration system components are subject to monitoring and security control under the DoD policy in that hosting environment, such as the DoD Cloud Computing Security Requirements Guide (SRG) [2] and DISA’s Secure Cloud Computing Architecture (SCCA) [3] for the cloud environment. 
* In Option B, the mission program uses a CSP container service, which must have a DoD provisional authorization and must be based on CNCF-certified Kubernetes. 
### Software Factory Using Hardened Containers
The software factory leverages technologies and tools to automate the CI/CD pipeline processes defined in the DevSecOps lifecycle plan phase. There are no “one size fits all” or hard rules about what CI/CD processes should look like and what tools must be used. Each software team needs to embrace the DevSecOps culture and define its processes that suit its software system architectural choices. The tool chain selection is specific to the software programming language choices, application type, tasks in each software lifecycle phase, and the system deployment platform. Software factory building itself follows the DevSecOps philosophy and goes through its own design, instantiate, verify, operate and monitor phases. It evolves through the application lifecycle iteration. Figure 14 illustrates the software factory phases, activities, and the relationship with the application lifecycle. Security must be applied across the software factory phases. Sidecar Container Security Stack (SCSS) discussed in 6.4.4 can be used for software factory runtime cybersecurity monitoring. 
 
![Software Factory Phases](https://user-images.githubusercontent.com/8856857/86083363-5da73780-badd-11ea-81fe-4d15b688dc68.png)
* Figure 12 is a software factory reference design. It includes the tools and process workflows to develop, build, test, secure, release, and deliver software application for production deployment. All the tools are based on the DoD enterprise DevSecOps hardened containers. Committing code into the code repository kicks off the automated factory CI/CD pipeline workflow. The CI/CD orchestrator executes the workflow by coordinating different tools to perform various tasks. Some tasks are completed by a set of DevSecOps tools, such as build, static code analysis, unit test, publish artifacts, build container image, etc. Other tasks may need assistance from underlying container orchestration layer, such as deploy application to test, pre-production, and final production environments. Some test and security tasks may need human involvement.

### DoD Applications 
* The term “DoD Application” refers to a DoD software program hosted by an information system [16], which spreads widely from legacy monolithic infrastructure-dependent applications to modern modular infrastructure-agnostic applications. Most systems are in brownfield with legacy applications or mixed legacy and modern applications. Programs should consider the nature of their application and the deployment environment when designing their software factory.
* It is recommended to leverage the Strangler Pattern [17] [18] to refactor legacy applications to modern microservices/containerized applications. 
   * DoD application environments at all phases (development, test, pre-production, production) are subject to security control from DoD common security services.  
   * While refactoring legacy code or writing new code, it is highly recommended to leverage the DoD hardened containers or hardening scripts to facilitate the application’s ATO. 

## Software Factory using Cloud DevSecOps Services  
* The DoD authorized cloud may already or will soon offer DevSecOps services, such as code repository, artifact repository, build service, code deploy service, etc. Programs should consider using these native managed services as alternatives to self-built and self-maintained DevSecOps tool sets, but they should understand that using them may lead to vendor lock-in with the CSP. The CSP is responsible for maintaining the service offering and the DoD Provisional Authorization (PA) for each service. The program still needs to follow the software factory lifecycle and performs the design, DevSecOps service selection instead of tool selection, CI/CD pipeline process workflow automation, verify the workflows, operates and monitors the workflows.  
* Another consideration is that the CSP may not offer a full solution set. For the capability that a DevSecOps service with a DoD PA is not available, the corresponding DoD Enterprise hardened container that provides the proper capability should be used. A CNCF-certified Kubernetes container orchestration service is required for container runtime. Figure 15: Software Factory illustrates a software factory using both cloud DevSecOps services and self-maintained security tools. 
![Software Factory using Cloud DevSecOps Services](https://user-images.githubusercontent.com/8856857/86083478-b5de3980-badd-11ea-8569-f05d3e607255.png)

## Serverless Support 
* So-called “serverless computing” is becoming more popular in the DoD, and it is being used extensively in industry. This is a kind of Platform as a Service (PaaS) that is sometimes called Function as a Service (FaaS). Despite the “serverless” moniker, a FaaS still needs servers, but developers don’t have to worry about the servers, but rather how to deploy the code to them, how to set up autoscaling, and other deployment tasks. This frees the developers to focus on the code. 
* Figure 16 illustrates that a FaaS can reduce development complexity and increase efficiency over an Infrastructure as a Service (IaaS), a Containers as a Service (CaaS), or some Platform as a Service (PaaS) offerings. Although a Software as a Service (SaaS) offering is even more efficient, and good to use when it meets requirements, a SaaS is typically focused on only a few capabilities, and cannot provide the flexibility the DoD needs to develop custom applications. A good FaaS, on the other hand, does provide that flexibility, although some applications will need the even greater flexibility of an IaaS. 
![Operational Efficiency](https://user-images.githubusercontent.com/8856857/86083553-f047d680-badd-11ea-9285-ee50f8f29011.png)

* The FaaS concept has made its way into the Kubernetes environment. The basic concept is to hand the FaaS some code, then the FaaS will build an image from the code and start it running on Kubernetes. The FaaS must have these features: 
1) Build – builds containers from source code 
   a) Uses container images as the deployment unit 
   b) Given source code, build the code and create a container to house it 
2) Serving – runs the containers created by Build and automatically scales them up or down as necessary 
   a) Uses CNCF Kubernetes as the underlying container orchestration layer 
   b) Auto-scale up (given that the code is written to allow this) 
   c) Auto-scale down all the way to zero 
   d) Gradual rollouts of new versions 
   e) Network routing within the cluster, and ingress connections into the cluster 
3) Eventing – allows functions/applications to publish and subscribe to event streams, to enable loosely-coupled, event-driven systems 
   a) Universal subscription, delivery, and management of events 
   b) Bind events to functions or containers 
   c) Trigger functions when called via and Hypertext Transfer Protocol (HTTP) requests 
   d) Automatically scale from a few events per day to live streams 
One popular open source product that implements FaaS for Kubernetes is Knative. Another open source product is Kubeless. The DevSecOps Software Factories must offer Knative support. They may also support Kubeless or another FaaS for Kubernetes

## Application Security Operations 
* This section focuses on the software application lifecycle in the production environment. Continuous Deployment, Continuous Operation, and Continuous Monitoring are keys to streamlined and secure operations. 

### Continuous Deployment 
* Continuous deployment is triggered by the successful delivery of released artifacts to the artifact repository and may be subject to control with human intervention according to the nature of the program application. 
* The typical activities for continuous deployment include, but are not limited to, 
   * deploying a new software release to the production environment, 
   * applying necessary infrastructure and security configuration changes, 
   * running a smoke test to make sure essential functionality is working, 
   * and performing security scans. 
* Each activity is completed by specific tools or configuration/orchestration scripts. The selection of tools and the configuration/orchestration system depends on the application and the production platform. 
   * For example, if the application is containerized and the production platform uses Kubernetes, the orchestration is done by Kubernetes. In this case, the configuration scripts would be Kubernetes Operators or Helm charts. 
   * On the other hand, if the application is VM based, the configuration/orchestration tool could be Chef, Puppet or Ansible. Continuous deployment interacts with other DevSecOps components, such as the artifact repository for retrieving new releases, the log storage and retrieval service for logging deployment events, and the issue tracking system for recording any deployment issues. 
* The firsttime deployment may involve heavy infrastructure provisioning, dependency system configuration (such as monitoring tools, logging tools, scanning tools, backup tools, etc.), and external system connectivity (such as DoD common security services, etc.).
### Continuous Operation 
* Continuous operation is an extension of continuous deployment. It is triggered by a successful deployment to the production environment, so that it operates the latest stable software release. 
* The activities of continuous operation include, but are not limited to, 
   * system patching, 
   * compliance scanning, 
   * data backup, 
   * system recovery if failure happens, 
   * and resource optimization with load balancing and scaling. 
* The selection of the tools that facilitate the activities are application and environment dependent. The resource optimization heavily depends on the underlying platform. A containerized application can rely on Kubernetes to automatically scale containers across cluster nodes. On the other hand, a VM-based application with no containers can rely on the underlying CSP’s scaling service. 
* Continuous operation interacts with the logging system, issue tracking system, and the underlying infrastructure platform. 
### Continuous Monitoring 
* Continuous monitoring is an extension to continuous operation. 
* It continuously inventories all system components, monitors the performance and security of all components, and logs application and system events. 
* Earlier fig illustrates the components for monitoring a containerized application deployed on Kubernetes. Figure 17 illustrates a simplified sample process of monitoring, logging, and log analysis and alerting, which also applies to deployments to non-containerized environments. 
   * The process starts with application logging, compute resource monitoring, storage monitoring, network monitoring, security monitoring, and data monitoring at the Kubernetes pod level in the case of containerized deployment or individual subsystem level in the case of VM deployment. 
   *  Each application will need to determine how it is divided into subsystems, the number of subsystems, and the specific monitoring mechanisms within the subsystems. The security tools within each subsystem (e.g., the Sidecar Container Security Stack) will aggregate and forward the event logs gathered from monitoring to a locally centralized aggregated logs database on the mission program platform. This should be automated within the Kubernetes cluster. 
   * The aggregated logs will be further forwarded to the Logs/Telemetry Analysis in the DoD Common Security Services after passing the program application configured log filter. The program’s local log analysis capability will analyze the aggregated logs and generate incident alerts and reports. Incidents will be forwarded to the mission program incident management system to facilitate change request generation for incident resolution. The mission program incident management should alert or notify the responsible personnel about the incidents. The change request may be created to address the incident. These actions make the DevSecOps pipeline a full closed loop from secure operations back to planning. 
![Logging](https://user-images.githubusercontent.com/8856857/86084082-479a7680-badf-11ea-80fd-161e8aadd3d6.png)

### Sidecar Container Security Stack 
* A new service that is enabled by DevSecOps and the container-based Kubernetes runtime environment is the Sidecar Container Security Stack (SCSS). This security stack enables: correlated and centralized logs, container security, east/west traffic management, a zero-trust model, a whitelist, Role-Based Access Control (RBAC), continuous monitoring, signature-based continuous scanning using Common Vulnerabilities and Exposures (CVEs), runtime behavior analysis, and container policy enforcement. 
* One advantage of using the SCSS is that Kubernetes can inject the sidecar automatically, without the team having to do anything, once it’s configured. 
* The sidecar pattern is depicted in Figure 18. A container group or pod is a set of containers that are deployed together. 
* **A sidecar is a container running inside a pod alongside an application container. If there is one application container and one sidecar container in the container group, then we have the sidecar pattern as depicted in Figure 18.** 
![SideCar](https://user-images.githubusercontent.com/8856857/86084200-92b48980-badf-11ea-8162-a2e29fa11017.png)
* The sidecar can share state with the application container. In particular, the two containers can share disk and network resources while their running components are isolated from one another. 
* A sidecar is a general container pattern. The Sidecar Container Security Stack has a sidecar container that contains a security stack, along with some supporting services that run in the hosting environment, such as a logging service. 
* The security stack in the security sidecar container will include: 
   1. A logging agent to push logs to a platform centralized logging service. 
   2. Container policy enforcement. This includes ensuring container hardening from DCAR containers are preserved and complies with the NIST 800-190 requirements [12]. 
   3. Runtime Defense, this can perform both signature-based and behavior-based detection. This can also be used to send notifications when there is anomalous behavior. 
   4. Vulnerability Management 
   5. A service mesh proxy to connect to the service mesh 
   6. Zero Trust down to the container level. Zero trust requires strict controls, never trust anything by default and always verify. Key aspects of zero trust at the container level include mutual Transport Layer Security authentication (mTLS), an encrypted communication tunnel between containers, strong identities per Pod using certificates, and whitelisting rather than blacklisting. 
* In addition to the components in the sidecar, there are a few services that support the security sidecar. These include: 
   1. Program-specific Log Storage and Retrieval Service 
   2. Service Mesh 
   3. Program-specific artifact repository
   4. Runtime Behavior Analysis Artificial Intelligence (AI) service
   5. DCAR for the hardened containers 
   6. Common Vulnerabilities and Exposures (CVE)Service / host-based security to provide CVEs for the security sidecar container 
* The interaction of these services with the sidecar components is depicted in Figure 19. The arrows show the direction of the data flow. The items in purple are services provided by the DoD, while blue indicates components that are provided by the DoD but instantiated and operated by the program.
![SideCarComponents](https://user-images.githubusercontent.com/8856857/86084336-f474f380-badf-11ea-950c-2924e3633401.png)

![SC1](https://user-images.githubusercontent.com/8856857/86084388-21290b00-bae0-11ea-8f4c-06ffba17c3dc.png)
![SC2](https://user-images.githubusercontent.com/8856857/86084427-3c941600-bae0-11ea-9b48-f48cbf15edc0.png)

* Figure 20 depicts another view of the sidecar, along with some of the other DevSecOps components. Again, the arrows show the direction of the data flow, and not all interactions between the depicted components are indicated. The program dashboard displays information about the application. The dashboard is built partly using visualizations from the log visualization service. The items in purple and blue are either services or components that are provide by the DoD. But those in blue will be stood up by the program. For example, the Service Mesh is provided as a hardened container. Similarly, the Sidecar Container Security Stack is provided as a hardened container that the program installs in each pod (container group); this is injected by Kubernetes automatically without application developer involvement. 

![SC SecurityStack](https://user-images.githubusercontent.com/8856857/86084512-72d19580-bae0-11ea-8dc0-5c579a6c0f37.png)
