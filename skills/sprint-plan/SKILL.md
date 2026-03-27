---
name: sprint-plan
description: Plan a sprint or iteration. Selects tasks from backlog, estimates capacity, sets goals, and tracks progress.
---

# Sprint Plan

Plan what to build in the next sprint/iteration.

## Usage

`/appbuilder-one:sprint-plan` — Create new sprint plan
`/appbuilder-one:sprint-plan review` — Review current sprint progress

## Modes

- **Learning**: No sprints — just a prioritized to-do list
- **Solo**: Light sprint (1-2 week cycles, personal goals)
- **Team/Enterprise**: Full sprint (capacity, velocity, commitments)

## Workflow

### 1. Gather Context

Read:
- Modules index — what's designed vs implemented
- Active epics and features — what's in progress
- Previous sprint (if exists) — what carried over
- Open tasks from `tasks.md` files

### 2. Determine Capacity

**Solo mode:**
> How many hours can you dedicate this week/sprint?
> (realistic — account for meetings, life, etc.)

**Team mode:**
> Team capacity:
> - [Person 1]: [hours available]
> - [Person 2]: [hours available]
> - Total: [hours]

### 3. Select Work

Present prioritized candidates:

```markdown
## Sprint Candidates

### Must Do (carry-over, blockers, bugs)
1. [Task/Feature] — [estimate] — [reason]

### Should Do (next in priority)
1. [Task/Feature] — [estimate]
2. [Task/Feature] — [estimate]

### Could Do (if time allows)
1. [Task/Feature] — [estimate]

### Total estimated: [hours] / [capacity] hours
```

User selects what goes into the sprint.

### 4. Create Sprint Plan

Save to `production/sprints/sprint-[N].md`:

```markdown
# Sprint [N]: [dates]

## Goal
[One sentence: what's the main outcome of this sprint?]

## Capacity
- Available: [hours]
- Committed: [hours] ([percentage]%)

## Committed Work

| # | Task/Feature | Estimate | Owner | Status |
|---|-------------|----------|-------|--------|
| 1 | [name] | [hours] | [who] | Not Started |
| 2 | [name] | [hours] | [who] | Not Started |

## Stretch Goals (if time allows)
- [item]

## Risks
- [risk and mitigation]

## Definition of Done
- [ ] All committed items complete
- [ ] Tests passing
- [ ] Code reviewed (team mode)
- [ ] Deployed to staging (if applicable)
```

### 5. Sprint Review

`/appbuilder-one:sprint-plan review` generates:

```markdown
## Sprint [N] Review

### Completed
- [item] — [actual vs estimate]

### Carried Over
- [item] — [reason]

### Unplanned Work
- [item] — [what happened]

### Velocity
- Planned: [X hours]
- Completed: [Y hours]
- Velocity: [Y/X]%

### Retrospective
- What went well: [ask user]
- What didn't: [ask user]
- Action items: [ask user]
```

## Collaborative Protocol

- User decides what goes into the sprint
- Estimates are suggestions, not commitments
- Flag if committed work exceeds capacity
- Review at end of sprint to improve estimates
