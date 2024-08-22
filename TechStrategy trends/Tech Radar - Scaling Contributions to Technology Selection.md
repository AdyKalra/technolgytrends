## Scaling Contributions to Technology Selection via Tech Radar

[zalando](https://engineering.zalando.com/posts/2021/06/zalando-tech-radar-scaling-contributions.html)

### Scaling contributions
- One of the challenges for us to solve was scaling contributions to the Tech Radar across our 250+ delivery teams. Technologists are often more excited in promoting a new, promising technology than working on guidelines or sharing knowledge about already well-known tech. Such individuals are also essential for continued innovation. On the other hand, companies look for organizational efficiency by ensuring talent mobility across teams supported by a more or less standardized tech stack. **This makes it easier to address cross-team dependencies in product delivery by allowing teams to contribute to code bases beyond their area of responsibility.** Further, it creates career opportunities for Engineers, who can quickly switch teams and work on a challenging, high impact project. **Thus, for technology selection, there is a natural tension between early adopters' vested interest and the needs of the organization they work for.** 

- At Zalando, we have created a two-sided contribution model to the Tech Radar: 
  - Anyone in Zalando is encouraged to contribute knowledge about technologies we have on the Tech Radar or suggest ones that are promising to evaluate and play a key role in this process.
  - **Our Principal Engineers are maintainers of the Tech Radar and are moderating information collection on incoming suggestions**, driving creation of good practices for technologies being evaluated or used, and for promoting technologies to increase their adoption.
- Ring change suggestions are supported by issue templates in our internal Tech Radar GitHub repository. These templates provide guidance on common questions around use case fit, key differences from alternatives already on the Tech Radar, conformance to our Technology Selection Principles, and support within the Engineering Community.
- We encourage and expect our Engineers to contribute information about usage, lessons learned from production incidents, or challenges they face at scale. Voluntary contributions alone are insufficient to keep an updated view of the technologies we use. Thus, to support usage information collection, we collect usage data from our AWS accounts, source code repositories, or our infrastructure platform offerings. Collected information is collected in a documentation page with a common structure across all entries:
- **Finally, we leverage Principal Engineers to moderate and drive discussions around technology adoption at Zalando. These colleagues have a sufficiently broad view on technology usage and performance in production across multiple teams and serve as a multiplying factor. They're responsible for encouraging teams they work with to share knowledge and highlight technology usage based on the software systems in their areas - either themselves or by enabling others to do so. Additionally, they moderate discussions within technology guilds or initiate working groups to create specific artifacts for the technologies, like collections of good practices or guidelines tailored to our environment, use cases, and scale. Such working groups are also excellent opportunities to develop or identify talent within the company.**

### Re-scoring - how have we decided upon changes?

- After a longer period of time with no regular changes to the Tech Radar, we had a re-scoring exercise to complete. A similar approach was used originally at ThoughtWorks and can be used to create a Tech Radar from the ground up.

- **Within our Principal Engineering Community, we formed a working group per dimension: Datastores, Data processing, Infrastructure, and Queues. Our Tech Radar visualization merges Data processing and Queues in a single Data Management dimension for simplicity. Each working group was responsible for the data collection and analysis. One person from each group compiled the information in a structured format where per technology there was a case made for a ring change (or not). The change reasoning was supported by data points on usage, incidents, and expertise we gained since the technology was added to the Tech Radar (a few years in some cases) as well as conformance with our Technology Selection Principles. Where necessary to build a solid case, we reached out to teams in order to understand more details about their use cases or experience, if this was not sufficiently documented through recent information in our Tech Radar.**

- Based on the collected data, Principal Engineers participated in a review and re-scoring exercise. In a spreadsheet, we collected votes. Every 'nay' vote required a short rationale which we later discussed in the group to ensure we did not miss out on usage or use cases. We also found inconsistencies in the way we handle technologies with multiple deployment options (self-hosted vs. managed or vendor offerings), for which we did not find a good solution yet.

- After the voting, the collected ring changes were discussed with our Senior Leadership Team. The main focus was on ensuring long-term support for the technologies we promote to ADOPT and that technologies on lower rings are in line with long-term strategies (e.g. Data Strategy).

- Finally, the changes were shared with our Engineers where we shared detailed rationale per ring change and further information on the re-scoring process and contributions moving forward.

### Notable changes
With the re-scoring, we moved a few technologies to ADOPT, confirming our investment in these. To scale adoption, in some cases, we formed dedicated teams that operate service offerings available to all Zalando Engineers and Data Scientists.

### Tech Radar changes moving forward and future focus
The re-scoring exercise described in this post was a house-keeping exercise supported by clarifying the purpose of the Tech Radar, long-term ownership, and the contribution model. The amount of upcoming changes will of course depend on contributions from our Engineering Community and our appetite for trying out new technologies. While changes to ADOPT/HOLD are going to be evaluated on a quarterly basis, we have a steady stream of ongoing assessments and trials.

[How to use a Radar within the org/personal use](https://www.youtube.com/watch?v=w_u8mQpTuhc)

- The Principal Engineering Community focuses on:
  - supporting and guiding contributions from the Engineering Community,
  - identifying promising technologies to invest in,
  - collecting best practices and expertise around technologies on TRIAL and ADOPT.

