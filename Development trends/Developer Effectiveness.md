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

