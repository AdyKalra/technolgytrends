## Context
* The microservice architecture structures an application as a set of **loosely coupled services. 
* The goal of the microservice architecture is to accelerate software development by enabling continuous delivery/deployment.

* These benefits are not automatically guaranteed. Instead, they can only be achieved by the careful functional decomposition of the application into services.
* A service must be small enough to be developed by a small team and to be easily tested.
* A useful guideline from object-oriented design (OOD) is the **Single Responsibility Principle (SRP)**. The SRP defines a responsibility of a class as a reason to change, and states that a class should only have one reason to change. It make sense to apply the SRP to service design as well and design services that are cohesive and implement a small set of strongly related functions.

### Why?
* The architecture must be stable
* Services must be **cohesive. A service should implement a small set of strongly related functions.
* Services must conform to the **Common Closure Principle - things that change together should be packaged together** - to ensure that each change affect only one service
* Services must be **loosely coupled - each service as an API that encapsulates its implementation. The implementation can be changed without affecting clients
* A service should be testable
* Each service be small enough to be developed by a “two pizza” team, i.e. a team of 6-10 people
* Each team that owns one or more services must be autonomous. A team must be able to develop and deploy their services with minimal collaboration with other teams.

# Decompose by business capability
**Define services corresponding to business capabilities. A business capability is a concept from business architecture modeling. It is something that a business does in order to generate value.**
