## Service mesh

```Service mesh is an approach to operating a secure, fast and reliable``` **microservices ecosystem** ``` It has been an important stepping stone in making it easier to adopt microservices at scale.```

It offers **discovery, security, tracing, monitoring and failure handling.** It provides these cross-functional capabilities without the need for a shared asset such as an API gateway or baking libraries into each service. 

A typical implementation involves lightweight [reverse-proxy](https://hub.packtpub.com/6-common-use-cases-of-reverse-proxy-scenarios/) processes, aka``` **sidecars** ```, deployed alongside each service process in a separate container. Sidecars intercept the inbound and outbound traffic of each service and provide cross-functional capabilities mentioned above. 

This approach has relieved the distributed service teams from building and updating the capabilities that the mesh offers as code in their services. This has lead to an even easier adoption of polyglot programming in a microservices ecosystem. Our teams have been successfully using this approach with open source projects such as [Istio](https://www.thoughtworks.com/radar/platforms/istio) and we will continue to monitor other open service mesh implementations such as [Linkerd](https://linkerd.io/) closely.
