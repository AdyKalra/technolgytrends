Results from a structured Copilot experiment show users completed tasks 40% faster and found "hard" tasks less difficult. Metrics included the average time spent on tasks and developers’ self-reported difficulty of those tasks. 
[Source](https://newsletter.getdx.com/p/impact-of-copilot-at-anz-bank)

**Summary**
To evaluate whether Copilot should be used org-wide, the authors of this paper conducted an experiment for six weeks, and compared the tool’s impact on a test group versus a control group. They based their evaluation of the tool’s impact using measures for productivity, quality, and security. 

**Experiment design**
The experiment included two weeks of preparation and four weeks of actual testing. Here’s how the experiment was designed:

- Prior to starting the experiment, risks related to intellectual property, data security, and privacy were assessed in conjunction with ANZ’s legal and security teams to arrive at a set of guidelines.
- The experiment started with by getting a baseline on productivity, quality, and security measures.
- About 100 engineers participated. Participants were randomly divided into either a control group, where the Copilot extension was disabled, or a Copilot group. These groups were reversed in week 3.
- Each week, participants were required to solve six algorithmic coding challenges.
- All engineers were asked to use only Python to code, for uniformity in assessing code quality and interpretation of code correctness, ensuring rigor in statistical evaluation.
- Upon completing each task, participants would upload their solutions to their repositories and complete a survey. 

**ANZ’s experiment team paid attention to the following metrics:** 

- They measure “productivity” as the total time spent solving a problem (in minutes, self-reported)
- “Quality” was determined by measuring the unit test success ratio, number of bugs, and code smells
- “Code Security” was measured with the number of vulnerabilities

This data was collected from Copilot, surveys, and static code analysis, and the solutions submitted by participants were manually graded by the ANZ Copilot Experiment Team according to how well they completed the assigned tasks.

The experiment demonstrated that Copilot significantly reduced the time engineers take to complete tasks and positively influenced their ability to perform specific functions. However, the research team found no statistically significant improvements in code quality or security as a result of using the tool.

H**ere’s a closer look at the results:**

**Impact on speed**
Throughout the experiment, participants recorded the time they took to complete each challenge. This data allowed the research team to calculate and compare the average time spent on tasks by both the Copilot group and the control group.

The findings were notable: the group using Copilot completed their tasks 42.36% faster than the control group. Specifically, the control group took an average of 30.98 minutes per task, while the Copilot group averaged 17.86 minutes.


When we look closer at the impact for engineers with different levels of Python proficiency, we can see that Copilot was beneficial for participants of all skill levels, but it was most helpful for those who were ‘Expert’ python programmers. 


- This is intriguing because it conflicts with a GitHub study which found that developers with less programming experience benefited the most from Copilot. The GitHub study also measured task completion time but did not restrict participants to a specific programming language, unlike the ANZ study. It’s possible that the ‘expert’ python programmers at ANZ were more effective at using Copilot, however this is not certain. 

Participants also reported the difficulty of each task. We can see that Copilot gave the largest improvement when completing ‘Hard’ tasks. This observation makes sense: harder tasks have more opportunities where AI-assisted tools can help. 


As for measures of quality and security, the Copilot group had a 12.86% higher unit test success ratio, however this result was not statistically significant. The experiment was also unable to generate meaningful data to measure code security—however, the data suggests that Copilot did not introduce any major security issues into the code. 

**Impact on developer experience**
Across all areas, engineers responded positively regarding GitHub Copilot. They felt it helped them review and understand existing code, create documentation, and test their code. Additionally, they felt Copilot helped them spend less time debugging and reduced their overall development time. They also found the suggestions provided by Copilot to be somewhat helpful and generally in line with their project’s coding standards. It should be noted, however, that while sentiment was positive, it was moderate. 


Ultimately, the experiment provided clear results about Copilot’s impact on the speed and ease of completing tasks in engineering. The authors recommended its wider adoption, and by the time the paper was published, over 1,000 users had already integrated Copilot into their workflows.

**Final thoughts**
While the findings from this study are interesting, I’m mostly inspired by how the organization approached its adoption of Copilot. In its simplest form, they established a baseline, ran an A/B test, and selected a range of metrics to assess the tool’s impact. It’s a great example for organizations looking to evaluate the effectiveness of a tool and determine whether it should be adopted on a larger scale. 
