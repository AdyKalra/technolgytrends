# Introducing and Scaling a GraphQL BFF

## Summary
* Journey of introducing and then scaling a GraphQL BFF to serve multiple applications. 
* Covers the benefits of the Backend For Frontend pattern and why it's a popular way to introduce GraphQL. 
* how to remain agile and support a production application throughout this process.

## What is GraphQL?
* Many of you will already know about GraphQL. I want to give a quick 101 regardless. 
### Let's talk about what GraphQL is. 
* Here are a few definitions. If you go to the official GraphQL website, the documentation will tell you that it is a **query language for APIs.** I also quite like the definition of a **language for requesting remote data.**
* Finally, you've probably heard GraphQL talked about as the **cool, popular new alternative to REST.**
* This is a definition that I think encompasses all of that from How to GraphQL, which is a great website for learning how to GraphQL. It's howtographql.com. They say **GraphQL is a new API standard that provides a more efficient, powerful, and flexible alternative to REST.**

### Here are some things that GraphQL is not. 
* GraphQL is not a database language. 
* It's not related to graph databases in any way. 
* It's not anything to do with Neo4j. It is a query language for APIs not for databases. 
* It **provides an interface to describe data, regardless of where that data is stored, whether that's a database or another API.**
* GraphQL is not just for React or JavaScript developers. GraphQL may be extremely popular with web developers. JavaScript is not the only language in which you can write and work with GraphQL. 
* GraphQL can be used anywhere that a client communicates with an API regardless of the language. There are **libraries for working with GraphQL in Python, Go, Ruby, Java.**

### Here are some of the key differences between REST and GraphQL. 
* In REST APIs, you'll usually have multiple endpoints. You have a Content API that gives content for a news website, you might have an endpoint, which is /article and one which is /video. The article endpoint will give you article data. The video endpoint will give you video data. 
* In GraphQL, there is **only one multipurpose endpoint.** This single endpoint can provide all the data that that API is concerned with. 
 * If it's a Content API, then you can go to /GraphQL to find out about articles, videos, galleries, and whatever else that API cares about. 
* In REST, you get the same set of fields from an endpoint every single time. If I'm looking up an article, I will always get the same 50 fields every single time. Even if I only want the title of an article, if I make a request to the article endpoint, I'll probably get the body, the contributors, the categories, the tags, a bunch of metadata, and probably a lot of stuff that I won't use. 
* With GraphQL, you **get exactly the fields that you ask for**, no more and no less. You specify exactly the fields that you want, and GraphQL will give those to you.

## Key Concepts in GraphQL
* The key concepts in GraphQL are schema and query. **The GraphQL schema tells you what fields you are able to request from the API.** Then you write a GraphQL query describing the data fields that you want. It's like a shopping list for all the data that you want back from the API. You will get back exactly the data that you ask for in your query.

*  Let's do the BFF software design pattern, which does not stand for best friends forever. It stands for a **Backend for Frontend API.** This is a software design pattern that was first popularized by SoundCloud a number of years ago. It's a design pattern for internal APIs. I'm talking about APIs that are internal to a particular organization, rather than published as a third-party API for the public to use.

* I want to talk about what the Backend for Frontend API pattern is offering an alternative to. That is the one size fits all API. **This is a monolithic API that is shared between multiple applications or frontends inside of an organization.** It most likely wraps the primary data source inside of that organization. It might look like this where you have multiple applications, all speaking to a single shared API. These applications might have different user experiences or use different parts of that shared API. Because it is a one size fits all API, the API must serve all of these clients equally. It is a monolith that is a common denominator between all platforms.

* It's not necessarily a bad idea to share an API between different applications. There are some common pain points in this scenario. 
  * Firstly, different clients need different sets of data. The one size fits all has to try and serve all of these different needs. Unfortunately, it's almost impossible to provide the perfect endpoint for every single client. If it tries to do this, the monolith is probably going to become increasingly unruly as it tries to keep up with the demands of all the different clients.
  * Secondly, the shared API becomes a bottleneck when rolling out new features. Every time a new feature is required, the frontend team has to coordinate with the API team or the backend team, which is responsible for the single shared API. This API team then in turn has to balance the priorities of all of the different clients. Because of the nature of software, your priority might not always be the top of the list. 
    * This is where the Backend for Frontend design pattern comes in. **In order to solve the pain points of having one API and multiple consumers, the BFF pattern recommends building one API per client.** That means that each frontend essentially has its own custom API, which is built and maintained by the same team as the frontend.

* It might look a bit like this. **A BFF is created as an interface between each API consumer and a shared API or data resource.** The BFF implements API logic that is specific to that particular application. It's essentially a translation layer that ensures data is transformed specifically to suit the needs of that particular client. **Clients might be using multiple APIs, in which case, the BFF can also act as an API gateway that is defined just for a single application. It will perform the task of aggregating and combining all the data from a set of APIs into a common format that is convenient for the client.**

### What are the benefits of this? 
* Firstly, it's easier to adopt the API as UI requirements change. As a frontend developer, now instead of having to wait for the API team to create a particular endpoint for you or integrate a new field, or a new set of data, you now have the power to just go ahead and make those changes yourself. 
* It also simplifies the process of lining up server and client releases. Now that one team manages both the UI and the API, there's no longer coordination that has to happen between a frontend and a backend team. 
* Thirdly, because it's focused, the BFF API will be smaller than the shared single purpose API. It'll probably be easier to understand and navigate and will probably have smaller payloads if it's a REST API. Finally, you're able to aggregate multiple calls to downstream APIs into a single call to the BFF, which is a lot simpler and often more performant.


