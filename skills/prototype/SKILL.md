---
name: prototype
description: Rapid prototyping to validate a concept or mechanic. Throwaway code, relaxed standards, focused on learning fast.
---

# Prototype

Build a quick, throwaway prototype to validate an idea before committing
to full implementation. Standards are intentionally relaxed for speed.

## Usage

`/appbuilder-one:prototype [what-to-test]`

Example: `/appbuilder-one:prototype drag-and-drop kanban board`

## When to Prototype

- Unsure if a UX approach works → build it, try it
- Technical feasibility question → prove it works
- Choosing between approaches → build both, compare
- Stakeholder needs to see something → quick demo

## Rules

- **Throwaway code** — it will be deleted, not refactored
- **No tests** — speed over quality
- **Hardcoded data** — no real database
- **Minimal styling** — functional, not pretty
- **Single file if possible** — reduce complexity

## Workflow

### 1. Define the Hypothesis

Ask:
- What are you trying to validate?
- What's the minimum you need to build to answer the question?
- How will you know if it worked?

### 2. Build Fast

- Create in `prototypes/[name]/` directory
- Use the simplest possible approach
- Skip architecture, skip patterns, skip standards
- Get to "can I interact with it?" as fast as possible

### 3. Evaluate

- Does it answer the question?
- What did you learn?
- Go / pivot / kill decision

### 4. Document Learnings

Brief note in `prototypes/[name]/README.md`:
```markdown
# Prototype: [Name]

## Hypothesis
[What we were testing]

## Result
[What we learned]

## Decision
[GO: proceed to real implementation / PIVOT: try different approach / KILL: abandon]

## Notes for Implementation
[If GO: what to keep in mind when building it for real]
```

### 5. Clean Up

If GO: start fresh implementation using proper architecture.
**Never promote prototype code to production.**

## Collaborative Protocol

- Don't suggest tests or architecture — it's a prototype
- Build the minimum viable thing
- Focus on the question, not the code
- When done, ask: "Did this answer your question?"
