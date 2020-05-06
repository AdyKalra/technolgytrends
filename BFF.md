* The **Backend for Frontend design pattern**, as described by Phil Calçado, refers to the concept of developing niche backends for each user experience. A Backend for Frontend is a unique type of shim that fills a design gap that is inherent in the API process
* The Backend for Frontend (BFF) architecture is a type of pattern built with microservices. The key component of this pattern is an application that connects the front-end of your application with the backend. 
* While an API Gateway is a single point of entry into the system for all clients, a BFF is only responsible for a single type of client. Let’s assume your system has two (typical) clients: a Single Page Application (SPA) and a mobile client (Android, iOS). In this case each client would get its own API Gateway, which would therefore be a BFF.
* [microservices.io](https://microservices.io/patterns/apigateway.html)
![BFF](https://www.devdelly.com/static/159dc09fc4961aa2333ebbdb29c4933e/fef0a/BFF.png)
