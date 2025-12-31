# Avoiding LLM Drift When Using AI Coding Assitants

The way we code with AI assistants has evolved with the rise of agentic coding. Direct instructions now beat meta ones and using multiple lean instructions helps avoid LLM drift (this means when AI stops listening to you). However, you still need a controlled way to provide context and maintain a shared state across sessions.

I used to rely on a bunch of separate files like `BRD.md` (Business Requirements Document), `PRD.md` (Product Requirements Document), `PLANNING.md` (Architecture and additional meta instructions), and `TASKS.md`. But this feels too "waterfally," even for AI, which seems to lean heavily on Agile principles. Jokes aside, coding agents perform better when instructions explicitly cover:

* Problem statement, target users & JTBD (Jobs to Be Done), scope vs non-scope
* Acceptance criteria (what “done” means)
* Constraints (latency, cost, privacy, deployment)
* “Golden flows” and edge cases
* Evals and testing (how we know it works, commands, metrics, fixtures)
* Explicit out-of-scope items

The key shift is that `BRD.md` and `PRD.md` are documents **you** fill out, not artifacts you ask the AI to generate (though you can use AI to enhance them).

Consequently, `PLANNING.md` is gone. I only keep the BRD and PRD as pre-work. Then, I generate the `AGENTS.md` file (small, concise, and distributed in folders) from the PRD if the project is new; otherwise I have it read the entire codebase. The `AGENTS.md` (https://agents.md/) project is an attempt to standardize meta-instructions across different AI assistants. I also use `TASKS.md` to track progress with bullet points to tick off by the AI.

Last but not least, a critical aspect of assistant coding is the integration of testing frameworks and security audits. This involves a combination of standard tools (e.g., pytest for Python, integrated via instructions in your AGENTS.md) and MCP security agents such as Sonar (https://www.sonarsource.com/).

## How to Use These

In the coding assistant of your preference, do the following. Consider that if you have an existing project just jump to step 3.

**Step 1:** Copy BRD template, fill it out yourself in 10 minutes. This forces you to clarify your own thinking.

**Step 2:** Copy PRD template, fill it out. Be specific on the features table, this becomes your actual spec.

**Step 3:** Generate AGENTS.md and TASKS.md
```
* Generate AGENTS.md file(s) based on the guide found on this file: generate-agents.md

* Create a TASKS.md file with bullet points tasks divided into milestones for building this app.
```

**Step 4:** Start Implementation
```
Based on my AGENTS.md and TASKS.md proceed with building the tasks and ticking them off once they are done
```

When working with a coding assistant, mention or paste the relevant section directly into context. Give it the content.


**Example prompt to start implementation:**
```
Here is my root AGENTS.md: [paste or mention AGENTS.md]

Let's build the MVP. Start with the first tasks. 
I want to see:
1. Project structure you would create
2. First file to implement
3. How you would test it works
```

## Acknowledgements

* **generate-agents.md**: This file was adapted from [llm-cursor-rules](https://github.com/RayFernando1337/llm-cursor-rules) created by [@RayFernando1337](https://twitter.com/RayFernando1337).