## The strongest organisations and individuals to study
### 1. Shopify: probably the most complete AI-native engineering example

Shopify has built an internal Slack-based engineering agent called **River**. It operates against the company’s **monorepo**, uses **reproducible development environments** and **written-down engineering skills**, and was reported as co-authoring one in eight merged pull requests. The important story is not the agent itself. Shopify first simplified the engineering substrate through a monorepo, reproducible Nix environments, stronger CI and codified knowledge.

Its workflows demonstrate what genuine SDLC reengineering looks like:

- A developer delegates work through Slack.
- The agent reads repository context and engineering conventions.
- It implements the change in an isolated remote environment.
- It builds, runs tests, interacts with simulators, gathers screenshots and opens a pull request.
- If a test fails, it inspects the logs, modifies the change and retries.
- The engineer reviews evidence and makes the final decision.

#### Shopify has also moved beyond general coding into specific operational flows:

- **Mobile engineering**: multiple agents independently build and test iOS and Android work in parallel.
- **Application migration**: Helix decomposes migration into small checkpoints. Each checkpoint must pass tests, visual comparison, two adversarial reviews and human approval before progressing.
- **Security remediation:** River validates the original vulnerability, updates the patch, requests expert judgment where needed, follows the remediation through merge and rechecks the repository before declaring completion. Shopify reported that the initial dependency workflow reduced its open-issue backlog by about 70% in 11 days.
- **Reusable orchestration:** Roast combines deterministic code execution with constrained AI steps, with workflows represented in YAML and Markdown so they can be version-controlled and tested.

**Leadership lesson:** Shopify is turning organisational knowledge into executable infrastructure. Engineering standards are no longer just documents. They are skills, environments, tests and gates that agents and humans both use.

2. Atlassian: strongest whole-of-SDLC transformation framing

Atlassian describes AI-native development as a shift from synchronous, single-threaded coding to asynchronous, multi-threaded work. As code generation accelerates, planning, design, review, maintenance and collaboration become the new constraints. Its model combines workflow redesign with two foundational investments: enterprise context and measurement.

Its seven-part framing covers:

Context
Measurement
Planning
Design
Development
Review
Maintenance

Leadership lesson: do not optimise coding while leaving every upstream approval and downstream assurance process untouched. That simply moves the queue.

3. Anthropic: strongest stage-by-stage AI SDLC playbook

Anthropic argues that code is no longer the dominant bottleneck. Traditional requirements, estimation, review, security and release gates were designed for a world where implementation consumed weeks or months. When agents produce code faster, those controls become the constraint unless the whole lifecycle is redesigned.

Its six-stage model covers:

Planning
Design
Building
Testing
Deployment
Maintenance

The central design move is to convert documents and handoffs into structured artifacts that agents can consume and independent checks can verify.

Leadership lesson: human control should not mean a human manually touches everything. It should mean humans set intent, define boundaries, own exceptions and retain authority for consequential decisions.

4. GitHub: agentic work embedded in the engineering system

GitHub has moved from IDE assistance to asynchronous engineering agents. Its coding agent can accept an issue, inspect repository context, work in a controlled environment, run tests and return a pull request for review. Human approval, branch protections, restricted permissions and auditability remain part of the flow.

GitHub Agentic Workflows extends this into continuous repository operations:

Issue summarisation, labelling and routing
CI-failure investigation
Documentation maintenance
Code-quality improvement
Security and dependency maintenance
Pull-request creation for human review

GitHub also warns that multi-agent systems behave more like distributed systems than chatbots. Reliable designs require explicit state, typed schemas, constrained interfaces, ordering and validation rather than free-form agent conversations.

Leadership lesson: the scalable asset is not a collection of prompts. It is a governed catalogue of reusable workflows, context contracts, permissions and evaluation mechanisms.

5. IBM: the clearest enterprise HR operating workflow

IBM AskHR provides a strong example of AI moving from answering questions to completing work. IBM says AskHR automates more than 80 HR tasks and handles more than 2.1 million employee conversations annually. It uses a two-tier model in which AI handles routine requests while human advisers manage more complex needs. The platform integrates with systems including Workday, SAP and Concur.

Example workflow:

Employee or manager intent → policy/context lookup → personalised response → backend transaction → confirmation → human escalation for complexity

This reportedly supports activities such as:

Policy and payroll questions
Employment verification letters
Vacation requests
Employee transfers
Organisational structure updates

Before automating, IBM applied an “eliminate, simplify, automate” principle so it did not merely digitise inefficient processes.

Leadership lesson: one intelligent front door is more powerful than dozens of disconnected assistants. But the front door must be able to complete transactions across systems, not simply provide advice.

6. Unilever: a useful recruitment case, with important caution

The documented Unilever model reorganised early-career recruitment into a digital sequence:

Application → gamified assessment → technology-assisted video assessment → human-led final assessment

The Case Centre reports a 75% reduction in recruitment time, increased diversity and savings exceeding £1 million from this transformation.

The transferable idea is not “let AI choose people.” It is:

Automate high-volume administration.
Standardise evidence collection.
Move recruiters toward relationship-building and final judgment.
Retain human accountability for employment decisions.
Continuously test assessments for validity, accessibility, adverse impact and privacy.

This last point is essential. AI-assisted hiring is materially higher-risk than code generation because it directly affects people’s opportunities. The system should support structured evidence and administration, not make opaque final decisions.

7. Bain & Company: strongest leadership and org-model thesis

Bain & Company argues that AI breaks the traditional link between headcount and output. As execution becomes cheaper and more scalable, judgment becomes the scarce resource. It describes org charts shifting toward “accountability charts,” with leadership focusing on outcomes rather than supervising activity.

It highlights three areas that must change together:

Structure, teams and accountabilities
Talent engine and roles
Leadership and culture

Leadership lesson: if AI expands execution capacity but every decision still climbs five management layers, the organisation has accelerated the wrong side of the system.

8. PwC: strongest description of the AI-era HR operating model

PwC describes three increasingly mature modes:

HR with AI: practitioners use AI assistance.
HR through AI: workflows are redesigned around AI.
HR by AI: routine execution becomes increasingly autonomous, while people retain judgment and accountability.

Its Australian operating-model view proposes that agentic automation shifts human work toward exception handling, oversight and continuous improvement. It also anticipates wider spans of control, fewer transactional layers and management attention moving from throughput to system performance.

Leadership lesson: managers will increasingly manage an outcome system comprising people, workflows, agents and controls, rather than simply allocating tasks to employees.
