---
name: setup-stack
description: Configure technology stack: frontend, backend, database, auth, hosting, architecture. Recommends infrastructure packs by project mode.
---

# Setup Stack

Configure the project's technology stack through guided recommendations.
Adapts depth based on project mode (learning/solo/team/enterprise).

## Workflow

### 1. Read Mode

Read `.claude/docs/project-mode.md` to determine depth:
- **Learning**: Recommend simple stacks, skip advanced questions
- **Solo**: Full stack choice, architecture question
- **Team/Enterprise**: Full stack choice, architecture, frontend rules, CI/CD

### 2. Ask Questions ONE AT A TIME

#### Q1: Experience with web development (if not already known from /start)

Skip if already answered in `/start`.

#### Q2: Frontend Framework

Present options based on experience:

**For beginners:**
> I recommend starting with one of these — they include both frontend and backend:
>
> **A) Next.js (React)** — The most popular. Huge ecosystem, tons of tutorials.
> **B) Nuxt (Vue)** — Gentler learning curve than React. Great docs.
> **C) SvelteKit** — The simplest to learn. Less boilerplate.

**For experienced:**
> Frontend framework?
>
> | Framework | Best for | SSR | Learning curve |
> |-----------|----------|-----|---------------|
> | Next.js (React) | Large SaaS, big ecosystem | Yes | Moderate |
> | Nuxt (Vue) | Gentler DX, good conventions | Yes | Gentle |
> | SvelteKit | Performance, simplicity | Yes | Gentle |
> | React SPA + Vite | If you have a separate backend | No | Moderate |
> | HTMX + templates | Simple CRUD, minimal JS | Server | Minimal |

#### Q3: Backend (if not fullstack framework)

Only ask if they chose a SPA or HTMX approach:

> Backend framework?
>
> | Framework | Language | Best for |
> |-----------|----------|----------|
> | FastAPI | Python | APIs, async, type-safe |
> | Django | Python | Full-featured, admin panel |
> | Express | Node.js | Minimal, flexible |
> | NestJS | TypeScript | Structured, enterprise |
> | Laravel | PHP | Rapid development, batteries included |
> | Rails | Ruby | Convention over configuration |
> | Go + Gin | Go | Performance-critical APIs |

#### Q4: Infrastructure Pack

Instead of asking DB, Auth, and Hosting separately, recommend a **pack**
based on the user's mode and project type. Present the recommended pack
first, then offer alternatives.

**Pack recommendations by mode:**

##### Learning Pack (€0/mo)
> For learning, I recommend **Supabase** — it gives you database, auth, and
> hosting in one place, all free:
>
> - **Database**: PostgreSQL (hosted by Supabase)
> - **Auth**: Supabase Auth (built-in)
> - **Hosting**: Supabase (backend) + Vercel (frontend)
> - **Domain**: Not needed yet
> - **Cost**: Free
>
> Alternatively, everything local: SQLite + built-in auth + localhost.

##### Solo Fast Pack (~$5-10/mo)
> For a real project with minimal ops:
>
> - **Database**: PostgreSQL (via Railway or Supabase)
> - **Auth**: Supabase Auth / Auth.js / Clerk
> - **Hosting**: Railway (full-stack) or Vercel + Supabase
> - **Domain**: Cloudflare (~$10/year, cheapest + best DNS)
> - **Cost**: $0-10/mo

##### Solo Budget Pack (~€4/mo)
> Maximum control, minimum cost:
>
> - **Database**: PostgreSQL (self-hosted on VPS)
> - **Auth**: Built-in or Supabase Auth
> - **Hosting**: Hetzner/OVH VPS + Coolify (self-hosted PaaS)
> - **Domain**: Cloudflare (~$10/year)
> - **Cost**: ~€4/mo
>
> Coolify gives you a Railway-like experience on your own VPS.

##### Team Pack (~$20-50/mo)
> Production-ready for a real product:
>
> - **Database**: PostgreSQL (Railway / Supabase / managed)
> - **Auth**: Auth0 / Clerk
> - **Hosting**: Railway / Fly.io / Vercel
> - **Domain**: Cloudflare
> - **Cost**: $20-50/mo

##### Enterprise Pack (variable)
> Full control, compliance-ready:
>
> - **Database**: PostgreSQL / MySQL (AWS RDS or dedicated)
> - **Auth**: Auth0 / Custom
> - **Hosting**: AWS (full suite) or Hetzner dedicated
> - **Domain**: Cloudflare
> - **Cost**: Variable
>
> **Note on AWS**: Claude Code can manage all AWS resources directly via
> `aws` CLI — creating EC2 instances, RDS databases, S3 buckets, Lambda
> functions, IAM roles, CloudFront distributions, etc. No console needed.

After presenting the recommended pack, ask:
> "Does this pack work for you, or would you like to customize any part?"

Allow mixing: e.g., take the Solo Fast pack but swap Railway for Hetzner.

#### Q5: Domain (if hosting pack includes one)

> For domains, I recommend **Cloudflare Registrar**:
> - Domains at cost (~$10/year for .com)
> - Free DNS, CDN, and DDoS protection
> - Full API — Claude can manage DNS records via `wrangler` CLI
>
> Other options: Namecheap, Porkbun, Vercel Domains
>
> Do you want to set up a domain now, or later?

#### Q6: Backend Architecture (Solo/Team/Enterprise only)

Skip for learning mode.

> How do you want to structure your backend code?
>
> **A) Framework standard** — Follow the default conventions of your framework
> (MVC for Laravel/Rails/Django, routes+handlers for Express/FastAPI).
> Simpler, faster to start, well-documented.
>
> **B) DDD (Domain-Driven Design)** — Clean Architecture with bounded contexts,
> CQRS, hexagonal architecture. More structure, better for complex domains.
> More upfront work, but scales better.
>
> **C) Not sure** — I'll recommend based on your project scope.

If C: Recommend standard for small projects, DDD for complex domains with
many entities and business rules.

**If DDD selected**, generate architecture rules document at
`.claude/docs/architecture/backend-architecture.md` covering:
- Bounded contexts structure
- Domain layer (entities, value objects, events, interfaces)
- Application layer (commands, queries, handlers, DTOs)
- Infrastructure layer (repositories, models)
- Presentation layer (controllers, routers, schemas, mappers)
- Communication between bounded contexts
- Prohibited patterns (no business logic in controllers, no direct DB access)

**If Standard selected**, generate lightweight architecture doc with:
- Framework-specific folder structure
- Naming conventions
- Key patterns (services, middleware, etc.)

#### Q7: Frontend Design Rules (Solo/Team/Enterprise only)

Skip for learning mode.

> How do you want to manage frontend code quality?
>
> **A) Guided (recommended for teams)** — I'll generate coding standards
> covering: component patterns, TypeScript strictness, styling rules,
> error handling, API integration, performance patterns.
>
> **B) Free** — Minimal rules. Just follow framework conventions.
> More flexibility, less consistency.

**If Guided selected**, generate frontend standards at
`.claude/docs/architecture/frontend-standards.md` covering:
- Contract-first API development
- Component composition rules
- TypeScript strict guidelines (no `any`)
- Styling standards (Tailwind/CSS approach)
- Error handling patterns
- Performance optimization patterns
- File naming and organization
- Import ordering
- Security guidelines

**If Free selected**, generate minimal doc with just:
- File naming conventions
- Folder structure

#### Q8: Testing (All modes)

> What level of testing do you want?
>
> **A) Basic** — Unit tests for business logic only.
>
> **B) Standard** — Unit + integration tests.
>
> **C) Full** — Unit + integration + E2E (browser tests).

Recommended frameworks based on stack:

| Stack | Unit/Integration | E2E |
|-------|-----------------|-----|
| Next.js / React | **Vitest** + Testing Library | **Playwright** |
| FastAPI | **pytest** + httpx | Playwright |
| Express | **Vitest** / Jest | Playwright |
| Laravel | **PHPUnit** (built-in) | Playwright |

**Playwright** is the recommended E2E framework for all stacks — cross-browser,
fast, excellent DX. Claude can write and run Playwright tests.

#### Q9: Git Workflow

> How do you want to work with Git?
>
> **A) Simple** — Work on `main`, commit directly. Good for learning and solo.
>
> **B) Trunk-based** — Short-lived feature branches, merge to `main` via PR.
> Recommended for most projects.
>
> **C) GitFlow** — `main` + `develop` + feature/release/hotfix branches.
> For projects with formal releases.

If B or C, configure:
- Branch naming convention: `feature/[name]`, `hotfix/[name]`
- Conventional commits: `feat:`, `fix:`, `chore:`, `docs:`
- PR template in `.github/pull_request_template.md`

#### Q10: Internationalization (i18n)

> Will your app need multiple languages?
>
> **A) No** — Single language only.
>
> **B) Yes, from the start** — I want to set up i18n now so all text is
> translatable from day one.
>
> **C) Later** — Not now, but I want the architecture ready to add it.

If B or C:
> Recommended setup:
> - **next-intl** (for Next.js) or **react-i18next** (for React SPA)
> - Translation files in `locales/[lang].json`
> - All user-facing text via translation keys — no hardcoded strings
> - Default language: [ask which]
>
> If C (later): Set up the library and folder structure now, but only
> create the default language file. Adding languages later is trivial.

**Rule added to coding standards**: All user-facing strings must use
translation keys. No hardcoded text in components.

#### Q11: GDPR & Data Privacy (Solo/Team/Enterprise)

Skip for learning mode.

> Does your app handle personal data from EU users?
>
> **A) No** — No personal data or non-EU only.
>
> **B) Yes, basic** — User accounts with email, name, etc.
>
> **C) Yes, sensitive** — Health data, financial data, minors, etc.

If B:
> I'll add basic GDPR requirements to your project:
> - Cookie consent mechanism
> - Privacy policy page (template)
> - User data export capability (right to portability)
> - User account deletion (right to be forgotten)
> - Consent tracking in database
> - Data processing documentation

If C:
> Full GDPR compliance needed. I'll add:
> - Everything from B, plus:
> - Data Protection Impact Assessment template
> - Data processing register
> - Encryption requirements for sensitive fields
> - Audit logging for all data access
> - Data retention policies
> - Breach notification procedure
> - DPO (Data Protection Officer) requirements check

**Rule**: GDPR requirements become acceptance criteria in every module
that handles personal data.

#### Q12: AI Features

> Will your app use AI (LLMs, embeddings, classification, etc.)?
>
> **A) No** — No AI features planned.
>
> **B) Yes, basic** — Text generation, summarization, chat features.
>
> **C) Yes, advanced** — Embeddings, RAG, classification, fine-tuning.

If B or C, recommend provider:

> **AI Provider recommendation:**
>
> | Provider | Best for | Cost | Speed |
> |----------|----------|------|-------|
> | **Groq** | Fast inference, chat features, real-time | Very cheap | Ultra-fast |
> | **OpenAI** | GPT-4, DALL-E, Whisper, ecosystem | Moderate | Fast |
> | **Anthropic (Claude)** | Complex reasoning, long context, coding | Moderate | Fast |
> | **OpenRouter** | Access to ALL models via one API (Groq, OpenAI, Claude, Llama, Mistral...) | Varies by model | Varies |
> | **Ollama (local)** | Privacy, no API costs, development | Free | Depends on hardware |
>
> **My recommendation by use case:**
> - Chat / text generation → **Groq** (fastest, cheapest)
> - Complex reasoning / analysis → **OpenAI** or **Anthropic**
> - Embeddings / RAG → **OpenAI** (text-embedding-3) + **pgvector** (Supabase/PostgreSQL)
> - Privacy-critical → **Ollama** (runs locally)
> - Multiple models / flexibility → **OpenRouter** (one API key, all models, switch anytime)
> - Multiple needs → **Groq** for speed + **OpenAI** for quality (mix and match)

If C (advanced):
> For RAG / embeddings, I'll recommend:
> - **pgvector** extension for PostgreSQL (vector search in your existing DB)
> - Supabase has pgvector built-in
> - Embedding model: OpenAI `text-embedding-3-small` (cheap, good quality)
> - Chunking strategy as part of module design

**EU AI Act note** (Enterprise mode):
> If your app makes automated decisions that affect users (credit scoring,
> hiring, content moderation), the EU AI Act may classify it as high-risk.
> I'll add compliance checks to your requirements validation.

#### Q13: Extras (optional)

> Any of these? (skip any you don't need)
>
> - **ORM**: Prisma / Drizzle / TypeORM / SQLAlchemy / ActiveRecord
> - **CSS**: Tailwind / CSS Modules / Styled Components
> - **Component Library**: shadcn/ui / Radix / MUI / Ant Design
> - **Email**: Resend / SendGrid / Postmark
> - **File storage**: S3 / Cloudflare R2 / Supabase Storage
> - **Payments**: Stripe / Lemon Squeezy

### 3. Update CLAUDE.md

Replace `[CHOOSE]` placeholders with actual values.

### 4. Populate Technical Preferences

Fill `.claude/docs/technical-preferences.md` with stack-appropriate defaults:
- Naming conventions for the chosen stack
- Testing frameworks
- Performance budgets
- Linting/formatting config

Present to user for approval before writing.

### 5. Generate Architecture Docs

Based on Q6 and Q7 answers:
- Backend architecture doc (DDD or standard)
- Frontend standards doc (guided or free)

Ask approval before writing each.

### 6. Recommend Plugins & MCPs

After stack configuration, recommend installing these tools:

#### MCP Context7 (All modes)
> **Recommended: Install the context7 MCP**
> It provides up-to-date documentation for your stack libraries directly
> to Claude. Prevents suggesting deprecated APIs or incorrect patterns.
>
> Useful for: React, Tailwind, shadcn/ui, Next.js, FastAPI, Laravel, etc.

#### Anthropic Frontend Design Plugin (All modes)
> **Recommended: Install the official `frontend-design` plugin**
> https://github.com/anthropics/claude-code/tree/main/plugins/frontend-design
>
> Creates distinctive, production-grade frontend interfaces with high
> design quality. Avoids generic "AI slop" aesthetics.

#### GitHub CLI (All modes)
> **Required: `gh` CLI must be installed and authenticated**
> All projects use GitHub for version control. Claude manages repos,
> PRs, releases, and CI/CD via `gh`.
>
> Install: `brew install gh` → `gh auth login`

### 7. Create Initial Config Files (optional)

Suggest creating:
- `.gitignore` appropriate for the stack
- `package.json` or equivalent (for reference, not functional)
- Basic config suggestions (tsconfig, eslint, etc.)

Ask before creating each.

### 8. Output Summary

```
Stack Setup Complete
====================
Mode:           [learning / solo / team / enterprise]
Frontend:       [choice]
Backend:        [choice]
Infrastructure: [pack name]
  Database:     [choice]
  Auth:         [choice]
  Hosting:      [choice]
  Domain:       [choice or "later"]
Architecture:   [DDD / Standard / N/A]
Frontend Rules: [Guided / Free / N/A]
Testing:        [Basic / Standard / Full (+ E2E)]
Git Workflow:   [Simple / Trunk-based / GitFlow]
i18n:           [No / Yes (library) / Ready for later]
GDPR:           [No / Basic / Full]
AI Provider:    [None / Groq / OpenAI / Anthropic / Ollama / OpenRouter]

CLI Tools Available:
  [list of CLIs Claude can use for the chosen stack]

Next Steps:
1. Run /appbuilder-one:brainstorm to define your product
2. Run /appbuilder-one:map-modules to decompose into modules
3. Run /appbuilder-one:new-feature to start building
```

## CLI Tools Reference

Claude Code can manage infrastructure directly via CLI:

| Service | CLI | What Claude can do |
|---------|-----|-------------------|
| Supabase | `supabase` | Create project, migrations, deploy edge functions |
| Vercel | `vercel` | Deploy, env vars, domains, preview |
| Railway | `railway` | Deploy, create DB, env vars |
| Hetzner | `hcloud` | Create VPS, firewall, networks |
| AWS | `aws` | Everything: EC2, RDS, S3, Lambda, IAM, CloudFront |
| Cloudflare | `wrangler` | DNS records, Workers, Pages, R2, domains |
| Fly.io | `fly` | Deploy, scaling, volumes |
| Coolify | API | Deploy via REST API |

When the user chooses a hosting provider, note which CLI tools are available
and suggest installing them.

## Guardrails

- NEVER guess versions — verify or ask
- NEVER overwrite existing config without asking
- One question at a time
- Adapt depth to project mode
- Present recommended pack first, then alternatives
- Always mention CLI capabilities for the chosen stack
