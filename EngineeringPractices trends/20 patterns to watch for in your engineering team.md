# 20 patterns to watch for in your engineering team
* Efective managers view their teams as complex interdependent systems, with inputs and outputs.
* When the outputs aren’t as expected, great managers approach the problem with curiosity and are relentless in their pursuit of the root cause. They watch code reviews and visualize work patterns, spotting bottlenecks or process issues that, when cleared, increase the overall health and capacity of the team. 
* By searching for “why,” they uncover organizational issues and learn how their teams work and how to re how to resolve these
problems in the future.
* 20 patterns is a collection of work patterns we’ve observed in working with hundreds of software teams.

# PART 1 Work patterns exhibited on an individual level

## PATTERN 01 Domain Champion

* The Domain Champion is an expert in a particular area of the codebase. They know nearly everything there is to know about their domain: every class, every method, every algorithm and pattern. 
  * In truth, they probably wrote most of it, and in some cases rewrote the same sections of code multiple times.
  * The Domain Champion isn’t just “the engineer who knows credit card processing”; it’s all they ever work on. It’s their whole day, every day.
  * Some degree of job specialization is essential and often motivating. But even within specialized roles there can be ‘too much of one thing.’ Managers must balance enabling a team member to unilaterally own the expertise, and encouraging breadth of experience.
### How to recognize it 
* Domain Champions will always work in the same area of code. They’ll also rewrite their code over and over, and you’ll see it in churn and legacy refactoring metrics as they perfect it.
* Domain Champions are deeply familiar with one particular domain. As a result, they’ll typically submit their work in small, frequent commits and will show a sustained above average Impact.
* Because no one else knows more than the Domain Champion, there’s usually very little actionable feedback that 
others can provide in the review process. As a result, Domain Champions will typically show low Receptiveness in incorporating feedback from reviews.
* Domain Champions will seldom, if ever, appear blocked. Short-term, it’s a highly productive pattern. But it’s often not sustainable and can lead to stagnation, which of course can lead to attrition.
### What to do 
* Assign tickets that focus on other areas of the codebase.
* Of course, some engineers would prefer to stay where they are. It can be very enjoyable to do a task you’re good at. And, it can be uncomfortable to take on work that requires information or skills you have less practice with. But effective managers will strive to challenge their team.
* Start a new conversation in your next one-on-one:
  1. Acknowledge their expertise and encourage them to share that expertise with others.  Ask them who, if anyone, would beneﬁt from participating in code reviews in the domain to learn best practices. 
  2. Ask them what they like to work on — ﬁrst generally, then speciﬁcally.
  3. Ask them if they are willing to take on a small assignment outside their domain in part to help share the best practices they’ve developed reﬁning the code in their domain.
  Inch the engineer out of their domain using small, low-risk tickets. A little bit of diversiﬁcation can go a long way toward minimizing attrition risk and maximizing best practices.

## PATTERN 02 Hoarding the Code
* This pattern refers to the work behavior of repeatedly working privately and hoarding all work in progress to deliver one giant pull request at the end of the sprint.
* It’s not uncommon for programmers to wait until their work is done to share it. In creative and research-intensive ﬁelds, it can be a natural tendency to avoid sharing work when it’s only just started. 
* There are plenty of reasons why this might be: a fear of having others judge the work in progress, a fear of others taking ideas, or a desire to make the whole process seem effortless, to name a few.
* Whatever the reason, the heart of the problem is this: the more an individual saves up their work, the less they collaborate with others. Working alone is inherently riskier than working with others. And software engineering is a team sport.
* This tendency to work privately and then submit work all at once doesn’t just limit and slow down the individual — it’s damaging to the team’s progress as a whole. Submitting work all at once means that there weren’t any opportunities for collaboration along the way. Even more, once the work was submitted, someone else had to review all of that work. * So naturally, this work behavior can also lead to lower quality code — both from the Submitter’s standpoint (who didn’t check in their work early to get feedback or notice potential missteps), and the Reviewer’s perspective (who likely doesn’t have enough time or energy to adequately review all of that code).
* When you see large and infrequent commits, ﬁrst consider the pattern’s duration (have we seen this pattern for years, or has it only recently been visible?). This information can help determine whether this is the engineer’s preferred way of working, or if this is caused by something outside the normal development process.
### How to recognize it 
* Large and infrequent commits can be a sign that the engineer is working privately until their project is ﬁnished, and then submitting their work all at once.
* This pattern is typically ﬁrst seen in the Work Log report but is also identiﬁable in the team’s Review Workﬂow. These PRs are larger and usually come later in a sprint or project. Because of this, they’ll typically either take a longer time to review (relative to the team’s average) or will get a lower level of review (see Review Coverage).
* It’s also common for these engineers to show lower than average Receptiveness in the Submit Fundamentals. When people work in isolation, only submitting it for review once they’ve decided it’s the ‘right’ solution later in the sprint, it’s generally much more difficult to take feedback on that work objectively.
### What to do 
* Above all else, be compassionate. Odds are, you’ve recognized this pattern right before or just after the end of a sprint, so these engineers are likely tired, stressed, and worn out. Make sure they get the time and space they need to recover from delivering such a big payload.
* This can be great timing for an impromptu and informal 1:1. Going on a walk or getting coffee, for example, can keep the conversation casual. Get them talking about their latest project, ask what went well and what didn’t, and recognize their achievement.
* Along the way, bring up the topic of team collaboration, and how saving work until it’s completed leaves little room for learning from others throughout the process. When teams do work together throughout a project, they can learn from each other’s perspectives, reduce uncertainty and move faster, and even ﬁnd improved solutions to the problem. 
* In practice, that might look like submitting work far before the engineer thinks it’s ready for a review.
 
## PATTERN 03 Unusually High Churn
* Churn is a natural and healthy part of the development process and varies from project to project. However, Unusually High Churn is often an early indicator that a team or a person may be struggling with an assignment.
* In benchmarking the code contribution patterns of over 85,000 software engineers, Pluralsight’s data science team identiﬁed that Code Churn levels frequently run between 13-30% of all code committed (i.e., 70-87% Efficiency), while a typical team can expect to operate in the neighborhood of 25% Code Churn (75% Efficiency).
* Testing, reworking, and exploring various solutions is expected, and these levels will vary between people, types of projects, and stage in the software lifecycle. Given the variance, becoming familiar with your team’s ‘normal’ levels is necessary to identify when something is off.
* Unusually high churn levels aren’t a problem in themselves. More likely, there are outside factors causing the problem.
* An unusually high level of churn can be indicative of one of three behaviors:
 * Perfectionism: When an engineers’ standards of “good enough” are not aligned with the company’s standard of “good enough.” Engineers keep going back into the code to rewrite it because they think it can and should be better but may not add much to the actual functionality of the code.
 * They’re struggling with the problem at hand. This situation manifests differently than with Hoarding the Code (pattern #2), because in this case, the engineer initially thought they had correctly solved the problem, perhaps even sent it off for review, and then discovered it needed to be rewritten. Not just touched up. Rewritten. 
 * Or, most commonly, issues concerning external stakeholders. We see this with unclear or ambiguous specs, late arriving requirements, or mid-sprint updates to the deliverables.
### How to recognize it 
* This pattern is characterized by high levels of churn in the back of the sprint or project. Watch for churn rates that climb signiﬁcantly above the engineer’s historical average (see the Snapshot and Spot Check reports), pairing that information with where they are in a project.
### What to do 
* Churn is normal in lots of situations. Redesigns, prototypes, and POCs are all examples where you would expect to rewrite large chunks of code. So when you notice unusually high churn, take into consideration whether this is routine or something’s off. If it’s the latter:
* Determine whether an external stakeholder is driving the situation. If so (and the engineer has veriﬁed that this is causing the higher levels of churn), then:
 1. Show the data. Show how late arriving specs or last-minute changes are throwing the project off. 
 2. Pull the ticket from the sprint, or decide on an MVP and split off the additions into a reﬁnement sprint.
* If an external stakeholder is not driving the Unusually High Churn, call in the cavalry!
* It is usually preferable to be coached by a fellow engineer or team lead instead of a manager.
 1. Ask for a pre-submit code review or a rubber duck. 
 2. Ask to split the work. The act of dividing the work often reveals the root issue. 
 3. Ask a more senior engineer to assess what “good enough” is in the context of the project.
 4. If the problem is difficult, or if the domain is unfamiliar, bring in another engineer to pair program.
 
## PATTERN 04 Bullseye Commits
* This pattern is relatively common in most teams, but it often goes unrecognized: an engineer understands a problem, breaks down the project into smaller tasks, and submits code that has little room for improvement. 
* Most likely, not all of the commits that make up the project will be Bullseyes. But the ones that are, generally have a small to modest impact and were thoroughly reviewed and approved on the ﬁrst try. Celebrate them!
### How to recognize it 
* In practice, Bullseye Commits can be identiﬁed by when they were submitted in regard to the deadline, their impact, and how they were treated in the review process. Generally, the code was started and completed in advance of the deadline, with negligible churn. The commit’s Impact was small to modest in size and was then thoroughly reviewed. It was approved on the ﬁrst try (see Review Workﬂow).
* It’s the level of thoroughness in the review that distinguishes Bullseye Commits from Rubber Stamping (Pattern #15). In Bullseye Commits,  code reviews are substantive.
### What to do 
* Recognize a clean bullseye in a standup, or a simple note: “I saw that check-in, nice job!” Whether it’s public or private, showing that you noticed and that you care will only reinforce this pattern.
* If there’s an engineer who regularly makes Bullseye Commits, it may be helpful for others to understand how they approach projects. Ask the engineer to do a lunch and learn, or consider asking them to provide feedback on another engineer’s work  in the review process.
 
## 
