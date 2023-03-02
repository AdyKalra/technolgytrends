## Threat Modelling

[TM](https://wiki.owasp.org/index.php/Category:Threat_Modeling)

* We continue to recommend that teams carry out threat modeling — a set of techniques to help you identify and classify potential threats during the development process 
* **Threat modeling is a family of activities for improving security by identifying objectives and vulnerabilities, and then defining countermeasures to prevent, or mitigate the effects of, threats to the system. A threat is a potential or actual undesirable event that may be malicious (such as DoS attack) or incidental (failure of a Storage Device). Threat modeling is a planned activity for identifying and assessing application threats and vulnerabilities.**
* But we want to emphasize that this is not a one-off activity only done at the start of projects; teams need to avoid the [security sandwich.](https://www.thoughtworks.com/radar/techniques/security-sandwich) 
* This is because throughout the lifetime of any software, new threats will emerge and existing ones will continue to evolve thanks to external events and ongoing changes to requirements and architecture. 
* This means that threat modeling needs to be repeated periodically — the frequency of repetition will depend on the circumstances and will need to consider factors such as the cost of running the exercise and the potential risk to the business. 
* When used in conjunction with other techniques, such as establishing cross-functional security requirements to address common risks in the project's technologies and using automated security scanners, threat modeling can be a powerful asset.

* The **“Security Sandwich” approach is hard to integrate into Agile teams, since much of the design happens throughout the process, and it does not leverage the automation opportunities provided by continuous delivery.** 
* Organizations should look at how they can **inject security practices throughout the agile development cycle.** This includes: evaluating the right level of Threat Modeling to do up-front; **when to classify security concerns as their own stories, acceptance criteria, or cross-cutting non-functional requirements; including automatic static and dynamic security testing into your build pipeline; and how to include deeper testing, such as penetration testing, into releases in a continuous delivery model.** 
* In much the same way that DevOps has recast how historically adversarial groups can work together, the same is happening for security and development professionals. (But despite our dislike of the Security Sandwich model, it is much better than not considering security at all, which is sadly still a common circumstance.)

### Threat Modeling Across the Lifecycle
* Threat modeling is best applied continuously throughout a software development project. The process is essentially the same at different levels of abstraction, although the information gets more and more granular throughout the lifecycle. Ideally, a high-level threat model should be defined in the concept or planning phase, and then refined throughout the lifecycle. As more details are added to the system, new attack vectors are created and exposed. The ongoing threat modeling process should examine, diagnose, and address these threats.

* Note that it is a natural part of refining a system for new threats to be exposed. For example, when you select a particular technology -- such as Java for example -- you take on the responsibility to identify the new threats that are created by that choice. Even implementation choices such as using regular expressions for validation introduce potential new threats to deal with.
