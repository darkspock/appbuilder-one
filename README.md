# AppBuilder One

AI-driven web app development framework for SaaS and management apps.
A Claude Code plugin that guides you from idea to deployment.

## Prerequisites

- [Claude Code](https://claude.ai/code) installed
- [GitHub CLI](https://cli.github.com/) (`gh`) installed and authenticated
- Node.js 18+ (for most stacks)

## Install

Inside Claude Code:

```
/plugin install https://github.com/darkspock/appbuilder-one
```

## Your First Project

```bash
# 1. Create a new directory and open Claude Code
mkdir my-app && cd my-app
claude

# 2. Start the guided onboarding
/appbuilder-one:start

# 3. It will ask your experience level and project type, then guide you:
#    → /appbuilder-one:brainstorm     (define what to build)
#    → /appbuilder-one:setup-stack    (choose your tech stack)
#    → /appbuilder-one:init           (scaffold the project)
#    → /appbuilder-one:map-modules    (plan the architecture)
#    → Start building!
```

That's it. The plugin asks questions one at a time and adapts to your level.

## What Happens Step by Step

```
/start           → Detects your profile (learning/solo/team/enterprise)
     ↓
/brainstorm      → Defines your product concept
     ↓
/setup-stack     → Picks frontend, backend, database, hosting, auth, AI...
     ↓
/init            → Creates the actual project (installs deps, creates files)
     ↓
/map-modules     → Breaks the product into modules with dependencies
     ↓
/design-module   → Designs each module (data model, API, rules, edge cases)
     ↓
/api-contract    → Defines API contracts before coding
     ↓
/new-feature     → Day-to-day: add features, one at a time
     ↓
/check-security  → Scan for vulnerabilities
/check-performance → Check for N+1 queries, missing indexes, bundle size
     ↓
/deploy          → Ship it
     ↓
/status          → See where you are
```

## 25 Skills

### Onboarding & Setup
| Skill | What it does |
|-------|-------------|
| `/start` | Guided onboarding — detects experience, recommends workflow |
| `/setup-stack` | Choose tech stack: framework, DB, auth, hosting, AI, i18n, GDPR |
| `/init` | Scaffold the project: install deps, create files, first commit |

### Product & Design
| Skill | What it does |
|-------|-------------|
| `/brainstorm` | From zero idea to structured product concept |
| `/discovery` | Validate if a feature is worth building (team/enterprise) |
| `/map-modules` | Decompose product into modules with dependencies |
| `/design-module` | Design one module: data model, API, rules, edge cases |

### Requirements & Architecture
| Skill | What it does |
|-------|-------------|
| `/epic` | Write a full epic/PRD with entities, rules, flows |
| `/requirement-validate` | Check requirements for completeness and clarity |
| `/requirement-slicing` | Split large epics into deployable features |
| `/requirement-design` | Technical design: DDD or standard architecture |
| `/requirement-tasks` | Generate implementation tasks from design |
| `/api-contract` | Define API contracts before coding (prevents front/back desync) |

### Development & Quality
| Skill | What it does |
|-------|-------------|
| `/new-feature` | Add a feature: impact analysis → design → implement → test |
| `/db-migrate` | Create, apply, rollback database migrations |
| `/prototype` | Quick throwaway prototype to validate an idea |
| `/code-review` | Review code for quality, security, architecture compliance |
| `/design-review` | Review design docs for completeness and consistency |
| `/bug-report` | Document, diagnose, and fix bugs |
| `/check-security` | Scan for vulnerabilities (OWASP, deps, secrets, GDPR) |
| `/check-performance` | Find N+1 queries, missing indexes, bundle bloat |

### Operations & Planning
| Skill | What it does |
|-------|-------------|
| `/architecture-decision` | Create ADR documenting a technical decision |
| `/sprint-plan` | Plan sprints, track progress, run retrospectives |
| `/deploy` | Deploy to Vercel, Railway, Hetzner, AWS, Fly.io, Docker |
| `/status` | Project dashboard: progress, tests, deploys, next actions |

## Adaptive Complexity

The plugin detects your situation and activates only what you need:

| Mode | For whom | What's active |
|------|----------|---------------|
| **Learning** | First-time devs | Simple stack, just build, minimal docs |
| **Solo** | Solo devs, real apps | + Architecture choice, light docs |
| **Team** | Small teams, real product | + Review gates, slicing, full docs |
| **Enterprise** | Professional projects | + GDPR, RACI, compliance, audit trails |

## Tech Stack

**Frontend** (recommended): React + Tailwind + shadcn/ui + Lucide React

**Backend** (by your language):

| You know... | We recommend |
|------------|-------------|
| Python | FastAPI |
| TypeScript | Next.js (fullstack) or Express |
| PHP | Laravel |
| Nothing yet | Next.js (one language for everything) |

**Infrastructure packs:**

| Pack | For | DB | Hosting | Cost |
|------|-----|-----|---------|------|
| Learning | Learning | Supabase | Supabase + Vercel | Free |
| Solo Fast | Ship quick | PostgreSQL | Railway | ~$5-10/mo |
| Solo Budget | Save money | PostgreSQL | Hetzner + Coolify | ~$4/mo |
| Team | Real product | PostgreSQL | Railway / AWS | ~$20-50/mo |
| Enterprise | Compliance | PostgreSQL | AWS | Variable |

**AI providers** (if your app uses AI):

| Provider | Best for |
|----------|----------|
| Groq | Fastest, cheapest — chat, real-time |
| OpenAI | GPT-4, embeddings, ecosystem |
| Anthropic | Complex reasoning, long context |
| OpenRouter | One API, all models |
| Ollama | Local, free, private |

## Recommended Companions

Install these for the best experience:

- **[context7 MCP](https://github.com/upstash/context7)** — Up-to-date docs for React, Tailwind, shadcn/ui, etc.
- **[frontend-design plugin](https://github.com/anthropics/claude-code/tree/main/plugins/frontend-design)** — Anthropic's official plugin for beautiful UI
- **`gh` CLI** — Required for GitHub, deploys, PRs (`brew install gh`)

## Philosophy

1. **Spec-Driven Development** — Define before you build
2. **Hierarchy of Technical Impact** — Foundation > Behavior > Aesthetics. Get the data model right first.
3. **Adaptive Complexity** — Only as much process as you need
4. **Contract-First APIs** — Define the contract, then implement both sides
5. **AI accelerates execution, humans own decisions**

## License

MIT
