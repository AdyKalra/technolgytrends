![gateway-pattern](https://martinfowler.com/articles/gateway-pattern/gateway.png)

Interesting software rarely lives in isolation. The software a team writes usually has to interact with external systems, these may be libraries, remote calls to external services, interactions with a database, or with with files. Usually there will be some form of API for that external system, but that API will often seem awkward from the context of our software. The API may use different types, require strange arguments, combine fields in ways that don't make sense in our context. Dealing with such an API can result in jarring mismatches whenever its used.

**A gateway acts as a single point to confront this foreigner. Any code within our system interacts with the interface of the gateway, which is designed to work in the terms that our system uses. The gateway then translates this convenient API into the API offered by the foreigner.**

While this pattern is widely used (but should be more prevalent), the name "gateway" has not caught on. So while you should expect to see this pattern frequently, there is no widely-used name for it.

### How it Works
**A gateway is typically a simple wrapper. We look at what our code needs to do with the external system and construct an interface that supports that clearly and directly. We then implement the gateway to translate that interaction to the terms of the external system.** This will usually involve translating a familiar function call into what's required by the foreign API, adjusting parameters as needed to make it work. When we get the results, we then transform those into a form that's easily consumable in our code. As our code grows, making new demands on the external system, we enhance the gateway to continue to support its different needs.

Gateways should only include logic that supports this translation between domestic and foreign concepts. Any logic that builds on that should be in clients of the gateway.

**It's often useful to add a connection object to the basic structure of the gateway.** The connection is a simple wrapper around the call to the foreign coded. The gateway translates its parameters into the foreign signature, and calls the connection with that signature. The connection then just calls the foreign API and returns its result. The gateway finishes by translating that result to a more digestible form. The connection can be useful in two ways. Firstly it can encapsulate any awkward parts of the call to the foreign code, such as the manipulations needed for a REST API call. Secondly it acts as a good point for inserting a Test Double.

### When to Use It
I use a gateway **whenever I access some external software and there is any awkwardness in that external element. Rather than let the awkwardness spread through my code, I contain to a single place in the gateway.**

Using a gateway can make a system **much easier to test by allowing the test harness to stub out the gateway's connection object.** This is particularly important for gateways that access remote services, as it can remove the need for a slow remote call. It's essential for external systems that need to supply canned data for testing but aren't designed to do so. I would use a gateway here, even if the external API is otherwise okay to use (in which case the gateway would only be the connection object).

Another virtue of a gateway is that it makes much easier to swap out an external system for another, should that happen. Similarly should an external system change its API or returned data, a gateway makes it much easier to adjust our code since any change is confined to a single place. But although this benefit is handy, its hardly ever a reason to use a gateway, since just encapsulating the foreign API is justification enough.

A key purpose of the gateway is to translate a foreign vocabulary which would otherwise complicate the host code. But before doing that, we do need to consider whether we should just use the foreign vocabulary. I have come across situations where a team has translated a widely-understood foreign vocabulary into a particular one for their code base because "they didn't like the names". There's no general rule I can state for this decision, a team has to exercise its judgment on whether they should adopt the external vocabulary or develop their own. (In Domain Driven Design patterns this is the choice between Conformist and Anticorruption Layer.)

A particular example of this is where we are building on platform and considering whether we wish to isolate ourselves from the underlying platform. In many cases the platform's facilities are so pervasive that it's not worth going through the effort of wrapping it. I won't consider wrapping a language's collection classes, for example. In that situation I just accept that their vocabulary is part of the vocabulary of my software.

Source:[gateway-pattern](https://www.ctouniverse.com/edition/weekly-business-continuity-off-the-shelf-2021-08-07?open-article-id=19945117&article-title=gateway-pattern&blog-domain=martinfowler.com&blog-title=martin-fowler)
