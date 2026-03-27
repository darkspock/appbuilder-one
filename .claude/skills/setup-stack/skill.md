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

#### Q4: Database

> Database?
>
> | Database | Best for |
> |----------|----------|
> | **PostgreSQL** | Most SaaS apps. Industry standard. Recommended. |
> | **MySQL** | Simpler apps, wide hosting support |
> | **SQLite** | Prototypes, small apps, zero config |
> | **MongoDB** | Document-heavy, flexible schema |

**For learning mode**: Default to SQLite or PostgreSQL with a note.

#### Q5: Auth

> How do you want to handle authentication?
>
> | Option | Best for | Cost |
> |--------|----------|------|
> | **Built-in** | Learning, full control | Free |
> | **Supabase Auth** | Quick setup, Postgres-native | Free tier |
> | **Auth0** | Enterprise, complex requirements | Free tier |
> | **Clerk** | Beautiful UI, fast integration | Free tier |
> | **NextAuth/Auth.js** | Next.js projects | Free |

#### Q6: Hosting

> Where do you want to deploy?
>
> | Option | Best for | Cost |
> |--------|----------|------|
> | **Vercel** | Next.js, easy deploys | Free tier |
> | **Railway** | Full-stack, DB included | Free tier |
> | **Fly.io** | Docker, edge deployment | Free tier |
> | **Supabase** | Backend-as-service + Postgres | Free tier |
> | **VPS (Hetzner/DO)** | Full control, predictable cost | ~$5/mo |
> | **AWS** | Enterprise, scalable | Pay-as-you-go |

#### Q7: Backend Architecture (Solo/Team/Enterprise only)

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

#### Q8: Frontend Design Rules (Solo/Team/Enterprise only)

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

#### Q9: Extras (optional)

> Any of these? (skip any you don't need)
>
> - **ORM**: Prisma / Drizzle / TypeORM / SQLAlchemy / ActiveRecord
> - **CSS**: Tailwind / CSS Modules / Styled Components
> - **Component Library**: shadcn/ui / Radix / MUI / Ant Design
> - **Email**: Resend / SendGrid / Postmark
> - **File storage**: S3 / Cloudflare R2 / Supabase Storage

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

Based on Q7 and Q8 answers:
- Backend architecture doc (DDD or standard)
- Frontend standards doc (guided or free)

Ask approval before writing each.

### 6. Create Initial Config Files (optional)

Suggest creating:
- `.gitignore` appropriate for the stack
- `package.json` or equivalent (for reference, not functional)
- Basic config suggestions (tsconfig, eslint, etc.)

Ask before creating each.

### 7. Output Summary

```
Stack Setup Complete
====================
Mode:        [learning / solo / team / enterprise]
Frontend:    [choice]
Backend:     [choice]
Database:    [choice]
Auth:        [choice]
Hosting:     [choice]
Architecture: [DDD / Standard / N/A]
Frontend Rules: [Guided / Free / N/A]

Next Steps:
1. Run /brainstorm to define your product
2. Run /map-modules to decompose into modules
3. Run /prototype to scaffold the base app
```

## Guardrails

- NEVER guess versions — verify or ask
- NEVER overwrite existing config without asking
- One question at a time
- Adapt depth to project mode
