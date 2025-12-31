# [Project Name] - Product Requirements

## Overview
> [One paragraph: what is this, who's it for, what does it do]

## Delivery Format
- [ ] Web app
- [ ] CLI tool
- [ ] API/service
- [ ] Jupyter notebook
- [ ] Mobile app
- [ ] Desktop app
- [ ] Library/package

## Core User Flows
Describe the 1-3 primary things a user does, step by step.

### Flow 1: [Name]
1. User does X
2. System responds with Y
3. User sees Z

### Flow 2: [Name]
1. ...

## Features by Priority

### Must Have (MVP)
| Feature | Description | Acceptance Criteria |
|---------|-------------|---------------------|
| [Name] | [What it does] | [How we know it works] |

### Should Have (v1.1)
| Feature | Description |
|---------|-------------|
| [Name] | [What it does] |

### Won't Have (for now)
- [Feature we're explicitly deferring]

## Technical Requirements
- **Language/Runtime:** [e.g., Python 3.12+]
- **Key Dependencies:** [e.g., FastAPI, SQLAlchemy, OpenAI SDK]
- **Data Storage:** [e.g., SQLite for local, Postgres for prod]
- **External APIs:** [e.g., OpenAI, BigQuery]
- **Auth:** [e.g., None for MVP / API key / OAuth]
- **Package Manager:** [e.g., uv, pip]
- **Testing:** [e.g., pytest]

## Data Model (if applicable)
```
[Simple ERD or table descriptions]
```

## UI/UX Notes (if applicable)
> [Describe the vibe: minimal CLI? Dashboard? Chat interface?]
> [Link to sketch/wireframe if you have one]

## Open Questions
- [ ] [Decision we haven't made yet]
- [ ] [Thing we need to research]

## Github Repository Structure
```
project/
├── README.md          # What this is, how to run it
├── AGENTS.md          # Project-specific AI instructions (tech stack, patterns to follow, anti-patterns)
├── tests/             # Your spec - write these first
└── src/               # AI implements to pass tests
```