# What is Auxiliary Engineering?

* If you work in software, this might sound familiar to you: an engineering team has been tasked with designing and building a large, highly visible product or system from the ground up. The team is mostly made up of newer engineers with less institutional knowledge, and the tech lead doesn’t have much experience in this particular domain. However, there’s a senior engineer with domain knowledge and some temporary availability. What’s the most effective way they can help?

* Here’s how this is often handled: the senior engineer comes in to help but does most of the work themselves. They write a ton of new code. It’s well-written but foreign to the team, who doesn’t have any insight into why any decisions were made – they see the code in its finished state, but not the process to get there. The code is handed off and now it’s theirs to own and maintain. They’ve just traded a lack of domain knowledge for a lack of knowledge in their own codebase.

* Let’s go back to when the senior engineer arrives. What if instead of writing all the code, they coach the team through the whole process? They become part of the team for a few months, helping create tickets, give architectural advice, and have daily pair programming sessions. The team writes all the code themselves so there’s no handoff at the end. They understand the new code top to bottom, and they’re more proficient at writing code in general. Not only are they better equipped to pick up the next project, they can be a resource for other developers. All the while, the senior engineer has been getting hands-on feedback to help improve the platform tools used across the organization, avoiding an “ivory tower” mentality on the platform.

## That’s Auxiliary Engineering 
* **“Partnering with engineering teams to increase their velocity and build a lasting culture of quality.” We travel from team to team, embedding for enough time to help developers build habits as they build an MVP.**

* The concepts I cover are shared across all Auxiliary Engineering teams, although the experiences are from my perspective on Frontend Aux Eng, focusing on JavaScript and React. I’ve been going on what we call embeds (or engagements) for over a year, iterating on the process with my team and the other Aux Eng teams. It’s an investment in engineers and engineering culture. What does it look like in practice? Read on!

### What Makes an AuxEngineer?
* Self-described “humble experts eager to learn,” we’re each equal parts engineer, teacher, mentor, and coach. Instead of “you’re not doing your job well enough,” we say: “let’s take your skills to the next level.” We’re there to support and grow skills across Wayfair’s engineering organization.

* We take copious notes and ask for critical feedback in order to improve the platform. Our engagements give us a unique chance to make platform tools better for the developers using them. Rather than assume we’re building the right tools for teams, we work with the tools directly and feel the pain points ourselves. This practice has uncovered opportunities leading to some of our largest platform wins.

* An AuxEngineer needs to have deep technical knowledge in their domain, balanced with people skills and process management. We firmly believe in the growth mindset, and we use regular retrospectives for feedback and to uncover our blind spots.

### What Does an Embed Look Like?
* Before: The vetting process
* It’s important to have teams reach out to us (rather than us approaching them) so we know they’re on board with our process. They should know what they want to get out of the engagement, namely a deliverable and a group of more proficient developers. After teams submit proposals for projects they’ll be building, we go through an interviewing period before making a commitment to a team to make sure our goals and timelines are aligned. We evaluate projects based on a number of criteria, including:

  * Business value – does the product itself provide measurable value?
  * Technical value – is the project strategic for the platform and engineering org?
  * Deliverable – What will we have to show at the end of the project?
  * Timeline – Very tight deadlines aren’t ideal, building habits takes time. We want to make sure the focus is on growing developers and not rushing a product out the door.

* We also like to meet the individual developers and make sure they’re all on board. We’ll be working most closely with them so it’s important to have their buy-in.

* Once we’ve accepted a proposal and both teams have agreed to a shared goals document, we’re off and running! Everyone has their own workflow, so there’s an introductory period where we get familiar with each developer and their process. We move to their space and work there full time Monday through Thursday. Fridays we return to the platform team to write up notes, prepare for the next week, and incorporate any actionable feedback into tools or documentation.

### During: What teams are signing up for
* Knowledge transfer from a JS expert – It should be obvious that having a resident JS expert on-hand can give teams a big boost in velocity. Less searching Stack Overflow, less combing through the internal docs. But the real value of having an onsite JS expert is that you get more than just the answer. We will provide a deeper understanding and help the developer build a robust mental model as they work, which helps sustain proficiency after we leave.

 

* Upfront Software Design – Embeds are 3-month long commitments. The teams are building an MVP of a new product, so software design is a top priority. These are apps that will be maintained for perhaps years to come, so we emphasize a clean flexible design. The product needs will evolve so we design with that in mind – the final design is never really final. We recognize that we won’t predict everything, and we allow the implementation itself to provide feedback to the initial design.

### We also help with the ticket estimation, making sure:

* All developers are involved in the estimation
  * We’re giving proportional input, not dictating estimates
  * Tickets have a well-defined scope and acceptance criteria
  * Unit/integration tests are included in every feature ticket
  * Pair Programming – Co-locating with the team means we can transfer a lot of knowledge through pair programming. We’re primarily the navigator of the pair, i.e. we explain what we’re trying to accomplish, they write the code. As they become more comfortable with the new topics our guidance becomes less explicit, preferring leading questions over direct answers.

* This is where the heavy lifting is done, and for me it’s the most interesting part. Pairing is highly dynamic, different with every single person. There’s some social navigation that needs to happen to make it productive for everyone. I love the challenge and reward that comes from this part of the engagement.

* Automated Tests – One of our requirements is that teams agree to write tests as part of the process. We consider automated tests an integral part of a healthy codebase, and since many teams don’t have testing integrated into their workflow, we’re clear that this can incur a short-term velocity hit as developers learn the tools and get into the flow of testing.

* This is all in service of “go slow to go fast,” and while it’s counterintuitive that writing code _and_ tests will speed things up, it works because “speed depends on stability“. With our guidance adding testing to the workflow, both devs and stakeholders see that it improves velocity and has well-tested code baked into the process. It gives developers confidence in their app, and confidence to make changes. In our experience, tests make code easier to refactor and help find bugs before they go to production. It’s common to hear things like “I didn’t know these things affected each other until the test broke!”

* Small, frequent deploys – This is primarily to reduce cognitive load on both the developer and the reviewer. For the developer, small frequent deploys mean to deploy a single feature, or make a few discrete changes – or even just one! Similar to the Single Responsibility Principle, deploying only one thing provides more clarity around what the effect of the deploy will be. Smaller PRs mean less reviewer fatigue, a more immediate understanding of the changes, and bugs caught and fixed faster.

* Live Code Review – I consider code review one of the most important tools for learning and working on a team. Doing it live is a great way to spread best practices, make decisions as a team, and model the soft skills needed when leaving comments. I’ve gotten some great insights watching domain experts walk through reviews, so this allows me to pass that experience along. We set a few ground rules to emphasize psychological safety, e.g. “assume best intentions,” and “comment as if the author is in the room (which they might be!)”. Nobody is trying to tear anyone down. Junior devs can learn from having their code reviewed by more senior devs, but by flipping the roles the more junior folks will be exposed to patterns they might not otherwise see (and might catch a few bugs too!)

* Live code review also gives us the opportunity to include neighboring teams, expanding our reach as we generally work with teams of no more than 5 developers. We get to meet the neighboring team members, and let them know we’re also available as a resource for them when we have extra bandwidth.

* After: Creating lasting relationships with teams
We measure success by the launch of a successful product, but also by long-term code quality and habits. After every embed we set up a 3-month check-in to see:

### How comfortable they are maintaining their code
* Have they been able to maintain velocity
* How the tests have helped, or if they’ve caused any friction
* Since the metrics we look at aren’t always immediate, we hunger for critique and look for areas where we can improve and expose our blind spots. We want to get as much feedback as possible during the embed to improve the long-term effects of what we’re doing.

## Win, Win, Win
* The host team gets the most obvious benefit from an engagement, but the Auxiliary Engineering model has benefits across the board.

### How the Host Team Benefits
* Software architecture
* Extended access to a platform engineer with deep domain and institutional knowledge
* Build lasting habits – writing tests and small, frequent deploys.
* Exposure to new patterns and technologies

### How the Company Benefits
* We’re like hired consultants but with a vested interest in the long-term health of the engineering organization.

* Healthier codebase overall
* More test coverage
* Cross-pollination of best practices
* Growing our developers
* Hands-on feedback for platforms to make sure we’re doing the right work to enable developers

### How the AuxEngineer Benefits
* This job is an exciting challenge for the embedded developer. It’s an intense experience, being expected to be the resident expert in a wide range of topics and technologies.

* Have impact on both feature and platform teams
* Work with many different parts of the codebase
* Rewards of being a coach/mentor 
### Direct impact on the business
* High challenge, high growth

### Few Things I’ve Learned
* Psychological safety is crucial for success
* Among the most important meetings are informal introductory one-on-ones with each developer. For my personal process, I like to know their background, anything specific they want to work on or learn, and what they do for fun. One of our stated goals is to build lasting relationships with these teams, and this starts with trust and psychological safety. It’s important for the individuals to know that we’re there to help and support them.

* One of the questions I often get is “so how do the developers feel about you being there?” In all my embeds I’ve never felt anything but welcome, and I attribute that to building trust out of the gate.

* It’s not my job to know everything
* The idea that an expert knows everything is harmful for a few reasons. For one, it’s unrealistic – nobody knows everything about everything. Maybe, more importantly, this mindset assumes that knowledge is static. It’s important to reinforce the idea that even experts are always learning and growing.

* My job is to figure out how I can fill in the gaps in your knowledge. If I have a knowledge gap in the same area, it’s then my job to fill that gap and remove barriers for you. That might mean research, finding someone who does know, or developing a solution myself.

* I’ve discovered over time that it’s actually MORE helpful to developers to see you work through something you don’t know, as uncomfortable as it is. It shows that even senior developers have knowledge gaps, and pulls back the curtain on my own process of debugging or working through an unknown problem.

* We get a unique perspective on process
* There are dozens of engineering teams at Wayfair. By working with teams from all different parts of the organization we get a broad view of all different kinds of processes. We see what works, what doesn’t, and we can cross-pollinate best practices and process improvements.

* Give a person an answer and you unblock them for a day…
* I always have to fight the impulse to give answers directly. I have to remind myself that our mission is long-term sustainability and that giving developers the answer will only help in the moment. It’s more impactful to ask leading questions and help a developer arrive at the solution on their own. It’s more rewarding to arrive at your own answer and more likely to stick.

* Making an Exit
* Since we only have a few months with each team, we have a short time to elevate their skills and leave them more self-sufficient when it’s time to go. A sign of success is when we’re able to transition smoothly away from the host team to the point that they almost don’t notice we’re gone, like Homer fading into the bushes. Leaving after an experience with great people is bittersweet, but the limited time makes us even more focused on the engagement. When it’s over, nothing is more rewarding than seeing a successful launch, and seeing the engineers have a higher impact, often being a resource for others.

* You can hire experts, or you can grow them. For a company the size of Wayfair there’s a huge amount of potential experts, and from what I’ve seen here, plenty of people with a drive to level up their skills. Auxiliary Engineering is a proactive, hands-on way to invest in our developers, grow our own experts, and keep raising the bar.
