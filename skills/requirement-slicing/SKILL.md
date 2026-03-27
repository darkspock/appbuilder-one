---
name: requirement-slicing
description: Slice a large epic into independently deployable features with dependency mapping.
---

# Requirement Slicing

Slice a large epic into independently deployable features.

**Modes**: Solo (optional), Team (recommended), Enterprise (required for large epics)

## Usage

`/requirement-slicing [path-to-epic-folder]`

Example: `/requirement-slicing docs/working_docs/epics/reservation-system`

## When to Slice

**Slice when:**
- Epic exceeds 2-3 weeks of work
- Multiple developers can work in parallel
- Value can be delivered incrementally
- Risk can be reduced by staging delivery

**Don't slice when:**
- Epic is small and cohesive
- Requirements are atomic
- Same files would be changed across slices

## AI-Era Considerations

AI-assisted development changes slicing economics:

**Hidden cost of slicing:**
- Branch management: 15-30 min per feature
- Merge conflicts: 30 min - 2 hours
- Code review coordination: 1-4 hours per PR
- CI/CD runs: 15-45 min per deployment
- Integration testing: 1-2 hours after each merge

**Consider single-developer ownership when:**
- Epic completable in 1-2 weeks by one person with AI
- Cohesive domain (all features touch related code)
- Low external dependencies
- Clear requirements

## Slicing Rules

1. **Vertical slices** by user value, not technical layers
2. Each feature must be **independently deployable**
3. **No circular dependencies** between features
4. **No overlapping ownership** of the same entities
5. **Foundation work** (schemas, base classes) goes first

## Workflow

### 1. Read Epic

Read `requirements.md` and `validation.md` from the epic folder.

### 2. Identify Features

For each feature:
- Name
- Value delivered
- Dependencies on other features
- Risk level (Low/Medium/High)
- Estimated size (S/M/L/XL)

### 3. Determine Delivery Order

Map dependencies and determine parallel tracks.

### 4. Output

Write `slicing.md` to the epic folder:

```markdown
# Slicing: [Epic Name]

## Features

### Feature 1: [Name]
- **Value:** [What user value this delivers]
- **Dependencies:** None
- **Risk:** Low/Medium/High
- **Estimated Size:** S/M/L

### Feature 2: [Name]
- **Value:** [What user value]
- **Dependencies:** Feature 1
- **Risk:** Low/Medium/High
- **Estimated Size:** S/M/L

## Delivery Order

1. Feature 1 - Foundation
2. Feature 2 - [reason]
3. Features 3 & 4 - Can be parallel

## Feature Tracking

| Feature | Status | Staging Date | Prod Date |
|---------|--------|-------------|-----------|
| Feature 1 | Not Started | - | - |
| Feature 2 | Not Started | - | - |
```

### 5. Create Feature Folders

For each feature, create:
```
docs/working_docs/features/[feature-name]/
├── requirements.md    (extracted from epic)
```

Ask approval before creating.

## Collaborative Protocol

- Present slicing for review
- User approves feature boundaries
- Foundation features always go first
