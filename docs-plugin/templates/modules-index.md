# Modules Index: [Product Name]

> **Status**: [Draft / Under Review / Approved]
> **Created**: [Date]
> **Last Updated**: [Date]
> **Source Concept**: design/product/product-concept.md

---

## Overview

[One paragraph explaining the product's modular scope.]

---

## Modules Enumeration

| # | Module Name | Category | Priority | Status | Design Doc | Depends On |
|---|-------------|----------|----------|--------|------------|------------|
| 1 | [e.g., Auth] | Core | MVP | Not Started | — | — |

---

## Categories

| Category | Description |
|----------|-------------|
| **Core** | Foundation modules: auth, users, permissions, settings |
| **Domain** | Business-specific modules: the actual product features |
| **Data** | Database schema, migrations, seed data |
| **API** | Endpoints, middleware, validation |
| **UI** | Layout, navigation, shared components, pages |
| **Infrastructure** | Email, file storage, background jobs |
| **Admin** | User management, system config, audit logs |

---

## Dependency Map

### Foundation Layer (no dependencies)
1. [Module] — [rationale]

### Core Layer (depends on foundation)
1. [Module] — depends on: [list]

### Domain Layer (depends on core)
1. [Module] — depends on: [list]

### Presentation Layer (depends on domain)
1. [Module] — depends on: [list]

### Polish Layer
1. [Module] — depends on: [list]

---

## Recommended Design Order

| Order | Module | Priority | Layer | Est. Effort |
|-------|--------|----------|-------|-------------|
| 1 | [First module] | MVP | Foundation | [S/M/L] |

---

## Progress Tracker

| Metric | Count |
|--------|-------|
| Total modules identified | [N] |
| Design docs started | [N] |
| Design docs approved | [N] |
| MVP modules designed | [N/total] |

---

## Next Steps

- [ ] Design MVP-tier modules (`/design-module [name]`)
- [ ] Prototype the core workflow (`/prototype`)
- [ ] Plan first sprint (`/sprint-plan`)
