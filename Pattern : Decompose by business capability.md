## Context
* The microservice architecture structures an application as a set of **loosely coupled services. 
* The goal of the microservice architecture is to accelerate software development by enabling continuous delivery/deployment.

* These benefits are not automatically guaranteed. Instead, they can only be achieved by the careful functional decomposition of the application into services.
* A service must be small enough to be developed by a small team and to be easily tested.
* A useful guideline from object-oriented design (OOD) is the Single Responsibility Principle (SRP). The SRP defines a responsibility of a class as a reason to change, and states that a class should only have one reason to change. It make sense to apply the SRP to service design as well and design services that are cohesive and implement a small set of strongly related functions.
