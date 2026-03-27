---
name: db-migrate
description: Manage database migrations. Create, apply, rollback, and check status. Supports Prisma, Drizzle, Alembic, Laravel, and raw SQL.
---

# Database Migrate

Manage database migrations across different ORMs and frameworks.

## Usage

`/appbuilder-one:db-migrate create [name]` — Create new migration
`/appbuilder-one:db-migrate apply` — Apply pending migrations
`/appbuilder-one:db-migrate rollback` — Rollback last migration
`/appbuilder-one:db-migrate status` — Show migration status
`/appbuilder-one:db-migrate seed` — Run seed data

## Auto-Detect ORM

Read project files to detect which ORM/migration tool is in use:

| Indicator | ORM | Commands |
|-----------|-----|----------|
| `prisma/schema.prisma` | Prisma | `npx prisma migrate` |
| `drizzle.config.ts` | Drizzle | `npx drizzle-kit` |
| `alembic.ini` | Alembic (Python) | `alembic` |
| `artisan` | Laravel | `php artisan migrate` |
| `supabase/` | Supabase | `supabase db` |

## Workflows

### Create Migration

1. Ask what changed (new entity, new field, relationship change)
2. Generate migration based on ORM:

**Prisma:**
```bash
# Edit schema.prisma first, then:
npx prisma migrate dev --name [name]
```

**Drizzle:**
```bash
npx drizzle-kit generate --name [name]
```

**Alembic:**
```bash
alembic revision --autogenerate -m "[name]"
```

**Laravel:**
```bash
php artisan make:migration [name]
```

**Supabase:**
```bash
supabase migration new [name]
```

3. Show the generated migration for review
4. Apply after approval

### Apply Migrations

```bash
# Prisma
npx prisma migrate deploy

# Drizzle
npx drizzle-kit push

# Alembic
alembic upgrade head

# Laravel
php artisan migrate

# Supabase
supabase db push
```

### Rollback

```bash
# Prisma — no built-in rollback, create reverse migration
npx prisma migrate dev --name rollback_[name]

# Drizzle
npx drizzle-kit drop

# Alembic
alembic downgrade -1

# Laravel
php artisan migrate:rollback

# Supabase
supabase db reset  # CAUTION: resets all data
```

### Status

Show pending and applied migrations.

### Seed Data

Generate or run seed data for development:
- Create seed files with realistic test data
- Run seed command for the ORM
- Idempotent seeds (safe to run multiple times)

## Safety Rules

- **ALWAYS show migration SQL before applying**
- **NEVER run destructive migrations without confirmation**
- **NEVER drop columns/tables without explicit user approval**
- Warn when migration might lock tables (large table ALTER)
- Suggest backing up before destructive changes
- For production: always use `migrate deploy` (not `dev`)
