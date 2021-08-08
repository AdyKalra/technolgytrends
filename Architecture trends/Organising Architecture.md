### Do we need architects anyway?
Looking at the current technological and organizational paradigm, we can only recognize the world is massively different from 10 or 20 years ago. We live in a world where we can instantly make use of infrastructure via cloud providers. Using common software, functionalities can be purchased and integrated with the click of a button and the availability of a credit card.

Gone are the days of creating large project plans and business cases. No need to negotiate the proposed solution for any given problem with the budget holder. No long debates with other engineers about the envisioned solution. Great for our agility, but it also has consequences. 

Value-stream teams have been given more autonomy and possibilities to select, purchase and integrate hardware and software. Albeit via cloud providers where you can autoscale your infrastructure, or via Software-as-a-Service providers who offer you functionality out of the box. Gone are the days of making well-thought documents who are reviewed and tested by colleagues in the organization.

Clearly this benefits the speed of delivery and flexibility in choosing solutions. Consequently, however, it requires more maturity from a team. The solution proposed and decisions made not only have to fit the context of the team, but as well as the organization. The complexity and pressure to guard consistency and best interest for the organization, as a whole, now relies on the value-stream teams. The tension of choosing between different options and stakeholders now solely falls on the burden of the team.

The architect function is key in getting to conscious decisions that are beneficial for the customers and the organization as a whole. Either by limiting the number of options that are available for a team, or by refining and improving the reasoning and acceptance of trade-offs between proposed solutions.

## Organizing architecture guided by two perspectives

First-of-all, architectural scopes are not to be seen as static elements. Architects should be dynamic, **understanding the purpose of management with the organization and the engineering challenges of the development teams.** Gregor Hohpe describes this as [riding the elevator.](https://architectelevator.com/) 

* One way to determine scope is to look at complexity. The scope of complexity for a value-stream team is different from the complexity of a whole organization.

Inspired by Ruth Malan and Dana Bredemeyer, we can use the model where the architecture function can be organized in two axes: on the vertical axis is the locality of decision-making, and the horizontal axis the complexity and detail of the challenge:  

![scope](https://lh6.googleusercontent.com/MZdXU8X-EWsrOIyxPS8BFzo6Y6E3grcpotphktC7VZGpvk1OKCp6aB3-9_wUZjyzqngVPVdt7UIeSNSgzipMf-ceQgmZp699cR6siJJ2xhjKi0QRkSkaf3f91Y5EpzVxsEhYkTfI)

Let’s start with the axis of complexity. The scope of a team often concerns a limited number of components, microservice or other functionalities. The main objective for the team here is to ensure functionality of the component is above or up to par of customer’s expectations. 

As we move up to domain-oriented units, business lines and enterprises, we see an increase in the complexity. On business-line and enterprise level, for example, the concerns are different from a team. One has to balance the best interest of multiple teams, commercial interests and organizational concerns. Simply put, the world is a bit bigger and increasingly complex.

Decision-making is the other axis to consider, especially the impact of a decision. The decisions made on organizational level typically offer boundaries and guidelines towards the organization. These are meant to bound the options available to the smaller units of the organization and aid in better decision-making for those units in the best interest of that unit and the organization. We can frame as the stewardship increases with the complexity, and the decision-making increases with the locality:

![scopeaxis](https://lh5.googleusercontent.com/jmIOIkXO6lEfrowwLJ_SBW2XAKcXMBcwQee1t0vrTrdEBcQkmJ_Jq2eCYOizN-mAA2rCXW-hCOwHNF7s3Jz6GFG5AuQda0dPcCwdLBXgyUZdVA_GzFaEcFn3CyRL00Fq28qj1tnH)

### What about the architecture role?
As a starter, we see architecture as a function. A function that can be delegated to a day-to-day role, or a function that is attributed to an existing role. This could be a principal engineer or assigned to a group of people, e.g. the product engineering team. A senior engineer or team lead can be appointed as the tie-breaker.

For an organization, it is important to be conscious about the attitude of the architects it hires and puts in charge. The character and way of working of the architect function has a huge impact on the engineering culture. Putting a benevolent dictator in charge has a different impact than an architect that coaches and supports the team in their architecture decisions. 

However, context matters here. An architect for an in-shop product engineering department requires different capabilities and attitudes compared to an architect that has to work with vendors and ensure successful integration. The latter architect needs to be stronger in vendor management and the corresponding negotiation. 
