# Coordinating code deploys and continuous integration in Slack
## Overview
* Software development at large organizations often entails dozens, even hundreds, of programmers working concurrently on millions of lines of code. Their success, however, is measured by a more precise metric: how quickly they can get what they build into their customers’ hands.
* Slack is a powerful addition to the toolchain of apps required to properly test, document and deploy code. It acts as a discussion space to foster collaboration and help support the efforts of engineering teams but also as a centralized, long-term record of what’s taken place, which includes most of the other apps your team may use.
* Here at Slack, we deploy dozens of code changes to production servers multiple times a day. To get the granular details of our in-house process, check out our post on [Code Deploys](https://github.com/AdyKalra/technolgytrends/blob/master/EngineeringPractices%20trends/Code%20Deployment%20best%20practices.md)


### Use deploy and CI apps to increase visibility into code changes
* Deploying code involves lots of scripts and automation, but many options now exist for these environments, so software development teams don’t need to reinvent the wheel.
![CodeDeploys_circle](https://slackhq.com/wp-content/uploads/2021/07/2020-07_Haughey_CodeDeploys_circle-ci.png)

* There are a variety of continuous integration (CI) apps for Slack—our most popular ones are **Jenkins CI, CircleCI and Travis CI**—and they all do a great job of integrating with existing CI systems that report back into Slack when changes occur. 
* This helps your team monitor and track changes to your codebase in production, especially if you create dedicated channels for these notifications. Your entire team can check in from time to time to see when new releases go out. If issues arise, a channel like this can help your team catch the releases that caused the issues so they can be rolled back.
![CodeDeploys_slash](https://slackhq.com/wp-content/uploads/2021/07/2020-07_Haughey_CodeDeploys_slash-deploy.png)
* Slack apps focused on deploys are also available, such as DeployHQ, Codeship and SlashDeploy. These apps bring that same transparency and visibility to your whole team when code changes are headed out to production, but they also offer slash commands to invoke those deploys, so your team can update your codebase without leaving Slack.

### How Slack’s engineering team organizes deploy channels
* We use a few channels to document and coordinate our deployments. First, there’s the #deploys channel, which shows a real-time stream of incremental changes throughout the day. * It also acts as the central channel for our daily deploy commanders, designated engineers in charge of reviewing recent changes and monitoring the health of our deploys.
![CodeDeploys_deploy](https://slackhq.com/wp-content/uploads/2021/07/2020-07_Haughey_CodeDeploys_deploy-cal.png)

* We have a rotating schedule of developers to work these on-call shifts, and we use the Google Calendar for Team Events app to remind everyone in the channel when a new commander’s shift begins. We also update the channel topic with the deploy commander’s name at the start of their shift so people know at a glance whom to contact.
![server-graphs](https://slackhq.com/wp-content/uploads/2020/07/server-graphs.png?w=1187)

* During their shifts, deploy commanders approve previously tested code, trigger the commands to release it, and watch graphs (created with Grafana) of our real-time server health. If a problem crops up, commanders can either discuss it with others or ask for help from our backend infrastructure/operations crew.
![CodeDeploys_allclear](https://slackhq.com/wp-content/uploads/2021/07/2020-07_Haughey_CodeDeploys_all-clear.png)

* We also use Workflow Builder to streamline posting when a deploy has been cleared. When a commander issues a deployment and can see that it’s reached 100% of servers with no ill effects after a review period, they hit the shortcuts menu to launch a Workflow Builder action that automatically posts their “all clear” message along with their username to show it’s fully complete.
![CodeDeploys_checkpoint2](https://slackhq.com/wp-content/uploads/2021/07/2020-07_Haughey_CodeDeploys_checkpoint2.png?resize=768,672)

* Our second channel is called #deploys-discuss, which, as the name suggests, was created for discussion related to deploys. Every morning it posts a rollup of deploys from the previous day, showing how long each deployment took, how many pull requests were included, and which deploy commander oversaw it. It’s a good way to get a quick overview of performance. Anyone can join to chat freely with the deployment team, whether it’s asking questions or sharing advice. It’s less rigorous than #deploys, and people often use this channel to trade deploy commander shifts with one another.

* Our Operations team uses #ops to talk about work on the backend infrastructure that keeps our servers running. It’s an open forum for asking questions or discussing our infrastructure health after deploys. It’s also where deploy commanders report issues and ask for assistance.

### Bringing transparency to the deployment process
* Our setup and approach to managing deployments has evolved over time with the goal of being as transparent and comprehensive as possible. The #deploys channel is a historical record of everything that has taken place. Anyone on the team can refer back to it later, which is helpful when we get a bug report. By looking at the time the bug reports started coming in, we can identify the deploy that caused the issue, and either roll it back or fix it forward.
* By sharing everything openly in channels, engineers can pass messages about important deploys or warnings into other channels or DMs and help solve problems together, instead of losing details in siloed inboxes.
