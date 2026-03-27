---
name: architecture-decision
description: Create an Architecture Decision Record (ADR) documenting a significant technical choice, alternatives considered, and consequences.
---

# Architecture Decision Record

Document significant technical decisions so the team (and future you)
understands why things were built a certain way.

## Usage

`/appbuilder-one:architecture-decision [topic]`

Example: `/appbuilder-one:architecture-decision authentication-strategy`

## When to Use

- Choosing between technologies (React vs Vue, PostgreSQL vs MongoDB)
- Deciding architecture patterns (DDD vs MVC, monolith vs microservices)
- Making irreversible or expensive-to-change decisions
- When someone asks "why did we do it this way?"

## Workflow

### 1. Gather Context

Ask ONE question at a time:
- What decision needs to be made?
- What options are you considering?
- What constraints matter? (cost, time, team skills, scale)

### 2. Generate ADR

Save to `docs/architecture/adr-[NNN]-[topic].md`:

```markdown
# ADR-[NNN]: [Title]

**Date**: [date]
**Status**: [Proposed / Accepted / Deprecated / Superseded]
**Deciders**: [who]

## Context

[Why is this decision needed? What problem or situation prompted it?]

## Options Considered

### Option A: [Name]
- Pros: [list]
- Cons: [list]

### Option B: [Name]
- Pros: [list]
- Cons: [list]

## Decision

[Which option was chosen and WHY]

## Consequences

### Positive
- [What improves]

### Negative
- [What trade-offs we accept]

### Risks
- [What could go wrong]
```

### 3. Update Index

Add to technical preferences or architecture docs.

## Collaborative Protocol

- Present all options with honest pros/cons
- User makes the final decision
- Document the WHY, not just the WHAT
