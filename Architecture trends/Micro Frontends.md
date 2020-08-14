## Micro Frontends
```We've seen significant benefits from introducing``` [microservices](https://martinfowler.com/articles/microservices.html)```, which have allowed teams to scale the delivery of independently deployed and maintained services. 

Unfortunately, we've also seen many teams create a frontend monolith — a large, entangled browser application that sits on top of the backend services — largely neutralizing the benefits of microservices.```

Since we first described **micro frontends** as a technique to address this issue, we've had almost universally positive experiences with the approach and have found a number of patterns to use micro frontends even as more and more code shifts from the server to the web browser. 

So far, [web components](https://www.thoughtworks.com/radar/platforms/web-components-standard) have been elusive in this field, though.

## How Micro Frontend Has Changed Our Team Dynamic - PayPal

* Since its first start in 2016, the term “Micro Frontend” has been gaining popularity in the frontend world; especially in today’s feature-rich single-page-application web developments. But what is Micro Frontend, and what does it solve?

### What is Micro Frontend?
* A lot of web development today involves siloed domain teams. Many adopt Microservices architecture, which allows teams to independently develop and deliver their applications. The idea is to **enable rapid, frequent, and reliable delivery of large, complex applications** by separating backend services into smaller (micro) services organized around the business logic.
![Microservices architecture](https://miro.medium.com/max/700/1*STvOWkbwkhuJj2Zgr4aeug.png)

* In general, frontend teams work on the user interface while backend teams handle the (micro) services. In the above diagram, a UI team manages the client application, which relies on services maintained by five other service teams. These service teams are often structured around specific business capabilities; they are loosely coupled and new features are pushed to production far more often than the client application. **Frontend, however, does not share the same modularity as its backend counterpart. In other words, the frontend becomes a monolith; one that would require knowledge about the whole backend services to render its views. As new changes are added to the frontend, it would eventually become too hard to maintain.**

* The Micro Frontend approach tackles these kinds of monolithic frontend issues by **extending the principles of Microservices to frontend development.** Instead of dividing the application’s architecture into frontend and backend, the **application itself is divided into multiple independent pieces — from the backend service and database right up to the user interface — and then merged into a single user-facing frontend.**

* Cam Jackson, in his article “Micro Frontend”, defined Micro Frontend as: **An architectural style where independently deliverable frontend applications are composed into a greater whole**
The below diagram illustrates this definition:

![Micro Frontend Architecture](https://miro.medium.com/max/700/1*ypru_ebUVp8A8cEbS_ZXUw.png)

* In the above diagram, we now see that the client application is divided into features where Feature A is worked on by three different teams (UI Component A and Service A + B), Feature B is worked on by two teams (UI Component B and Service C), and so on. Each team now owns a feature within a client application from end-to-end.

### Our Implementation
* **Fragments** are a set of patterns and principles that bring the Micro Frontend approach to PayPal. Fragments empower domain teams to continue building features however they see fit while enabling them to share those features with others in a composable way. **A fragment is a web application with its HTML, CSS, and JS that is packaged in a JSON object. Running a fragment is as simple as downloading the fragment JSON and using a utility method to unpack and render the fragment to the DOM.**
#### The key concepts behind fragments and Micro Frontends are that they allow for:
* **Decoupling of teams and codebases** — Teams do not have to worry about coordinating tech stack, runtime, upgrades with other teams, etc.
* **Independent release cycles** — Fragments can have their continuous testing/delivery pipeline with little thought to the state of other codebases
* **Shared user experiences** — The same fragment can be used on multiple pages to allow for consistent customer experience

* A good example of our fragments pattern in action is the PayPal Merchant’s Dashboard. All the “widgets” on the page are fragments, each managed by a different team, responsible for their respective functionality and business logic of their fragment.

![Our Micro Frontend Merchant’s Dashboard](https://miro.medium.com/max/700/1*m1TatPoR7LvZ7fN5M_COCQ.png)

* In this example, the teams are:
  * Team Dashboard — responsible for maintaining the dashboard wrapper
  * Team Header — responsible for maintaining the global header with links to child pages
  * Team Quick links — responsible for displaying apps that are relevant to the merchant
  * Team Activation — responsible for displaying setup steps and sub-steps for each app that the merchant is integrating with
  * Team Balance — responsible for displaying merchant’s balance
  * Team Insights — responsible for displaying merchant’s money in / out within a specified period

![All fragments combined into one page](https://miro.medium.com/max/700/1*JW364X2ePoS9dF208wj4HQ.png)

* Each of these teams owns, develops, and maintains a separate fragment. These fragments are predominantly React components packaged in a node module but can be built by using any other JS lib out there like Angular or Vue or just vanilla JS, HTML, and CSS. They are no longer bound by a single framework. Suddenly our frontend world becomes more interesting.

### How does this change the team dynamic?
* With Microservices and Monolithic Frontend, we see teams separated by their skills or technologies. It makes sense after all, right? Frontend developers work as a team on the frontend layer; Backend developers work as a team on the backend layer. **With this architecture, teams will be specialized within their field; no cross-pollination of skills occurs. But what happens if we separate different functionalities within the same application and create teams based on that?**

* Our fragment teams consist of frontend developers, backend developers, product managers, and designers. Team members are exposed to different perspectives and methods to solve problems, and this results in more efficient and creative ways to solve the tasks at hand. This multi-dimensional team dynamic makes it easier for team members to understand the impact of their work from end-to-end and allows for a better sense of ownership of specific functionalities they are working on.

### Final Thoughts
* Micro Frontend changes the way we think and work to solve problems. **Imagine having a page where each component is its own mini-application or having the ability to inject the same features/flows into different applications and pages. It opens up the possibility of a dynamic and ever-evolving environment.** Of course, there is a big paradigm shift here; from a separation of architectural layers to a separation of features; so it might not be suitable for your organization or projects. We have been fortunate enough to have found a project where this can help our teams collaborate to build the page merchants visit most when they log in to our system. We certainly hope you find a project where Micro Frontend helps your team, too!

[Source](https://medium.com/paypal-engineering/how-micro-frontend-has-changed-our-team-dynamic-ba2f01597f48)

