# The Genesis System: Project Initialization Workflow

A structured 3-phase approach to initializing software projects with AI assistants. This workflow prevents hallucination and ensures architectural alignment before any code is written.

## Why This Exists

When you ask an AI to "build me an app," it often jumps straight to code, inventing requirements, picking random libraries, and creating inconsistent structures. The Genesis System forces a deliberate progression:

| Phase | Role | Output | Purpose |
|-------|------|--------|---------|
| 1 | Product Manager | `docs/PRD.md` | Converts ambiguity into specifications |
| 2 | Systems Architect | `docs/ARCH.md` | Converts specifications into constraints |
| 3 | DevOps Engineer | `setup_genesis.py` | Converts constraints into reality |

## Quick Start

### Prerequisites

1. Access to Claude, ChatGPT, or another capable LLM
2. A project idea you want to build
3. A code editor and terminal

### Phase 1: Define WHAT You're Building

**Prompt File:** [phase1.md](https://github.com/en4ble1337/The-Genesis-System-Project-Initialization-Workflow/blob/main/phase1.md)

**Steps:**

1. Copy the entire contents of `phase1.md`
2. Start a new conversation with your AI assistant
3. Paste the prompt, then describe your project idea
4. Answer the clarifying questions (respond like "1A, 2C, 3B" for speed)
5. Review the generated PRD
6. Save the output as `docs/PRD.md` in your project folder

**What You Get:** A complete Product Requirements Document with user stories, acceptance criteria, and clear scope boundaries.

**Example Interaction:**
```
You: [paste phase1.md] I want to build a task management app for small teams.

AI: Great! Let me ask a few clarifying questions...
    1. What is the primary goal?
       A. Replace existing tool (Trello, Asana)
       B. Lightweight internal tool
       C. Client-facing project tracker
       D. Other

You: 1B, 2C, 3A

AI: [Generates PRD.md]
```

### Phase 2: Define HOW You'll Structure It

**Prompt File:** [phase2.md](https://github.com/en4ble1337/The-Genesis-System-Project-Initialization-Workflow/blob/main/phase2.md)

**Steps:**

1. Create a `docs/` folder in your project if it doesn't exist
2. Save your PRD from Phase 1 as `docs/PRD.md`
3. Copy the entire contents of `phase2.md`
4. Start a new conversation (or continue if context allows)
5. Paste the prompt AND the contents of your `docs/PRD.md`
6. Answer the architecture clarifying questions
7. Save the output as `docs/ARCH.md`

**What You Get:** Technical architecture including tech stack, data models, API contracts, directory structure, and a domain dictionary that prevents conceptual drift.

**Example Interaction:**
```
You: [paste phase2.md]

     Here is my approved PRD:
     [paste contents of docs/PRD.md]

AI: Before I design the architecture, let me ask a few questions...
    1. What is the deployment target?
       A. Single VPS
       B. Docker containers
       ...

You: 1B, 2A, 3D, 4C, 5A

AI: [Generates ARCH.md]
```

### Phase 3: Create the Project Scaffold

**Prompt File:** [phase3.md](https://github.com/en4ble1337/The-Genesis-System-Project-Initialization-Workflow/blob/main/phase3.md)

**Steps:**

1. Ensure both `docs/PRD.md` and `docs/ARCH.md` exist in your project
2. Copy the entire contents of `phase3.md`
3. Start a new conversation
4. Paste the prompt AND the contents of both documents
5. The AI generates `setup_genesis.py`
6. Save the script to your project root
7. Run: `python setup_genesis.py`

**What You Get:** A complete project scaffold including directory structure, configuration files, `AGENTS.md` (the AI instruction kernel), and your first development directive.

**Example Interaction:**
```
You: [paste phase3.md]

     Here is my PRD:
     [paste docs/PRD.md]

     Here is my Architecture:
     [paste docs/ARCH.md]

AI: [Generates setup_genesis.py]
```

## After Genesis: The Development Loop

Once your project is scaffolded, development follows this pattern:

```
┌─────────────────────────────────────────────────┐
│  1. Agent reads AGENTS.md (system kernel)       │
│  2. Agent reads docs/PRD.md and docs/ARCH.md    │
│  3. Agent checks directives/ for current task   │
│  4. Agent writes tests first                    │
│  5. Agent implements in src/                    │
│  6. Agent marks directive complete              │
│  7. Repeat from step 3                          │
└─────────────────────────────────────────────────┘
```

## Project Structure After Setup

```
your-project/
├── AGENTS.md              # AI instruction kernel (read first every session)
├── setup_genesis.py       # The script that created this structure
├── requirements.txt       # Python dependencies (or package.json for Node)
├── .env.example           # Environment variable template
├── .gitignore             # Standard ignores for your stack
├── .cursorrules           # IDE AI configuration
│
├── docs/
│   ├── PRD.md             # Product Requirements (Phase 1 output)
│   └── ARCH.md            # Technical Architecture (Phase 2 output)
│
├── directives/
│   └── 001_initial_setup.md   # First task: configure environment
│
├── execution/
│   └── verify_setup.py    # Environment verification script
│
├── src/                   # Application source code
│   ├── api/               # Route handlers
│   ├── models/            # Database models
│   ├── schemas/           # Request/response schemas
│   └── services/          # Business logic
│
├── tests/                 # Test files (mirrors src/ structure)
│
└── .tmp/                  # Agent scratchpad (gitignored)
```

## Tips for Best Results

### Be Specific in Phase 1
The more detail you provide about your idea, the fewer clarifying questions needed. Include:
| Include | Example |
|---------|---------|
| Target users | "Internal team of 5 developers" |
| Core problem | "We waste time context switching between tools" |
| Must have features | "Task assignment, due dates, status tracking" |
| Explicit non goals | "No time tracking, no invoicing" |

### Don't Skip Phase 2 Questions
Architecture decisions have long term consequences. Take time to think through:
| Decision | Impact |
|----------|--------|
| Database choice | Data modeling, query patterns, scaling |
| Auth model | Security surface, user experience |
| Deployment target | DevOps complexity, cost |

### Trust the Constraints
Once ARCH.md defines your tech stack and structure, resist the urge to deviate. The whole point is to prevent drift and inconsistency.

## Customization

### Adding Your Own Sections

Feel free to extend the templates:

**PRD additions:**
| Section | When to Add |
|---------|-------------|
| Competitive Analysis | Building a product with market competitors |
| Compliance Requirements | Healthcare, finance, or regulated industries |
| Localization Needs | Multi language support required |

**ARCH additions:**
| Section | When to Add |
|---------|-------------|
| Caching Strategy | High traffic or expensive computations |
| Queue Architecture | Background jobs or async processing |
| Monitoring & Observability | Production systems needing alerts |

### Framework Specific Variants

The base templates are framework agnostic. For specific stacks, you might create variants:

| Stack | Modifications |
|-------|---------------|
| Next.js | App router structure, server components guidance |
| Django | Apps organization, settings split, migrations |
| FastAPI + React | Monorepo structure, shared types |

## Troubleshooting

### "The AI ignored my ARCH.md and used different libraries"

This usually happens when:
1. The conversation context was lost (start fresh, paste both docs)
2. The AI model has strong defaults (explicitly say "use ONLY the stack in ARCH.md")
3. ARCH.md wasn't specific enough (add version pins)

### "The generated PRD is too vague"

Go back to Phase 1 and:
1. Answer the clarifying questions more specifically
2. Add concrete examples of user workflows
3. Define explicit acceptance criteria for each story

### "Phase 3 script has errors"

The script is generated based on your specific ARCH.md. Common fixes:
1. Ensure ARCH.md has a complete "Tech Stack" section
2. Verify directory structure is fully specified
3. Check that all required environment variables are listed

## Contributing

Found ways to improve the prompts? Contributions welcome:

1. Fork the repository
2. Create a feature branch
3. Submit a pull request with your improvements

Especially valuable:
| Contribution Type | Examples |
|-------------------|----------|
| Framework variants | Rails, Laravel, Spring Boot specific versions |
| Additional phases | Phase 0 (discovery), Phase 4 (deployment) |
| Language translations | Non English versions of the prompts |

## License

MIT License. Use freely, modify as needed, no attribution required.
