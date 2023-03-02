## Threat Modelling

* We continue to recommend that teams carry out threat modeling — a set of techniques to help you identify and classify potential threats during the development process 
* But we want to emphasize that this is not a one-off activity only done at the start of projects; teams need to avoid the [security sandwich.](https://www.thoughtworks.com/radar/techniques/security-sandwich) 
* This is because throughout the lifetime of any software, new threats will emerge and existing ones will continue to evolve thanks to external events and ongoing changes to requirements and architecture. 
* This means that threat modeling needs to be repeated periodically — the frequency of repetition will depend on the circumstances and will need to consider factors such as the cost of running the exercise and the potential risk to the business. 
* When used in conjunction with other techniques, such as establishing cross-functional security requirements to address common risks in the project's technologies and using automated security scanners, threat modeling can be a powerful asset.

* The **“Security Sandwich” approach is hard to integrate into Agile teams, since much of the design happens throughout the process, and it does not leverage the automation opportunities provided by continuous delivery.** 
* Organizations should look at how they can **inject security practices throughout the agile development cycle.** This includes: evaluating the right level of Threat Modeling to do up-front; **when to classify security concerns as their own stories, acceptance criteria, or cross-cutting non-functional requirements; including automatic static and dynamic security testing into your build pipeline; and how to include deeper testing, such as penetration testing, into releases in a continuous delivery model.** 
* In much the same way that DevOps has recast how historically adversarial groups can work together, the same is happening for security and development professionals. (But despite our dislike of the Security Sandwich model, it is much better than not considering security at all, which is sadly still a common circumstance.)
