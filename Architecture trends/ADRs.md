## ADRs at GitHub

* **Architecture decision records**, also known as ADRs, are a great way to document how and why a decision was reached within a codebase. We’ve started to adopt them within the mobile team here at GitHub, documenting decisions that affect the iOS codebase and Android codebase, as well as decisions that affect both mobile clients.

* ADRs are not the most common within open source codebases, but have gained more popularity since ~2017 within long-lived, “evolutionary” codebases like those in more enterprise-y settings.

* So why write an ADR? Why spend time documenting something when a decision has already been made?

### They’re not for you, they’re for future you
* ADRs are not meant to be a self-discovery, reflection process on what you decided. ADRs will help you 6-12 months from now recall what your mindset was when you decided upon that architecture.

* ADRs **capture the decision at the time it’s being made.** ADRs are the culmination of all those minutes and hours you spent in meetings, on Zoom, in Slack, or jamming through various proof-of-concepts in Xcode. All of the context that’s in your head has a chance to get out into words so that when you’re revisiting the architecture down the road, you can put that context right back into your head.

* The real bonus comes when someone git blames you some months from now and asks you how the GitHubAPIClient module works. Better than setting up a 30-minute pairing call to walk them through the code, you can now link to the ADR you wrote to explain some more about the decisions made while building the GitHubAPIClient module.

### They’re not for you, they’re for your peers
* ADRs force you to write more than a one-liner “this ships the feature for #3128”. They are a longer form of prose to help your teammates understand why the feature is built the way it is, and not built some other way (see: “Alternatives Considered” and “Pros/Cons” within ADRs themselves).

* Something that may be simple for you might be complicated for your teammates. Taking the time to write down what your thought process was as you made decisions gives your teammates the chance to get inside your head. Writing ADRs allows for “decision socialization”, where your team comes to a decision that the team is responsible for maintaining, rather than decisions made in isolation.

* By expanding upon what you write in your pull request titles and descriptions (and you are still writing quality pull request descriptions, right?), you give your teammates more information about how a patch or diff works in a larger system.

* Better yet, by writing an ADR ahead of putting your pull requests up, you’ll get better pull request reviews from the team reviewing it. No longer do you need to explain how line 387 in APIClient+Caching.swift will affect data fetching and caching architecture, because your teammates already understand how you’re changing the system from the ADR you wrote about “Adding cache support to E-Tag entities”.

### They’re not for you, they’re for your future peers
* ADRs are not meant you to show off how smart you are or for folks to fawn over the architecture you built. ADRs are for helping onboard new teammates as they work to understand the codebase and how it has evolved over time.

* As teams scale and grow, the number of lines of communication between teammates increases. A team of three individuals only has three lines of communication (A <> B, A <> C, B <> C). A team of four has six (A <> B, A <> C, A <> D, B <> C, B <> D, C <> D). Wanna do the math for a team of five or six? How about 14 engineers, two designers, two PMs, and three EMs?

* Writing down decisions made helps communicate to your current teammates, but also those who join your team as it scales and grows. By informing your team how and why a decision was made in an asynchronous fashion, you no longer need to “hop on a Zoom call” to onboard each new teammate on a per-architectural-decision basis.

* In the best-case scenario, you’ll have your teammates writing new ADRs for you, superseding the decisions past you made, so that you can learn from your teammates in the future.

### Write more ADRs
* I hope this has convinced you to document the decisions that you’re making as we build software that (hopefully) millions of folks use! As our team grows larger and our codebases grow more entangled and intertwined, architecture decision records are a great way to help future us, our current teammates, and future teammates.


More Info
* [architecture_decision_record](https://github.com/joelparkerhenderson/architecture_decision_record)
* [earn-maintainers-esteem-with-adrs](https://understandlegacycode.com/blog/earn-maintainers-esteem-with-adrs/)
* [Architecture Decisions:Demystifying Architecture](https://personal.utdallas.edu/~chung/SA/zz-Impreso-architecture_decisions-tyree-05.pdf)

[Source](https://github.blog/2020-08-13-why-write-adrs/)
