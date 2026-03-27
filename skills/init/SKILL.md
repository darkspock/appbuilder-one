---
name: init
description: Scaffold a new project from the configured stack. Creates real files, installs dependencies, sets up the development environment.
---

# Init Project

After `/setup-stack` configures choices, this skill creates the actual project.

## Usage

`/appbuilder-one:init` — Scaffold project from current stack configuration

## Prerequisites

- Stack must be configured (run `/appbuilder-one:setup-stack` first)
- Read `.claude/docs/technical-preferences.md` for stack choices

## Workflow

### 1. Read Stack Configuration

Read technical preferences to determine what to scaffold.

### 2. Scaffold by Stack

#### Next.js (React + TypeScript)
```bash
npx create-next-app@latest . --typescript --tailwind --eslint --app --src-dir
# Install shadcn/ui
npx shadcn@latest init
# Install Lucide icons
npm install lucide-react
```

#### React SPA + Vite
```bash
npm create vite@latest . -- --template react-ts
npm install tailwindcss @tailwindcss/vite
npx shadcn@latest init
npm install lucide-react
```

#### FastAPI (Python backend)
```bash
python -m venv .venv
pip install fastapi uvicorn sqlalchemy alembic pydantic
# Create folder structure (standard or DDD based on config)
```

#### Express (Node.js backend)
```bash
npm init -y
npm install express typescript @types/express ts-node
npm install -D nodemon
```

#### Laravel (PHP backend)
```bash
composer create-project laravel/laravel .
```

### 3. Create Common Files

For ALL stacks:

- **`.env.example`** — Template with all required env vars (no real values)
- **`.env`** — Copy of example, gitignored
- **`.gitignore`** — Stack-appropriate
- **`docker-compose.yml`** — If using local database (PostgreSQL, Redis)

### 4. Setup Database

Based on stack choice:

| Database | Setup |
|----------|-------|
| SQLite | Create DB file, no extra setup |
| PostgreSQL (local) | `docker-compose.yml` with postgres service |
| PostgreSQL (Supabase) | `supabase init` + link project |
| PostgreSQL (Railway) | `railway add --plugin postgresql` |

### 5. Setup Auth (if configured)

| Auth | Setup |
|------|-------|
| Built-in | Create auth module skeleton |
| Supabase Auth | Install `@supabase/supabase-js`, create client |
| NextAuth/Auth.js | `npm install next-auth`, create route handler |
| Clerk | `npm install @clerk/nextjs`, create middleware |

### 6. Setup i18n (if configured)

| Framework | Setup |
|-----------|-------|
| Next.js | Install `next-intl`, create `messages/` dir, configure middleware |
| React SPA | Install `react-i18next` + `i18next`, create `locales/` dir |

Create default language file with initial structure.

### 7. Setup AI (if configured)

| Provider | Setup |
|----------|-------|
| Groq | `npm install groq-sdk`, add `GROQ_API_KEY` to `.env.example` |
| OpenAI | `npm install openai`, add `OPENAI_API_KEY` to `.env.example` |
| Anthropic | `npm install @anthropic-ai/sdk`, add `ANTHROPIC_API_KEY` to `.env.example` |
| OpenRouter | `npm install openai` (compatible API), add `OPENROUTER_API_KEY` to `.env.example` |

### 8. Setup Architecture (if DDD)

Create the full folder structure:
```
src/
├── [context]_bc/
│   └── [domain]/
│       ├── application/
│       │   ├── commands/
│       │   ├── queries/
│       │   └── handlers/
│       ├── domain/
│       │   ├── entities/
│       │   ├── value_objects/
│       │   ├── events/
│       │   └── interfaces/
│       └── infrastructure/
│           ├── models/
│           └── repositories/
```

### 9. Setup Testing

| Stack | Framework | Setup |
|-------|-----------|-------|
| Next.js / React | Vitest + Testing Library | `npm install -D vitest @testing-library/react` |
| FastAPI | pytest | `pip install pytest pytest-asyncio httpx` |
| Express | Vitest / Jest | `npm install -D vitest` |
| Laravel | PHPUnit (built-in) | Already included |
| E2E | Playwright | `npm install -D @playwright/test` |

### 10. Create Project CLAUDE.md

Generate a project-specific CLAUDE.md in the project root with:
- Stack configuration
- Coding standards reference
- Architecture rules (if DDD)
- Frontend rules (if guided)
- Testing commands
- Development commands (`npm run dev`, etc.)

### 11. First Commit

```bash
git init
git add -A
git commit -m "Initial project scaffold — [stack summary]"
```

Ask user if they want to create a GitHub repo:
```bash
gh repo create [name] --public/--private --source=. --push
```

### 12. Verify

Run the project to verify it works:
```bash
npm run dev  # or equivalent
```

Report success or fix issues.

## Collaborative Protocol

- Show what will be installed before running
- Ask approval before each major step (scaffold, deps, docker)
- Verify the project runs before marking done
- Never install packages without showing them first
