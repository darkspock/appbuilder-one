# Deploy

Deployment management using GitHub as source of truth and `gh` CLI for
automation. Different strategies based on hosting choice.

## Prerequisites

- **GitHub**: All projects use GitHub for version control
- **`gh` CLI**: Required. Claude manages repos, PRs, releases, and actions via `gh`
- **Hosting CLI**: Depends on chosen stack (vercel, railway, fly, aws, hcloud, etc.)

## Usage

`/deploy` — Deploy current branch to staging/production
`/deploy setup` — Configure deployment pipeline for the first time
`/deploy staging` — Deploy to staging only
`/deploy production` — Deploy to production (with confirmation)
`/deploy status` — Check deployment status
`/deploy rollback` — Rollback to previous version

## Environments

| Environment | Purpose | Branch | Auto-deploy |
|-------------|---------|--------|-------------|
| **Preview** | Per-PR preview (if supported) | Feature branches | Yes (Vercel/Netlify) |
| **Staging** | Testing before production | `main` or `staging` | Configurable |
| **Production** | Live users | `main` + tag/release | Manual or auto |

## Deploy Strategies by Hosting

### Vercel (Next.js, SvelteKit, Nuxt)

**Setup** (`/deploy setup`):
```bash
# Link project
vercel link

# Set environment variables
vercel env add DATABASE_URL production
vercel env add DATABASE_URL preview

# Configure domains
vercel domains add myapp.com
```

**Deploy flow:**
- Push to GitHub → Vercel auto-deploys preview for PRs
- Merge to `main` → Vercel auto-deploys to production
- Manual: `vercel --prod`

**Claude can:**
- `vercel` — deploy
- `vercel env ls/add/rm` — manage env vars
- `vercel domains` — manage domains
- `vercel logs` — check logs
- `gh pr create` — create PR that triggers preview

### Railway

**Setup** (`/deploy setup`):
```bash
# Login and link
railway link

# Add database
railway add --plugin postgresql

# Set env vars
railway variables set DATABASE_URL=...
```

**Deploy flow:**
- Push to GitHub → Railway auto-deploys
- Manual: `railway up`

**Claude can:**
- `railway up` — deploy
- `railway logs` — check logs
- `railway variables` — manage env vars
- `railway add` — add services (DB, Redis)

### Hetzner VPS + Coolify

**Setup** (`/deploy setup`):
```bash
# Create VPS
hcloud server create --name myapp --type cx22 --image ubuntu-24.04

# Install Coolify on VPS
ssh root@[IP] 'curl -fsSL https://cdn.coollabs.io/coolify/install.sh | bash'

# Configure Coolify via API
# Add GitHub repository
# Configure build and deploy settings
```

**Deploy flow:**
- Push to GitHub → Coolify webhook → auto-deploy
- Or: Coolify API trigger

**Claude can:**
- `hcloud server` — manage VPS (create, resize, delete)
- `hcloud firewall` — manage firewall rules
- `hcloud network` — manage networks
- `ssh` — server management
- Coolify API — deploy, configure, logs

### Fly.io

**Setup** (`/deploy setup`):
```bash
# Create app
fly launch

# Add database
fly postgres create

# Set secrets
fly secrets set DATABASE_URL=...
```

**Deploy flow:**
- `fly deploy` — manual deploy
- GitHub Actions → `fly deploy` on push to main

**Claude can:**
- `fly deploy` — deploy
- `fly logs` — check logs
- `fly secrets` — manage secrets
- `fly scale` — scale instances
- `fly postgres` — manage database

### AWS (Enterprise)

**Setup** (`/deploy setup`):
```bash
# Configure AWS CLI
aws configure

# Create infrastructure (example for ECS + RDS)
aws rds create-db-instance --db-instance-identifier myapp-db ...
aws ecs create-cluster --cluster-name myapp
aws ecr create-repository --repository-name myapp
aws ecs create-service ...

# Or use CloudFormation / CDK
aws cloudformation deploy --template-file infra.yaml --stack-name myapp
```

**Deploy flow:**
- Build Docker image → Push to ECR → Update ECS service
- Or: GitHub Actions pipeline

**Claude can:**
- `aws ecs` — manage containers
- `aws rds` — manage databases
- `aws s3` — manage storage
- `aws cloudfront` — manage CDN
- `aws iam` — manage permissions
- `aws logs` — check CloudWatch logs
- `aws cloudformation` — infrastructure as code
- Basically everything. AWS CLI covers all services.

### Supabase (Backend)

**Setup** (`/deploy setup`):
```bash
# Link project
supabase link --project-ref [ref]

# Push migrations
supabase db push

# Deploy edge functions
supabase functions deploy [function-name]
```

**Deploy flow:**
- Migrations: `supabase db push`
- Edge functions: `supabase functions deploy`
- Frontend: via Vercel or other

**Claude can:**
- `supabase db push/pull/reset` — manage migrations
- `supabase functions deploy` — deploy edge functions
- `supabase secrets set` — manage secrets

### Docker (generic — any VPS)

**Setup** (`/deploy setup`):
```bash
# Create Dockerfile and docker-compose.yml
# Push to GitHub
# On server: clone and run
ssh user@server 'cd /app && git pull && docker compose up -d --build'
```

**Deploy flow:**
- SSH → git pull → docker compose up
- Or: GitHub Actions → SSH deploy

## GitHub Integration

All strategies use GitHub as the source. Common operations via `gh`:

```bash
# Create release
gh release create v1.0.0 --title "v1.0.0" --notes "First release"

# Create PR for review before deploy
gh pr create --title "Release v1.0.0" --body "..."

# Check CI status
gh run list
gh run view [run-id]

# View deployment status (if using GitHub Environments)
gh api repos/{owner}/{repo}/deployments
```

## GitHub Actions Templates

For Team/Enterprise, suggest creating `.github/workflows/`:

### CI Pipeline (all modes)
```yaml
# .github/workflows/ci.yml
# On PR: lint, test, build
```

### Deploy to Staging (Team/Enterprise)
```yaml
# .github/workflows/deploy-staging.yml
# On push to main: deploy to staging
```

### Deploy to Production (Team/Enterprise)
```yaml
# .github/workflows/deploy-production.yml
# On release tag: deploy to production
```

## Pre-Deploy Checklist

Before deploying, automatically run:

| Check | Command | Required |
|-------|---------|----------|
| Tests pass | `npm test` / `pytest` | All modes |
| Lint clean | `npm run lint` | Solo+ |
| Build succeeds | `npm run build` | All modes |
| Security scan | `/check-security` | Team+ |
| Performance check | `/check-performance` | Team+ |
| Env vars set | Check hosting provider | All modes |
| Migrations ready | Check pending migrations | All modes |

## Rollback

| Hosting | Rollback method |
|---------|----------------|
| Vercel | `vercel rollback` or redeploy previous commit |
| Railway | Redeploy previous commit via dashboard or CLI |
| Fly.io | `fly releases` → `fly deploy --image [previous]` |
| AWS ECS | Update service to previous task definition |
| Docker/VPS | `git checkout [previous] && docker compose up -d` |
| Supabase | `supabase db reset` (careful — destructive) |

## Collaborative Protocol

- **Production deploys always require explicit confirmation**
- Show pre-deploy checklist results before deploying
- For rollback, confirm before executing
- Never deploy with failing tests or security issues
- One environment at a time (staging first, then production)
