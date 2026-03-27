# AppBuilder One

AI-driven web app development framework for SaaS and management apps.
A Claude Code plugin that guides you from idea to deployment.

## Install

```bash
/plugin install https://github.com/darkspock/appbuilder-one
```

## Quick Start

```bash
# In any new project directory:
/appbuilder-one:start
```

The onboarding detects your experience level and project type, then
recommends the right workflow.

## What It Does

AppBuilder One provides **15 skills** that cover the full development lifecycle:

### Discovery & Planning
- **`/start`** — Guided onboarding, profile detection
- **`/brainstorm`** — Product ideation, from zero to concept
- **`/discovery`** — Validate opportunities before building
- **`/setup-stack`** — Choose tech stack with infrastructure packs

### Design & Requirements
- **`/epic`** — Write epics/PRDs with structured requirements
- **`/requirement-validate`** — Validate requirements completeness
- **`/requirement-slicing`** — Slice epics into deployable features
- **`/requirement-design`** — Technical design (DDD or standard)
- **`/requirement-tasks`** — Generate implementation tasks
- **`/map-modules`** — Decompose into modules with dependencies
- **`/design-module`** — Design individual modules section by section

### Development
- **`/init`** — Scaffold project from stack config (install deps, create files)
- **`/new-feature`** — Add features day-to-day
- **`/api-contract`** — Define API contracts before implementing
- **`/db-migrate`** — Database migrations (create, apply, rollback, seed)
- **`/check-security`** — Security vulnerability scanning
- **`/check-performance`** — Performance analysis and budgets
- **`/deploy`** — Deploy strategies per hosting provider
- **`/status`** — Project status dashboard

## Adaptive Complexity

The framework adapts to your situation:

| Mode | For | What's Active |
|------|-----|---------------|
| **Learning** | First-time devs | Simple stack, minimal docs, just build |
| **Solo** | Solo devs, real projects | Architecture choice, light docs |
| **Team** | Small teams | Full docs, review gates, slicing |
| **Enterprise** | Professional projects | + Compliance, RACI, audit trails |

## Tech Stack

**Frontend (fixed):** React + Tailwind + shadcn/ui + Lucide React

**Backend (recommended by language):**

| Language | Framework |
|----------|-----------|
| Python | FastAPI |
| TypeScript | Next.js API routes or Express |
| PHP | Laravel |

**Infrastructure packs by mode:**

| Pack | Database | Hosting | Cost |
|------|----------|---------|------|
| Learning | Supabase (free) | Supabase + Vercel | Free |
| Solo Fast | PostgreSQL | Railway | ~$5-10/mo |
| Solo Budget | PostgreSQL | Hetzner + Coolify | ~$4/mo |
| Team | PostgreSQL | Railway / AWS | ~$20-50/mo |
| Enterprise | PostgreSQL / MySQL | AWS | Variable |

## Recommended Companions

- **[context7 MCP](https://github.com/upstash/context7)** — Up-to-date library documentation
- **[frontend-design plugin](https://github.com/anthropics/claude-code/tree/main/plugins/frontend-design)** — Anthropic's official frontend design skill
- **`gh` CLI** — Required for GitHub operations and deploy workflows

## Philosophy

1. **Spec-Driven Development** — Define before you build
2. **Hierarchy of Technical Impact** — Foundation > Behavior > Aesthetics
3. **Adaptive Complexity** — Only as much process as you need
4. **AI accelerates execution, humans own decisions**

## License

MIT
