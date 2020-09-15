* Developing things “-as-code” allows for engineering to move as quickly as possible. The same goes with feature flags / toggles.

## 𝗙𝗹𝗮𝗴𝘀-𝗮𝘀-𝗰𝗼𝗱𝗲 🏁 is no different 
– it can be one of those application configurations. By creating and provisioning feature flags as pieces of code in a config file you gain all the benefits of Infrastructure-as-Code, Configuration-as-Code, and the entire movement.

![𝗙𝗹𝗮𝗴𝘀-𝗮𝘀-𝗰𝗼𝗱𝗲](https://media-exp1.licdn.com/dms/image/C5622AQGTLdeslrlzPw/feedshare-shrink_1280/0?e=1603324800&v=beta&t=_u75f8lnj-CKRTtPmx_OQyoO5msF2j45XztD2ODlvqc)

### Benefits of Flags-as-Code
#### Maximim Visibility
* Flags-as-code allows everyone in your engineering organization to see changes made to configurations and flags in the Git Repository of choice – giving the entire team insight into feature flags strewn about inside code.

#### Accountable Traceability
* Because Flags-as-Code is traced through a versioning system like git, you can see who made changes to your feature flags at precisely what time. When organizations have hundreds of flags across many developers – traceability becomes paramount to decrease mix-ups and increase safety during rollbacks.

#### Standard Automation
* Checking in your Flags-as-Code alongside your application code and config files allows you to run automated tests against it in your pipeline like you would any other piece of code. This allows you to push fewer bugs and errors to users, especially as your feature flag use scales.

#### Easier Pipeline Promotion
* Flags-as-Code works really well with multiple environments, allowing you to easily promote builds between different staging and development servers without losing where you stand on feature flags.

## Managing feature toggles in teams

* Feature toggles, specifically release toggles, promise to address this, allowing us to hide unfinished features from users by toggling them off, removing barriers to deployment and enabling Continuous Delivery. While they’re integral to many teams' CD approaches, feature toggles come with associated costs: added complexity in the code and the overhead in the workflow for adding and removing them.

#### Feature toggles should be flippable
* There are many light- and heavyweight approaches to implementing feature toggles. Some store values in a database table and offer a UI to flip them; others just put them into environment variables. Whatever approach you choose, it should always be a matter of seconds to flip your toggles. Toggles hard-coded in an application’s configuration aren’t very valuable, as it may take a whole tour through the pipeline to flip them.

* If toggles can be flipped in different environments, this can enable product owners and stakeholders to easily demo and explore new features before they’re made visible to users in production.

#### Feature toggles should be used by default
* One of the key problems with feature toggles is when they are simply not used. This may be because the decision of adding a toggle isn’t discussed when kicking off a story or toggles are only added if there’s an explicit argument being made in favor of this particular toggle. Toggles should however be the default for every story. The only cases where toggles shouldn’t be created are for very minor issues — like small bugs or UI fixes. You should aim to reach a convention within your team on when toggles are necessary, taking into account your team’s structure and needs.

* The first step for every story could be to create the toggle, even if it’s not hiding anything at that point in time. The second step could then be to flip it on in any non-live environment and off in the production environment. This way, changes impacting or colliding with other features under development are noticed early on but cause no problems in the live environment.

* Toggles in non-live environments should only be flipped off if they’re causing major issues that risk or slow down other development or if the feature behind the toggle is being demonstrated. The toggle in the live environment is only flipped on once the story has been signed off successfully.

* Monitoring the state of toggles can help build another layer to detect potential problems. Toggles that aren’t enabled on every non-live environment or that are enabled on live, should be acknowledged. The first case needs to be checked for bigger problems, the latter toggles can probably be removed.

* When feature toggles are used consistently for every story, they provide an additional, quick visualization of the feature-development status in the team.

#### Feature toggles should be added per story
* Stick to the rule to have one toggle per story and not reuse toggles. Failure to do so might lead to catastrophic failures. Even without considering huge disasters, per story feature toggles give you and your team many advantages in the development.

* Example: Two stories are being worked on that enable ‘sort by date’ and ‘sort by price’ respectively. At first glance, it might feel intuitive to create one toggle for sorting and hide their feature behind it. However, if one of the stories is done but the other one is more complex and still needs time, the toggle is now hiding the feature of the finished story. If this toggle was enabled on live, it might leak the unfinished feature.

![Feature Toggles](https://insights-images.thoughtworks.com/Managing20Feature20Toggles20in20Teams_0_870d403ca1b6dc30e912f0be88c47557.png)

* Simple, per story feature toggles enable one of the key benefits of using toggles: independent development and deployment. Furthermore, the simpler a feature toggle is, the easier it becomes to clean it up once it is no longer needed.

#### Feature toggles should be visible
* A problem can be that team members picking up a new story aren’t aware of existing feature toggles. By simply adding a note to the corresponding story card with the name of the toggle, toggles gain visibility and all team members know which toggles they need to flip in case a feature should be turned on or off for a given situation.

![visible](https://insights-images.thoughtworks.com/Managing20Feature20Toggles20in20Teams2028129_33bce9292f1f65740b44c66366500ccc.png)

Feature toggles can be considered deliberate tech debt, so making this debt visible is the first step towards managing it.

Visible feature toggles enable team awareness about the amount of features currently in progress.

#### Feature toggles should be short-lived
* As with toggle creation, the decision of when to remove toggles should be a team-wide convention. In past projects, we’ve seen the removal of toggles being tracked with ‘remove toggle X’ story cards that were put in ‘ready for development’ once a story with a toggle was signed off. Experience showed that these cards would rarely be prioritized and toggles remained in the codebase much longer than they should, slowing future development as developers worked around them.

* Using a ‘work In progress’ limit is a common practice to improve the throughput of development teams. In addition, or even as a replacement, a ‘toggles in existence’ limit can be introduced, which forces the team to remove old toggles before a new one is created. This builds on the visibility of toggles to make this tech debt visible and push the team to actively manage it.

* Furthermore, once a story is signed off, it can be moved to a ‘toggled on’ column instead of ‘done’, which it only leaves when its toggle is deleted. This helps emphasize that a feature isn’t truly ’done’ until we’ve cleaned up the tech debt we created along the way. We can also attach an ‘expiry date’ to the toggle, allowing us to observe the feature ‘in the wild’ before we remove the toggle. The timing should be quite short, but a period of observation can help build confidence in new features.

![shortlived](https://insights-images.thoughtworks.com/Managing20Feature20Toggles20in20Teams2028229_7f537fedaef684e6dde3c0af1839df66.png)

* Keeping feature toggles short-lived reduces the technical debt that might pile up otherwise.

#### Feature toggles should be tested
* One challenge when working with feature toggles is testing. While a toggle exists, we need to maintain tests for both the old and the new functionality, which can mean duplicated code and confusion for developers who need to clean up those tests when removing the toggle.

O* ne strategy to avoid this confusion is to enable the feature toggle by default for all tests when adding a new feature. In practice this meant that when an old test failed, we copied the test — we kept the original one but switched off the toggle there and marked it as a legacy test; the copy, we either adjusted for the new expected behavior or decided while developing, that it became unnecessary.

* When cleaning up the toggle, we would remove all legacy tests, so those that were setting the toggle to inactive for their test scenario. This way, after cleaning up, only tests using the new feature or tests unaffected by the new feature would remain.

* Writing and updating tests in this way enables an easy clean-up of feature toggles such that they can be removed quickly and without needing to have much context.

[Source](https://www.thoughtworks.com/insights/blog/managing-feature-toggles-teams?utm_campaign=ping&utm_medium=email&utm_source=marketo)
