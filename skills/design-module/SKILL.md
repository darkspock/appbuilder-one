---
name: design-module
description: Guided section-by-section design document authoring for a single app module.
---

# Design Module

Guided, section-by-section design document authoring for a single app module.

## Arguments

Required: module name (e.g., `/design-module auth`, `/design-module invoices`)

## Workflow

### 1. Gather Context

- Read `design/product/product-concept.md`
- Read `design/product/modules-index.md`
- Read dependency module GDDs if they exist
- Read existing GDD for this module if resuming

### 2. Present Context Summary

> **Designing: [Module Name]**
> - Priority: [from index] | Layer: [from index]
> - Depends on: [list]
> - Depended on by: [list]
> - Principle alignment: [which product principle this serves]

### 3. Create File Skeleton

Create `design/product/[module-name].md` with all 8 section headers.

### 4. Section-by-Section Design

Walk through each section. For each: Context → Questions → Options → Decision → Draft → Approval → Write.

#### Section 1: Overview
One paragraph explaining what this module does and why it exists.

#### Section 2: User Story
Who benefits and how. Format: "As a [role], I want to [action] so that [benefit]."
List primary and secondary user stories.

#### Section 3: Detailed Design
- **Core Rules**: Business logic, workflows step by step
- **States and Transitions**: If the module has states (e.g., invoice: draft → sent → paid → overdue)
- **Interactions**: How this module connects to others (data flow, events)

#### Section 4: Data Model
- Entities with fields, types, constraints
- Relationships (one-to-many, many-to-many)
- Indexes needed
- Example data

#### Section 5: API Design
- Endpoints: method, path, request body, response, auth required
- Validation rules
- Error responses
- Pagination if applicable

#### Section 6: Edge Cases
- What happens at boundaries (empty state, max records, concurrent edits)
- Permission edge cases
- Data integrity scenarios

#### Section 7: Configuration
- Configurable values (limits, thresholds, feature flags)
- Environment variables needed
- Safe ranges and defaults

#### Section 8: Acceptance Criteria
- Testable conditions that prove the module works
- Performance requirements (response time, max load)
- Security requirements

### 5. Post-Design

- Update modules index status
- Suggest next module or `/code-review`

## Collaborative Protocol

- One section at a time
- Draft → Approval → Write for every section
- Cross-reference existing module GDDs for conflicts
- Never write without user approval
