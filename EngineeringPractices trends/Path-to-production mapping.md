## Path to Production Mapping

* Although path-to-production mapping has been a near-universal practice at Thoughtworks since codifying Continuous Delivery, we often come across organizations unfamiliar with the practice. 
* The activity is most often done in a **workshop with a cross-functional group of people — that includes everyone involved in designing, developing, releasing and operating the software — around a shared whiteboard (or virtual equivalent).** 
  * First, the steps in the process are listed in order, from the developer workstation all the way to production. 
  * Then, a facilitated session is used to capture further information and pain points. 

* The most common technique we see is based on [value-stream mapping](https://en.wikipedia.org/wiki/Value-stream_mapping), although plenty of process map variants are equally valuable. 
* The activity is often eye-opening for many of the participants, as they identify delays, risks and inconsistencies and continue to use the visual representation for the continuous improvement of the build and deploy process. 
* We consider this technique so foundational!!


### Detailed Steps

A path to production maps the steps, people, tools, tasks and output for software request/change to reach production.

It is a great technical inception activity for fostering conversations about cross functional requirements, build pipeline, continuous delivery and quality. It is very useful to make it visible the overall process time with all the queues and wait times.

Step by step

1. Ask the participants to represent the step by step of a new code (or fix/change) takes from the developer machine to the final product artefact (usually deployed in the production environment)
2. For each step, add notes under it for a few categories; for example: people, tools, tasks and output
3. Consider renaming the categories for your specific context


Note for Lean Inception facilitators
I have used Path to Production on many technical inceptions, but, at times, I use it on Lean Inceptions for one of the following two reason:
1. I’ll use the path to production in a Lean Inception that needs to raise the attention to the build pipeline (needed for pushing the MVP features to production).
2. I’ll use the path to production in a Lean Inception that the product itself is very technical (for example a platform, a cloud or a pipeline). In such cases, I keep the Lean Inception agenda, but I’ll adapt it as needed; for example I’ll rename an activity from ‘User Journey’ to ‘Code Journey’

Now let’s look at a software delivery process of a team that uses a hybrid of agile and waterfall methodologies:
![P2P](https://content.cdntwrk.com/files/aHViPTYzOTc1JmNtZD1pdGVtZWRpdG9yaW1hZ2UmZmlsZW5hbWU9aXRlbWVkaXRvcmltYWdlXzYwZGRmZWQ3YTQ4YTAuanBlZyZ2ZXJzaW9uPTAwMDAmc2lnPTg5OGVhYzNhMTkyZWRmMWNjNDIyYmRjYzgzZWMxZTA0)

**Path-to-production analysis allows IT leaders to identify opportunities for shipping better software, faster. It is best to optimize the process using an iterative approach, to both reduce any organizational resistance and allow the team to assess the impact before any further changes are made.**


#### Here’s how such a path-to-production session will look in practice:

* Have your entire team present. Please note that it is of paramount importance that your Product Owner and Team Leads are there, not just the team. 
* Prepare a blank wall or a large piece of paper where you can put sticky notes. From experience, you should have about 4 meters of usable space available
* Have sticky notes in four colors ready, one color each for people, media, deliverables, and security controls
* Start with the groups of people where input for your product comes from. This might be marketing, sales, expert groups. steering bodies, etc.. Then focus on who acts on the deliverables these groups produce, and where that information flows. These groups will be numerous, however many people in your team will be hearing about them for the first time.
* When you are confident that you have captured those groups, move subsequently closer to where your team is becoming involved. Typically, there will be some kind of refinement meetings where the functional requirements are worked out, and possibly architecture groups that define cross-functional requirements for the software produced by the company’s teams.
* Then, move on to capture the steps on you kanban board: When is a story going into development? How is that prioritized and picked up?
* Subsequently, capture what happens in your continuous integration/deployment pipelines
* Finally, how are your systems brought and kept operational? Is there a “firefighting team” for live support? Are there any logging or monitoring solutions you use
* How do you feed information about your live systems behavior back into development? Is there a bug tracking workflow?

**P2Ps create a shared responsibility in the entire team and create a common understanding and empathy for the work of other team members which are crucial for shared ownership of security. Security work starts with the first discussions of features, long before a story appears on the kanban board.**

## Secure P2P
[Secure P2P](https://www.thoughtworks.com/insights/articles/towards-a-secure-path-to-production)

