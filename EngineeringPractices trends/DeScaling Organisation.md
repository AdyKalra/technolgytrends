## How to De-Scale your Organization

[De-Scale](https://www.linkedin.com/pulse/how-de-scale-your-organization-peter-merel/)

### Maximum Meeting Size (MMS), Minimum Feedback Frequency (MFF) and Delegation/Collaboration Ratio (DCR).
- MMS is the largest number of people you need to put in a room to get any decision made across your organization.
- MFF is the longest any decision stands unreviewed in your organization.
- DCR is the ratio between the average number of people the organization delegates decisions to vs. the number of people who collaborate on making decisions face-to-face.

**Scaling is an anti-pattern. Big meetings, long loops, slow cadence, tight coupling, and deep hierarchies represent bottlenecks no matter how Agile an individual team may be. De-scaling refactors your organization into self-managing streams of self-organizing teams working together like pods of dolphins.**

- How can human organizations de-scale? How do we balance the autonomy of teams against alignment to business realities? This post is about metrics and practice patterns for de-scaling based on a uniquely successful historical precedent, the Iroquois Confederacy, which sustained a de-scaled society of hundreds of thousands for over five centuries. And the Spotify tribal model, and Steve Jobs' NeXT/Apple DRIs. And Goldratt's Theory of Constraints ...

### Three De-Scaling Metrics
- “Tell me how you measure me and I will tell you how I will behave.” – Eli Goldratt
We can't optimise what we don't measure. If agile organisations offer more flexible structures, it's possible for these structures to be even less efficient than the hierarchies they replace. But if we quantify the dimensions of de-scaling we can use the numbers to understand how to keep these forms of organization efficient.

1. Ceremony Size Limit
Big teams are inherently inefficient. Productivity and trust are best served by teams of just six people because that number balances efficiency of communication against opportunities for collaboration.
To be effective, such tiny teams must continuously coordinate on common challenges and learnings. Agile ceremonies can do this for teams just as they do for individuals within a team. So a first de-scaling metric is the maximum size of any ceremony at any level of organization. Let's call it the Ceremony Size Limit ("CSL").
2. Collaboration Loop Limit
"80% of Agile is efficient collaboration. The rest is book-keeping." – Ward Cunningham
What's the maximum number of conversations that have to happen for any two individuals to collaborate? One reason Agile squads have proven more productive than traditionally managed teams is reducing length of collaboration loops from four (worker 1 -> manager -> worker 2 -> manager -> worker 1) to just one (worker 1 <-> worker 2). As organizations become more complex, every extra level of middle-management adds another four conversations to the length of the loops.
We call the length of the longest collaboration loop in an organization its Collaboration Loop Limit ("CLL"). Big CLLs generate bureaucracy. No matter how you form your organisation, there's a natural tension between CSL and CLL. The alternative is for teams to represent themselves directly in face to face meetings, but that must be balanced against a third metric.
3. Feedback Frequency Limit
"Positive feedback will cause any system to oscillate out of control." – Robert Heinlein
Agile teams optimise flow by chopping everything into tiny pieces. Tiny plans, tiny meetings, tiny requirements, tests, sign-offs and retrospectives. Making these things tiny enables teams to review and refactor them in tiny ceremonies, boosting productivity through continuous negative feedback. The less continuous, the more oscillation - what the folk at Toyota call Mura, which we can translate as "wobble".

### Directly Responsible Individuals
You have to be run by ideas, not by hierarchy – Steve Jobs
Under Jobs, every meeting in Apple was required to identify its Directly Responsible Individuals – or DRIs. Each meeting agenda attached individuals to agenda items, not to roles in a RACI. Membership in Apple meetings was kept to the bare minimum with all meetings encouraged to throw out their least essential member. By the few published accounts, Jobs' Apple maintained a CLL of 2-4, a CSL of 8-10 and FFL of just a week. A rare exception to CSL was Jobs' Top-100.]
The flattened organization of Apple was designed to respond to its CEO like a sports-car to its driver. With Jobs at the wheel it repeatedly lapped entire industries, even obsoleting its own product lines. Under the more cautious Cook, as under Sculley before him, Apple's innovation rate, quality of service, and market cap have slowed entropically. The company retains a vast store of brains and capital but it was never designed to drive itself.

Tribal organizations are designed to do this of necessity. When agile people think about tribes the first word out of their mouths is "Spotify". But in fact there is a very extensive proof of concept for decentralised, tribal organizations that extends far beyond the Spotify model.

### De-Scaling By Numbers
Streams focus on flow of value to market. Squads on workflow. Portfolios on flow of learnings. As workflow multiplies value flow, learning-flow multiplies workflow. XSCALE's "Triple Loop Learning" principle

Spotify Chapters are accepted wisdom in most progressive Agile cultures because they help learnings flow faster than the old Scrum of Scrums practice. They lack an ability to make decisions, but that's where Iroquois Councils and Treaties shine. Product Squads form a council of representatives of their stream's feature delivery squads. And a Portfolio Squad responsible for coordinating releasing and resourcing across streams is formed of a council of reps of the portfolio's product squads' chapters.

The words "stream" and "portfolio" are intentionally evocative of SAFe. This is to suggest de-scaling as the continuous alternative to the centralised SAFe Big Room Planning. But structuring to optimise de-scaling metrics is critical to this. There may be better structures to do so but XSCALE suggests a simple model to start with.

Squads often involve more than one member of the same chapter. For example it's commonplace for a feature delivery squad to involve more than one of the same kind of developer. Assuming 6-person squads, to avoid chapters generating a CSL greater than 6 will mean no more than three feature delivery squads per value stream.
![descale](https://media-exp1.licdn.com/dms/image/C4E12AQGtH_RW_dixTQ/article-inline_image-shrink_1000_1488/0/1520192004703?e=1638403200&v=beta&t=HfbC5DXo__gEm4qkKCCR4p3ghPFPDtSlIDcFrbVnbM8)

At a portfolio level, Jobs pre-saged the Dunbar-limit in his original Macintosh team, which he restricted to 100 members. If the team found it necessary to hire one person more than a hundred, Jobs would remove someone else from the team.

DevOps "second way" requires overlap of membership between systems and product squads per stream. If the number of extra staff for these two runs to, say, six per stream the systems and product chapters can meet across all streams in the portfolio and still fit under CSL 6 / CLL 4. A maximum size of a portfolio of 6 x 4 x 4 = 96 souls is too close to Dunbar limits given there must also be relationships outside a portfolio. So when such a portfolio gets close to four right-sized value streams, it would generally split into two with two streams each.
