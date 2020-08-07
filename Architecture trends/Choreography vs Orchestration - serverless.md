## Choreography vs Orchestration in the land of serverless

* Choreography and Orchestration are two modes of interaction in a microservices architecture.

### Orchestration
* In orchestration, there is a controller (the ‘orchestrator’) that controls the interaction between services. It dictates the control flow of the business logic and is responsible for making sure that everything happens on cue. This follows the request-response paradigm.

### Choreography
* In choreography, every service works independently. There are no hard dependencies between them, and they are loosely coupled only through shared events. Each service listens for events that it’s interested in and does its own thing. This follows the event-driven paradigm.
