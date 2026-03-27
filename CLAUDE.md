# AppBuilder One — Plugin Reference

> This file is the plugin's internal reference. When installed as a plugin,
> skills are available as `/appbuilder-one:skill-name` in any project.

## Skills

| Skill | Purpose | Modes |
|-------|---------|-------|
| `/appbuilder-one:start` | Onboarding + profile detection | All |
| `/appbuilder-one:setup-stack` | Configure stack + infrastructure pack | All |
| `/appbuilder-one:brainstorm` | Define product concept | All |
| `/appbuilder-one:discovery` | Product Discovery (validate opportunity) | Solo+, Team, Enterprise |
| `/appbuilder-one:epic` | Write epic/PRD | Solo+, Team, Enterprise |
| `/appbuilder-one:requirement-validate` | Validate requirements | Solo+, Team, Enterprise |
| `/appbuilder-one:requirement-slicing` | Slice epic into features | Team, Enterprise |
| `/appbuilder-one:requirement-design` | Technical design for feature | All |
| `/appbuilder-one:requirement-tasks` | Generate implementation tasks | All |
| `/appbuilder-one:map-modules` | Decompose into modules | All |
| `/appbuilder-one:design-module` | Design individual module | All |
| `/appbuilder-one:new-feature` | Add features day-to-day | All |
| `/appbuilder-one:init` | Scaffold project from stack config | All |
| `/appbuilder-one:api-contract` | Define API contracts before implementing | All |
| `/appbuilder-one:db-migrate` | Database migrations (create, apply, rollback) | All |
| `/appbuilder-one:prototype` | Quick throwaway prototype | All |
| `/appbuilder-one:code-review` | Code quality and architecture review | Solo+ |
| `/appbuilder-one:design-review` | Design doc completeness review | Solo+ |
| `/appbuilder-one:bug-report` | Document, diagnose, fix bugs | All |
| `/appbuilder-one:check-security` | Security vulnerability scan | All |
| `/appbuilder-one:check-performance` | Performance analysis | All |
| `/appbuilder-one:architecture-decision` | Create ADR for technical decisions | Solo+ |
| `/appbuilder-one:sprint-plan` | Plan sprints and track progress | All |
| `/appbuilder-one:deploy` | Deploy with strategies per hosting | All |
| `/appbuilder-one:status` | Project status dashboard | All |

## Project Modes

| Mode | Target | Framework Depth |
|------|--------|----------------|
| **Learning** | First-time dev, learning project | Minimal docs, simple stack |
| **Solo** | Solo dev, real project | Light docs, architecture choice |
| **Team** | Small team, product | Full docs, review gates |
| **Enterprise** | Professional, compliance needed | Full + compliance + RACI |

## Stack Decisions

**Frontend (fixed):** React + Tailwind + shadcn/ui + Lucide React (no SVGs)
**Backend (by language):** FastAPI (Python) / Next.js API (TypeScript) / Express (Node) / Laravel (PHP)
**Infrastructure packs:** Learning (Supabase free) / Solo Fast (Railway) / Solo Budget (Hetzner+Coolify) / Team (Railway/AWS) / Enterprise (AWS)

## Recommended Plugins & MCPs

- **context7 MCP** — Up-to-date docs for React, Tailwind, shadcn/ui, etc.
- **frontend-design plugin** — Anthropic's official frontend design skill
- **gh CLI** — Required for all GitHub operations and deploy workflows

## Reference Docs

Plugin ships with reference docs in `docs-plugin/`:
- `coding-standards.md` — Code quality rules
- `technical-preferences.md` — Stack preferences template
- `coordination-rules.md` — Agent coordination
- `context-management.md` — Context window management
- `templates/` — Document templates (product-concept, module-design, epic, etc.)

## Hierarchy of Technical Impact

| Level | What | Cost of Error |
|-------|------|---------------|
| **1. Foundation** | Entities, business logic, integration contracts | **Critical** |
| **2. Behavior** | Flows, states, edge cases | **Medium** |
| **3. Aesthetics** | Colors, spacing, copywriting | **Low** |
