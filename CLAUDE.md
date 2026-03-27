# AppBuilder One — Web App Development Architecture

SaaS and management app development managed through coordinated Claude Code agents.
Adapts to your experience level and project complexity.

## Project Mode

@.claude/docs/project-mode.md

## Technology Stack

- **Type**: Web application (SaaS / management)
- **Frontend**: [CHOOSE — run /setup-stack]
- **Backend**: [CHOOSE — run /setup-stack]
- **Database**: [CHOOSE — run /setup-stack]
- **Auth**: [CHOOSE — run /setup-stack]
- **Hosting**: [CHOOSE — run /setup-stack]
- **Architecture**: [Standard / DDD — run /setup-stack]
- **Frontend Rules**: [Free / Guided — run /setup-stack]
- **Version Control**: Git with trunk-based development

## Project Structure

@.claude/docs/directory-structure.md

## Technical Preferences

@.claude/docs/technical-preferences.md

## Architecture

@.claude/docs/architecture/backend-architecture.md
@.claude/docs/architecture/frontend-standards.md

## Coordination Rules

@.claude/docs/coordination-rules.md

## Collaboration Protocol

**User-driven collaboration, not autonomous execution.**
Every task follows: **Question -> Options -> Decision -> Draft -> Approval**

- Agents MUST ask "May I write this to [filepath]?" before using Write/Edit tools
- Agents MUST show drafts or summaries before requesting approval
- Multi-file changes require explicit approval for the full changeset
- No commits without user instruction

> **First session?** Run `/start` to begin the guided onboarding flow.

## Development Workflow

The framework has two processes:

| Process | Question | When |
|---------|----------|------|
| **Product Discovery** | "Should we build this?" | New features, high uncertainty |
| **Development** | "How do we build this?" | After Discovery validates (or for low-risk items) |

### Development Flow (per feature)

```
Epic → Validate → Slice (if big) → Design → Tasks → Implement → Review → Deploy
```

### Available Skills

| Skill | Purpose | Modes |
|-------|---------|-------|
| `/start` | Onboarding, profile detection | All |
| `/setup-stack` | Configure technology stack | All |
| `/brainstorm` | Define product concept | All |
| `/discovery` | Product Discovery (validate opportunity) | Solo+, Team, Enterprise |
| `/epic` | Write epic/PRD | Solo+, Team, Enterprise |
| `/requirement-validate` | Validate requirements | Solo+, Team, Enterprise |
| `/requirement-slicing` | Slice epic into features | Team, Enterprise |
| `/requirement-design` | Technical design for feature | All |
| `/requirement-tasks` | Generate implementation tasks | All |
| `/map-modules` | Decompose into modules | All |
| `/design-module` | Design individual module | All |
| `/new-feature` | Add feature day-to-day | All |
| `/code-review` | Review code quality | Solo+, Team, Enterprise |
| `/sprint-plan` | Plan sprint | All |
| `/prototype` | Rapid prototype | All |
| `/deploy` | Deployment checklist | Team, Enterprise |

## Coding Standards

@.claude/docs/coding-standards.md

## Context Management

@.claude/docs/context-management.md

## Hierarchy of Technical Impact

When writing requirements, not all specifications are equal:

| Level | What | Cost of Error |
|-------|------|---------------|
| **1. Foundation** | Entities, business logic, integration contracts | **Critical** — define 100% before coding |
| **2. Behavior** | Flows, states, edge cases | **Medium** — define expected behavior |
| **3. Aesthetics** | Colors, spacing, copywriting | **Low** — can be iterative |

> Get Level 1 right, or pay the cost forever. Errors at the foundation level
> create a domino effect where each fix needs another fix.
