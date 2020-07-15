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

