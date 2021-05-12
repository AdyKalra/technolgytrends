# API expand-contract 

* The API expand-contract pattern, sometimes called **parallel change**, will be familiar to many, especially when used with databases or code; however, we only see low levels of adoption with APIs. 
* Specifically, we're seeing complex versioning schemes and breaking changes used in scenarios where a simple expand and then contract would suffice. 
  * For example, first adding to an API while deprecating an existing element, and then only later removing the deprecated elements once consumers are switched to the newer schema. This approach does require some coordination and visibility of the API consumers, perhaps through a technique such as **consumer-driven contract testing.**

More : https://www.martinfowler.com/bliki/ParallelChange.html
