# Avoiding LLM Drift When Using AI Coding Assistants

The way we code with AI assistants has evolved with the rise of agentic coding. Direct instructions beat meta (abstract) ones and using multiple lean instructions helps avoid LLM drift (this means when AI stops listening to you).

For example:
- Meta: "You are an expert Python developer. Write clean, Pythonic, robust code. Follow PEP 8 and best practices. Handle errors gracefully."
- Direct: "Use Python 3.12 and uv. Type-hint all public functions. Validate inputs with Pydantic models in src/schemas.py. Copy the repository pattern from src/db/user_repo.py. Name tests tests/test_*.py. Run ruff check . && uv run pytest -q before each commit."

However, you still need a controlled way to provide context and maintain a shared state across sessions.

Coding agents perform better when instructions explicitly cover:

* Problem statement, target users & JTBD (Jobs to Be Done), scope vs non-scope
* Acceptance criteria (what “done” means)
* Constraints (latency, cost, privacy, deployment)
* “Golden flows” and edge cases
* Evals and testing (how we know it works, commands, metrics, fixtures)
* Explicit out-of-scope items

When starting a project, it is crucial that `BRD.md` and `PRD.md` are documents **you** fill out, not artifacts you ask the AI to generate (though you can use AI to enhance them).

Then, generate the `AGENTS.md` file (small, concise, and distributed in folders) from the PRD if the project is new; otherwise have it read the entire codebase. The `AGENTS.md` (https://agents.md/) project is an attempt to standardize meta-instructions across different AI assistants. Also, use `TASKS.md` to track progress with bullet points to tick off by the AI.

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

## Work Task by Task

Do one task at a time. Create one branch and one PR for each task. Tick the task in TASKS.md after the PR.

For each task, do the steps below.

**a. Write the requirement.** You write this file, not the AI. Save it in `content-in/`. Example: `content-in/req.md`.

**b. Plan.** Use plan mode.
```
Ultrathink the requirement @content-in/req.md. Ask as many questions as you need.
Save the plan in content-out. Use the name YYYYMMDD-TOPIC-PLAN.md.
```

**c. Implement.** Use auto mode.
```
Ultracode the plan @content-out/YYYYMMDD-TOPIC-PLAN.md.
Use the python-expert developer skill when you write code.
Create a branch and a PR for this task.
```

**d. Record.**
```
Write an implementation record of all the work you did. Save it in content-out.
Use the name YYYYMMDD-TOPIC-RECORD.md. Include the record in the PR.
```

**e. Review.** Use another model for this step.
```
Review the implementation in PR #XX. The requirement is @content-in/req.md.
The plan is @content-out/YYYYMMDD-TOPIC-PLAN.md. The record is @content-out/YYYYMMDD-TOPIC-RECORD.md.
Review the code as well.
```

## Folders

- `content-in/` — Inputs. You put each requirement here.
- `content-out/` — Outputs. The AI saves plans and records here.

## Output Names

- Plan: `YYYYMMDD-TOPIC-PLAN.md`
- Record: `YYYYMMDD-TOPIC-RECORD.md`

Example: `content-out/20260821-improve-framework-PLAN.md`

## Project Structure

A project with this framework can look like this:

```
project/
├── README.md          # What the project is. How to run it.
├── AGENTS.md          # Root AI instructions. Sub-folders can have their own.
├── TASKS.md           # Milestones and tasks with checkboxes.
├── content-in/        # Inputs: requirements.
├── content-out/       # Outputs: plans and records.
├── src/               # Source code.
└── tests/             # Tests.
```

This tree is an example. Keep it in mind, but expect changes with the stack. A Python project and a JavaScript project need different folders. A backend and a frontend also differ.

## Rules

These rules apply to the prompts, the documents, and the code in a project.

**Writing rules**
- Do not use AI slop words. Examples: "delve", "seamless", "leverage", "robust", "comprehensive", "crucial".
- Use the ASD-STE100 technical writing style. The full specification is licensed. Use this summary of its core rules:
  - Write short sentences. Use 20 words or less.
  - Use the active voice.
  - Write one instruction per sentence.
  - Use simple words. Use one word for one meaning.
  - Use the present tense.
  - Do not stack more than two nouns.

**File mentions**
- Use `@path` mentions in prompts. Example: `@content-in/req.md`.
- Do not point to a file with prose only. A mention removes ambiguity. It also saves search tokens.

**Code rules**
- Do not preserve backward compatibility.
- Choose the simplest implementation that fully meets the current requirements.
- Prefer established, well-maintained libraries over custom implementations.

You can create a `guidelines.md` file in your project to hold these rules. The AI does not read it by itself. Point your AGENTS.md at it, or add `@guidelines.md` to your prompts.

The `reference/` folder has the python-expert skill as reference.

## Acknowledgements

* **generate-agents.md**: This file was adapted from [llm-cursor-rules](https://github.com/RayFernando1337/llm-cursor-rules) created by [@RayFernando1337](https://twitter.com/RayFernando1337).