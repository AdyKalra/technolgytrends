# The GoLD Stack
* **GoLang + Lambda + DynamoDB**

### Reasons
* [Why we like Go](https://dev.to/prozz/how-i-go-31jj)
* [How to write testable lambdas in Go](https://dev.to/prozz/serverless-in-go-how-to-write-testable-lambdas-4925)
* [Why even our front-end engineers like serverless](https://tlakomy.com/why-im-excited-about-serverless)
* [About deploying Go lambda with the serverless framework](https://maciejwinnicki.com/a-better-way-of-deploying-go-services-with-serverless-framework/)
* [How GoLD enables a more cost-aware culture](https://twitter.com/mthenw/status/1272549552265072640?s=21)
* [how serverless can give you a competitive edge](https://dev.to/szymanskilukasz/why-companies-will-adopt-serverless-sooner-than-you-think-27m7)

## GoLD stack could become the LAMP of the 2020s.
* To be clear, while GoLD nicely captures the core of the stack, it doesn’t describe a full one. In our context, in addition to using Go to write our Lambdas, and using DynamoDB as the main data store, we deploy using the serverless framework, and are heavy users of SNS, SQS, Kinesis, and S3 as well.

### Scaling and cost transparency
* When AWS launched 14 years ago one of its selling point was “pay for what you use.” In those early days, with primarily S3 and EC2 as services offered, this meant: you pay for the data you store, and the hours you run your VMs. Still, for the compute part it didn’t really matter if you used all of the CPU cycles, memory or allocated disk space — you picked your instance type, and you paid for the whole thing independent of “internal” utilization.
* If you outgrew your instance, you either scaled horizontally by adding another instance, or vertically by spinning up a bigger instance. 
* Over the past 14 years the AWS offering evolved a lot into two dimensions (yes, dimensions again):
  * A suite of “serverful” services, where visibly you spin up a cluster of EC2 instances (and associated services) that are preconfigured and managed by AWS to run some specific service, such as most of RDS, ElastiCache, Redshift, ECS, and EKS. 
  * AWS takes a lot of the operational burden (maintenance, backups, sometimes upgrades, sometimes scaling) but the way you provision these is still at the level of EC2 instances, so you select instance types, cluster sizes, scaling policies etc.
* A suite of **serverles services**, where the level of abstraction is higher and you tend to pay per request, messages passed, CPU cycles consumed, storage used, and are pretty much oblivious to the resources that power them behind the scenes — services like this include **SNS, SQS, Lambda, DynamoDB, and API gateway.**
  * Now intuitively, while you lose some level of control with the serverless options, what’s good is there’s a very close correlation between actual use and cost. If your service gets 0 requests, your cost will be close to $0, and if it gets more it’s fairly easy to calculate and track what the cost would be and where the money goes.
  * This tends to be much more implicit with many of the “serverful” services, where you pay e.g. for a 3 node DB cluster which will initially be underutilized, eventually reach capacity and then you need to scale it. 
  * The granularity is always measured in nodes, though, not e.g. number of read or write queries to particular tables like DynamoDB.
* Aren’t serverless solutions more expensive at scale, though? 
  * I think there are cases where it may be — consistently the conclusion has been that it’s been surprisingly affordable, and cheaper than serverful options. 
  
### Time to value
* Project built on the GoLD stack seem to see their first production release more quickly than non-GoLD projects, and quicker iterations after. 
  * This means: a **short time-to-value cycle** 
* From a technical perspective, it makes sense. Assuming you have an AWS account ready to go, all you need to do is install the serverless framework, look at some example serverless.yml file with Go examples, perhaps add a DynamoDB table definition, and sls deploy and you essentially have a production ready setup, no prepared additional infrastructure required (such as kubernetes, ECS, EB or database clusters).
* Because solutions built on the GoLD stack (or serverless in general) tend to involve a mix or a number of AWS services that are hard to fully emulate locally, testing in “production” (actual AWS) is largely inevitable. 
  * Sure, you write most of your automated tests at the lambda level, but to truly test the integrated whole, the best way to get confidence is to push it to either a staging environment on AWS, but since that “staging environment” is effectively the same thing as production — why not push it to production as well? 
  * Feature flags control access to features anyway, right? You are using feature flags, right?
* If it’s technically easy to push to production, you just do it more often, because why not? It adds to the level of confidence you have that things actually work the way they should, even if customers don’t get to interact with all of it yet.
* Another hint about why the GoLD stack may have a shorter Time to Value is nicely visualized in this graphic (under “Serverless”):
![Gold](https://miro.medium.com/max/700/0*gc1dKZox-_-h0__b.png)

### Onboarding
* As alluded to, deploying something basic on a GoLD stack is quite trivial, and an engineer can likely do this on her first day even if starting out with an empty AWS account.
  * Go as a language is relatively simple. To some it may feel unnecessarily low-level, but once you get over the fact you have pointer and non-pointer types, people with a solid programming background tend to be productive in Go in a matter of days. And quickly, you simply know the entire language, and it’s a matter of learning the “Go way” to solve problems. Go is very explicit, there’s little magic, relatively few “gotchas” compared to other languages, and there’s little room for clever APIs that allow you to write that for-loop in a single line, like other languages like Kotlin, Ruby, Rust and Scala would let developers do. Likely, you just have to suck it up and write out the for-loop every time, but at least anybody new to the project (and even new to the language) will instantly understand what’s going on, without being aware of magic provided by macros, reflection, aspects, or dynamic code generation.
#### From a management perspective, there’s a lot to like about Go as well: 
* it’s a relatively mature language, has a mature ecosystem, has solid backing from Google and others, it has proven to scale to large code bases (types help) if that would be required (ideally it wouldn’t be, lambda ought to be small), and it comes with a toolchain that eliminates the need for unproductive discussions, such as:
  * How code ought to be formatted (go fmt decides)
  * What package manager to use (go mod)
  * How to keep code clean and consistent: some things like capitalization of type and function names change semantics, and various types of dead code, like dead imports and dead variable declarations simply result in compile-time errors, go vet checks for various other pitfalls
#### On AWS lambda, Go is a first-class citizen, you don’t need custom runtimes to run it, and the Go AWS SDK is well maintained.
* Lambda as a runtime is easy to grasp. The event model may be a bit of a mind bend if you’re not used to thinking this way 
* But conceptually there’s not that much you need to understand to write lambdas: you write Go code, compile it, zip up the binary (which the serverless framework will upload to S3), and when certain events occur (such as SNS notifications, SQS messages, incoming API Gateway calls, DynamoDB stream events) your code is pulled down and run in some environment where your only real lever is how much memory you allocate to it (although this has implications on CPU as well, which is a bit of a gotcha).
* Running Go on lambdas is a good fit, because Go compiles into a single binary, which is quick for the lambda environment to pull down and boot. Also, since Go processes require relatively little memory, you can run them in low-memory (and therefore cheaper) configurations if that makes sense. 
* There’s a lot of ado about lambda cold starts (whether your lambda invocation will boot up a new lambda process or reuse an already running one, which obviously is more performant), but if you write in Go this is of relatively little concern — in this sense it’s probably one of the fastest options. 
  * There’s a story (not sure about the source) that the original API Gateway implementation runs on AWS Lambda with the logic implemented on top of the Java runtime, which has serious cost implications (because Java cold starts are slower and the JVM consumes quite a bit of memory). The new HTTP API offering is supposedly implemented in Go, and as a result significantly cheaper.
#### DynamoDB as a database is probably the tougher case in terms of onboarding. 
* A little while ago The DynamoDB Book came out, essentially a must read if you would like to use this service. 

### Culture and recruitment
* There’s a few ways that I see the GoLD affecting engineering culture:
#### Cost awareness 
* because of the pay-for-use model, engineers become very sensitive and aware of cost and closely monitor it.
#### Focus on monitoring 
* without proper monitoring, it’s rather hard to even debug basic issues on this stack. Since there’s so many interconnected, but loosely coupled parts, it is simply impractical not to invest in monitoring early. 
  * Luckily AWS publishes plenty of CloudWatch metrics about every deployed resources, and aggregates logs from lambda automatically — all that remains to be done is putting it together with dashboards and alerts.
* The type of people attracted to this stack is a bit different — let me expand on that in the context of recruitment.
### On recruitment. 
* Let’s be realistic. GoLD may be cool, but it’s far from being mainstream. The chances you will be able to recruit people with many years of GoLD experience on their CV is very low.
  * While this is a clear disadvantage compared to recruiting for e.g. engineers working on a LAMP stack, or a Java/Spring stack — a population that is significantly larger. 
  * It does provide an opportunity to recruit for a different mindset and culture — one that is less focused on reusing stack-specific knowledge acquired over the years, and more comfortable stepping out of their comfort zone and struggle a bit while learning something different. Something quite different, both in the language, architectural and data model dimensions. Can you handle that?
* However, to be able to support such a thing, you do need to bootstrap this process somehow. 

### The management perspective
* In management there’s a lot of angles to consider when deciding on technology stacks: maturity of the ecosystem, productivity, reliability, availability of talent able — and willing — to work on the stack in the short, but also long term. There’s no silver bullet solution to this challenge. However… now there’s a GoLD bullet one 🙃

[reference](https://medium.com/@zef/the-gold-stack-cf17ad32385f)
