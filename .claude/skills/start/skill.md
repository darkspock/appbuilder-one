# Guided Onboarding

Entry point for new users. Detects profile, activates the right mode,
and routes to the correct workflow.

## Workflow

### 1. Detect Project State (Silent)

Check:
- **Stack configured?** Read `.claude/docs/technical-preferences.md`
- **Product concept exists?** Check for `design/product/product-concept.md`
- **Source code exists?** Glob for source files in `src/`
- **Design docs exist?** Count markdown files in `design/product/`
- **Mode configured?** Check `.claude/docs/project-mode.md`

### 2. Detect User Profile

Ask ONE question at a time.

**Question 1: Experience**

> **Welcome to AppBuilder One!**
>
> Before I suggest anything, I need to understand your situation.
> What best describes your experience?
>
> **A) First timer** — I've never built a web app. I want to learn.
>
> **B) Some experience** — I've built things before, but I'm not an expert.
>
> **C) Experienced developer** — I know what I'm doing, I want structure
> and efficiency.
>
> **D) Team lead** — I'm setting up a project for a team.

Wait for answer.

**Question 2: Project type**

> What are you building?
>
> **A) Learning project** — Something to learn with, no real users.
>
> **B) Personal/side project** — Real app, but just me using it or small audience.
>
> **C) Startup/product** — Real product, real users, needs to be solid.
>
> **D) Enterprise/client work** — Professional project, compliance matters.

Wait for answer.

### 3. Assign Mode

Based on answers, assign a mode:

| Experience | Project Type | Mode |
|-----------|-------------|------|
| First timer | Learning | **learning** |
| First timer | Personal | **learning** |
| Some experience | Learning/Personal | **solo** |
| Some experience | Startup | **solo** |
| Experienced | Personal | **solo** |
| Experienced | Startup | **team** |
| Experienced | Enterprise | **enterprise** |
| Team lead | Any | **team** or **enterprise** |

### 4. Mode Definitions

Each mode activates a different subset of the framework:

#### Learning Mode
- `/start` → `/brainstorm` → `/setup-stack` (guided) → `/map-modules` → `/prototype`
- Minimal documentation, focus on building
- No compliance, no gates, no RACI
- Simple architecture (framework defaults)
- Free frontend design

#### Solo Mode
- `/start` → `/brainstorm` → `/setup-stack` → `/map-modules` → `/design-module` → `/sprint-plan`
- Light documentation (product concept + module designs)
- No compliance unless user asks
- Architecture choice: DDD or standard
- Frontend: guided or free
- Light code review (self-review checklist)

#### Team Mode
- Full Product Discovery available (optional)
- `/start` → `/brainstorm` or `/discovery` → `/setup-stack` → `/map-modules` → `/design-module` → `/sprint-plan`
- Full documentation (epics, features, designs, tasks)
- Architecture choice: DDD or standard
- Frontend: guided rules recommended
- Code review, design approval gates
- Slicing guidelines
- Definition of Done

#### Enterprise Mode
- Product Discovery required for major features
- All of Team mode, plus:
- Compliance checks (GDPR, data protection)
- RACI matrix
- Validation gates (all 7)
- Change management procedures
- Escalation procedures
- Metrics and KPIs
- Audit trails

### 5. Save Mode

Write mode to `.claude/docs/project-mode.md`:

```markdown
# Project Mode

**Mode**: [learning / solo / team / enterprise]
**Set**: [date]

## Active Features

- [ ] Product Discovery
- [ ] Validation Gates
- [ ] Compliance Checks
- [ ] RACI Matrix
- [ ] Slicing Guidelines
- [ ] Code Review Gates
- [ ] Change Management
- [ ] Metrics/KPIs
```

### 6. Ask Where They Are With Their Idea

Same as before:
- A) No idea → `/brainstorm`
- B) Vague idea → `/brainstorm [hint]`
- C) Clear concept → questions, then `/brainstorm` or `/setup-stack`
- D) Existing work → `/setup-stack` or `/map-modules`

### 7. Edge Cases

- **Returning user (mode exists, stack configured)**: Skip onboarding —
  "You're set up in [mode] mode with [stack]. What would you like to work on?"
- **User wants to change mode later**: `/start mode` to reconfigure
- **Mode doesn't fit**: Let them describe, adapt

## Collaborative Protocol

1. One question at a time
2. Present options — give clear paths
3. User decides
4. No auto-execution
5. Adapt to user's situation
