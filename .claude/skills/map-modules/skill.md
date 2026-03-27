# Map Modules

Decompose a product concept into individual modules, map dependencies,
prioritize design order, and create the modules index.

## Workflow

### Phase 1: Read Concept

- Read `design/product/product-concept.md` — fail if missing
- Read `design/product/modules-index.md` if exists (resume)

### Phase 2: Module Enumeration

Extract all modules the app needs. Categories:

| Category | Examples |
|----------|---------|
| **Core** | Auth, users, permissions, settings, notifications |
| **Domain** | The business-specific modules (invoices, projects, tickets...) |
| **Data** | Database schema, migrations, seed data |
| **API** | REST/GraphQL endpoints, middleware, validation |
| **UI** | Layout, navigation, forms, tables, dashboards |
| **Infrastructure** | Email, file storage, background jobs, caching |
| **Admin** | User management, system config, audit logs |

For each module: name, category, description, explicit vs inferred.
Present to user for review.

### Phase 3: Dependency Mapping

Map dependencies in layers:
1. **Foundation**: Auth, database, config (zero dependencies)
2. **Core**: User management, permissions (depend on foundation)
3. **Domain**: Business modules (depend on core)
4. **Presentation**: UI components, pages (depend on domain)
5. **Polish**: Analytics, notifications, admin tools

### Phase 4: Priority Assignment

- **MVP**: Minimum modules for the core workflow to work
- **V1**: Complete the primary user experience
- **V2**: Secondary workflows, admin tools
- **Full Vision**: Analytics, advanced features, integrations

### Phase 5: Create Modules Index

Write to `design/product/modules-index.md` with:
- Enumeration table
- Dependency map
- Recommended design order
- Progress tracker

Ask approval before writing.

### Phase 6: Design Individual Modules

Hand off to `/design-module [module-name]` when user is ready.

## Collaborative Protocol

- Present enumeration for review before proceeding
- User approves dependencies and priorities
- Ask before writing any file
- One decision at a time
