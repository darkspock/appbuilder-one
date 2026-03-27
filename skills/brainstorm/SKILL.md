---
name: brainstorm
description: Product ideation — from zero idea to a structured product concept document for SaaS and management apps.
---

# Product Brainstorm

Guided product ideation — from zero idea to a structured product concept document.

## Workflow

### Phase 1: Discovery

Understand the person and the problem. Ask ONE question at a time:

**Problem space**:
- What problem are you trying to solve? Who has this problem?
- How is this problem solved today? (spreadsheets, manual process, existing tools)
- What's frustrating about the current solutions?

**User understanding**:
- Who are the main users? (roles, technical level, frequency of use)
- What does a typical day look like for them without this tool?
- How many users do you expect? (10, 100, 10000+)

**Practical constraints**:
- Solo developer or team?
- Timeline: weeks, months?
- Budget for infrastructure?
- Any compliance requirements? (GDPR, industry-specific)

**Synthesize** into a **Product Brief** — 3-5 sentences covering the problem,
target users, and constraints. Confirm with user.

### Phase 2: Concept Generation

Generate **3 distinct product approaches** that each solve the problem differently:

For each concept, present:
- **Working Name**
- **One-line pitch**
- **Core workflow** (the #1 thing users do daily)
- **Key differentiator** (why this over existing tools)
- **Target user** (primary persona)
- **Estimated scope** (small / medium / large)
- **Biggest risk**

### Phase 3: Core Workflows

For the chosen concept, define the main workflows:

- **Primary workflow**: The thing users do most (e.g., create invoice, log ticket)
- **Secondary workflows**: Supporting actions (e.g., generate report, manage users)
- **Admin workflows**: Setup and configuration (e.g., invite team, set permissions)

For each workflow: trigger → steps → outcome → frequency

### Phase 4: User Roles & Permissions

Define who can do what:
- List all user roles
- For each role: what they can see, create, edit, delete
- Permission model: simple (admin/user) or complex (RBAC)

### Phase 5: Product Principles

3-5 principles that guide every decision:
- Each has a name, definition, and design test
- Anti-principles: what this product is NOT

### Phase 6: Scope and MVP

- **MVP definition**: minimum set of features to test "does this solve the problem?"
- **Scope tiers**: MVP → V1 → V2 → Full Vision
- **Biggest risks**: technical, product-market fit, adoption

### Output

Generate product concept document using template at
`.claude/docs/templates/product-concept.md`.

Save to `design/product/product-concept.md`.

Suggest next steps:
1. `/setup-stack` — configure the technology
2. `/map-modules` — decompose into modules
3. `/design-module` — design individual modules
4. `/prototype` — scaffold the MVP
5. `/sprint-plan` — plan the first sprint

## Collaborative Protocol

- One question at a time
- Question -> Options -> Decision -> Draft -> Approval
- Never auto-generate the full concept without review
- User decides direction at every fork
