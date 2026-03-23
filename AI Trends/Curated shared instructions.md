
- For teams actively using AI in software delivery, the next step is moving beyond individual prompting toward **curated instructions for software teams**.
- This practice helps you apply AI effectively across all delivery tasks — not just coding — by sharing proven, high-quality instructions. The most straightforward way to implement this is by committing instruction files, such as an AGENTS.md, directly to your project repository.
- Most AI-coding tools — including Cursor, Windsurf and Claude Code — support sharing instructions through custom slash commands or workflows. For noncoding tasks, you can set up organization-wide prompt libraries ready to use. This systematic approach allows for continuous improvement: As soon as a prompt is refined, the entire team benefits, ensuring consistent access to the best AI instructions.

- [AGENTS.md](https://agents.md/) is a common format for providing instructions to AI coding agents working on a project. Essentially a README file for agents, it has no required fields or formatting other than Markdown, relying on the ability of LLM-based coding agents to interpret human-written, human-readable guidance. Typical uses include tips on using tools in the coding environment, testing instructions and preferred practices for managing commits. While AI tools support various methods for context engineering, the value of AGENTS.md lies in creating a simple convention for a file that acts as a starting point.

### Cover what matters
Add sections that help an agent work effectively with your project. Popular choices:

- Project overview
- Build and test commands
- Code style guidelines
- Testing instructions
- Security considerations
- Commit messages or pull request guidelines, security gotchas, large datasets, deployment steps: anything you’d tell a new teammate belongs here too.

**Large monorepo? Use nested AGENTS.md files for subprojects**
- Place another AGENTS.md inside each package. Agents automatically read the nearest file in the directory tree, so the closest one takes precedence and every subproject can ship tailored instructions. For example, at time of writing the main OpenAI repo has 88 AGENTS.md files.


**Context engineering** is the systematic design and optimization of the information provided to a large language model during inference to reliably produce the desired output. It involves structuring, selecting and sequencing contextual elements — such as prompts, retrieved data, memory, instructions and environmental signals — so the model’s internal layers operate in an optimal state. Unlike prompt engineering, which focuses only on the wording of prompts, context engineering considers the entire configuration of context: how relevant knowledge, instructions and prior context are organized and delivered to achieve the most effective results.

Today, engineers use a range of discrete techniques that can be grouped into three areas: Context setup covers curation tactics such as using minimal system prompts, canonical few-shot examples and token-efficient tools for decisive action. Context management for long-horizon tasks addresses finite context windows through context summarization , structured note-taking to persist external memories and sub-agent architectures to isolate and summarize complex sub-tasks. Dynamic information retrieval relies on just-in-time (JIT) context retrieval, where agents autonomously load external data only when immediately relevant, maximizing efficiency and precision.
