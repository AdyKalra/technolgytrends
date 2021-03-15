## Maximizing Developer Effectiveness

Source: https://martinfowler.com/articles/developer-effectiveness.html

### Framework for maximizing developer effectiveness
* Key developer feedback loops, including micro-feedback loops that developers do 200 times a day. These should be optimized so they are quick, simple and impactful for developers.
* The teams are paralyzed with a myriad of dependencies, cognitive overload, and a lack of knowledge in the new tools/processes.
* Engineering organization has neglected to provide developers with an effective working environment. While transforming, they have introduced too many new processes, too many new tools and new technologies, which has led to increased complexity and added friction in their everyday tasks.

#### Day in the life in a highly effective environment
The developer:
* checks the team project management tool and then attends standup where she is clear about what she has to work on.
* notes that the development environment has been automatically updated with libraries matching development and production, and the CI/CD pipelines are green.
* pulls down the latest code, makes an incremental code change that is quickly validated by deploying to a local environment and by running unit tests.
* depends on another team’s business capabilities for her feature. She is able to find documentation and the API spec through a developer portal. She still has some queries, so she jumps into the team’s Slack room and quickly gets some help from another developer who is doing support.
* focuses on her task for a few hours without any interruptions.
* takes a break, gets coffee, takes a walk, plays some ping pong with colleagues.
* commits the code change, which then passes through a number of automated checks before being deployed to production. Releases the change gradually to users in production, while monitoring business and operational metrics.
* The developer is able to make incremental progress in a day, and goes home happy.

#### Day in the life in a low effective environment
The developer:

* starts the day having to deal immediately with a number of alerts for problems in production.
* checks a number of logging and monitoring systems to find the error report as there are no aggregated logs across systems.
* works with operations on the phone and determines that the alerts are false positives.
* has to wait for a response from architecture, security and governance groups for a previous feature she had completed.
* has a day broken up with many meetings, many of which are status meetings
* notes that a previous feature has been approved by reviewers, she moves it into another branch that kicks off a long nightly E2E test suite that is almost always red, managed by a siloed QA team.
* depends on another team's API, but she cannot find current documentation. So instead she talks to a project manager on the other team, trying to get a query. The ticket to find an answer will take a few days, so this is blocking her current task.

### Developer effectiveness
* What does being effective mean? 
    * As a developer, it is delivering the maximum value to your customers. It is being able to apply your energy and innovation in the best ways towards the company’s goals. An effective environment makes it easy to put useful, high-quality software into production; and to operate it so that the developers do not have to deal with unnecessary complexities, frivolous churn or long delays — freeing them to concentrate on value-adding tasks.

#### Change
* read Accelerate and the State of DevOps report. They know what type of organization they are striving to build. The four key metrics (lead time, deployment frequency, MTTR and change fail percentage) are great measures of DevOps performance.

### Feedback Loops
The key loops identified are:
![loops](https://user-images.githubusercontent.com/8856857/111218328-afbbc900-862a-11eb-8b11-cc759e4228ec.png)

* The metrics are based on what I have observed is possible. Not every company needs every feedback loop to be in the high effectiveness bucket, but they provide concrete goals to guide decision-making. Engineering organizations should conduct research within their specific context to figure out what cycles and metrics are important technology strategy.
* It is useful to look at what techniques have been applied to optimize the feedback loops and the journey that companies have taken to get there. Those case studies can provide many ideas to apply in your own organization.

![feedback](https://martinfowler.com/articles/developer-effectiveness/feedback-loops.png)

* The diagram above shows a simplified representation of how developers use feedback loops during development. You can see that the developer validates their work is meeting the specifications and expected standards at multiple points along the way. The key observations to note are:

1. Developers will run the feedback loops more often if they are shorter.
2. Developers will run more often and take action on the result, if they are seen as valuable to the developer and not purely bureaucratic overhead.
3. Getting validation earlier and more often reduces the rework later on.
4. Feedback loops that are simple to interpret results, reduce back and forth communications and cognitive overhead.

* When organizations fail to achieve these results, the problems are quickly compounded. There is a great deal of wasted effort for the developers. Embodied in the time spent waiting, searching, or trying to understand results. It adds up, causing significant delays in product development, which will manifest as lower scores in the four key metrics (particularly deployment frequency and lead time).

### Introducing micro feedback loops
* From what I have observed, you have to nail the basics, the things that developers do 10, 100 or 200 times a day. I call them micro-feedback loops. This could be running a unit test while fixing a bug. It could be seeing a code change reflected in your local environment or development environments. It could be refreshing data in your environment. Developers, if empowered, will naturally optimize, but often I find the micro-feedback loops have been neglected. These loops are intentionally short, so you end up dealing with some very small time increments.
* It is hard to explain to management why we have to focus on such small problems. Why do we have to invest time to optimize a compile stage with a two minute runtime to instead take only 15 seconds? This might be a lot of work, perhaps requiring a system to be decoupled into independent components. It is much easier to understand optimizing something that is taking two days as something worth taking on.
* Those two minutes can add up quickly, and could top 100 minutes a day. These small pauses are opportunities to lose context and focus. They are long enough for a developer to get distracted, decide to open an email or go and get a coffee, so that now they are distracted and out of their state of flow, there is research that indicates it can take up to 23 minutes to get back into the state of flow and return to high productivity. I am not suggesting that engineers should not take breaks and clear their head occasionally! But they should do that intentionally, not enforced by the environment.
* In reality, developers will compensate by filling these moments of inactivity with useful things. They might have two tasks going on and toggle between them. They might slow their compile frequency by batching up changes. In my research both of these will lead to a delay in integration of code, and development time.

### Organizational Effectiveness
* Highly effective organizations have designed their engineering organization to optimize for effectiveness and feedback loops. Leadership over time creates a culture that leads to empowering developers to make incremental improvements to these feedback loops.
* Technical leaders continually measure and re-examine effectiveness. Highly effective organizations have created a framework to make data-driven decisions by tracking the four key metrics and other data points important to their context. This culture starts at the executive level and is communicated to the rest of the organization.
* In addition to the metrics, they create an open forum to listen to the individual contributors that work in the environment day to day. Developers will know the problems they face and will have many ideas on how to solve them.
* Based on this information, engineering managers can decide on priorities for investments. Large problems may require correspondingly large programs of modernization to address a poor developer experience. But often it is more about empowering teams to make continuous improvement.
* A key principle is to embrace the **developer experience.** It is common to see a program of work of a team focused on this. Developer experience means technical capabilities should be built with the same approaches used for end-user product development, applying the same research, prioritization, outcome-based thinking, and consumer feedback mechanisms.
* After commitment, measurement and empowerment comes scaling.
* At a certain organizational size, there is a need to create efficiency through economies of scale. Organizations do this by applying platform thinking - creating an internal platform specifically focused on improving effectiveness. They invest in engineering teams that build technical capabilities to improve developer effectiveness. They regard other development teams as their consumers, and the services they provide are treated like products. The teams have technical product managers and success metrics related to how they are impacting the consuming teams. For example, a platform capability team focused on observability creates monitoring, logging, alerting, and tracing capabilities so that teams can easily monitor their service health and debug problems in their product.


* Governance can have a critical role in effectiveness when it is implemented via:
1. Clear engineering goals
2. Specifying ways that teams and services communicate with each other
3. Encouraging useful peer review
4. Baking best practices into platform capabilities

Automating control via architecture fitness functions
