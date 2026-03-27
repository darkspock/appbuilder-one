# Check Performance

Analyze the codebase and deployed app for performance issues.
Adapts depth based on project mode.

## Usage

`/check-performance` — Full scan
`/check-performance [path]` — Scan specific file or directory
`/check-performance --deployed [url]` — Test deployed app

## Checks by Mode

### Learning Mode (basics)

1. **N+1 Queries**
   - Scan ORM code for queries inside loops
   - Check for missing `include`/`join`/`prefetch_related`
   - Method: Code analysis (grep + read patterns)

2. **Missing pagination**
   - Check API endpoints that return lists
   - Verify they accept page/limit params
   - Flag any `findAll()` without limits

3. **Large images**
   - Check for unoptimized images in `public/` or `static/`
   - Flag images > 500KB
   - Suggest next/image or similar optimization

4. **Bundle size** (frontend)
   - Run `npx vite-bundle-visualizer` or equivalent
   - Flag bundles > 500KB
   - Check for heavy imports (moment.js, lodash full)

### Solo Mode (+ intermediate)

All Learning checks, plus:

5. **Missing database indexes**
   - Read migration files / schema
   - Check columns used in WHERE, ORDER BY, JOIN
   - Flag columns queried often without indexes

6. **Lazy loading**
   - Check frontend routes are lazy-loaded
   - Check images use lazy loading
   - Check heavy components are code-split

7. **Caching opportunities**
   - Identify static data fetched repeatedly
   - Suggest caching for: API responses, computed values, static assets
   - Check cache headers on API responses

8. **API response size**
   - Check for over-fetching (returning full objects when partial needed)
   - Suggest field selection / DTOs
   - Check for unnecessary nested data

### Team Mode (+ advanced)

All Solo checks, plus:

9. **Lighthouse audit** (if deployed)
   - Run `npx lighthouse [url] --output json`
   - Extract: Performance, LCP, FID, CLS scores
   - Flag anything below 90

10. **API response times**
    - Check for slow endpoints (complex queries, no caching)
    - Identify synchronous operations that should be async
    - Flag any computation > 100ms in request path

11. **Memory leaks** (frontend)
    - Check for missing cleanup in useEffect
    - Check for event listeners not removed
    - Check for growing state (unbounded arrays/maps)

12. **Database query analysis**
    - Check for SELECT * usage
    - Check for missing WHERE clauses on UPDATE/DELETE
    - Identify queries that could use views or materialized views
    - Check connection pooling configuration

13. **Render performance** (frontend)
    - Check for missing React.memo on list items
    - Check for missing useMemo/useCallback in providers
    - Check for context re-renders (split contexts by update frequency)

### Enterprise Mode (+ production)

All Team checks, plus:

14. **Load testing recommendations**
    - Identify critical paths for load testing
    - Suggest `k6` or `artillery` test scripts
    - Define performance budgets per endpoint

15. **CDN configuration**
    - Check static assets served from CDN
    - Verify cache headers (Cache-Control, ETag)
    - Check compression (gzip/brotli)

16. **Database connection pooling**
    - Check pool size configuration
    - Verify connection timeout settings
    - Check for connection leaks

17. **APM readiness**
    - Check if monitoring/tracing is set up
    - Suggest: Sentry, DataDog, New Relic, or open-source (Grafana)
    - Check error tracking configuration

18. **Auto-scaling readiness**
    - Check app is stateless (no local file storage, no in-memory sessions)
    - Verify health check endpoints exist
    - Check graceful shutdown handling

## Tools Used

| Check | Tool/Method | Auto-run |
|-------|------------|----------|
| N+1 queries | Code pattern analysis | Yes |
| Bundle size | `npx vite-bundle-visualizer` | If available |
| Lighthouse | `npx lighthouse` | If deployed |
| Image size | `find + ls -la` | Yes |
| DB indexes | Schema analysis | Yes |
| Dependencies | `npm ls --all` / `pip list` | Yes |
| Response times | `curl -w` timing | If deployed |

## Output

Generate `performance-report.md` with:

```markdown
# Performance Report — [Date]

## Summary
- Critical: [N] (will cause visible user impact)
- Warning: [N] (will cause issues at scale)
- Suggestion: [N] (optimization opportunities)

## Findings

### [CRITICAL] N+1 query in UserController
- **File**: src/controllers/users.ts:45
- **Issue**: Query inside loop fetching related data
- **Impact**: O(n) queries instead of O(1)
- **Fix**: Use `include` / `join` to eager-load

### [WARNING] Missing index on orders.customer_id
- **File**: migrations/003_orders.sql
- **Issue**: customer_id used in WHERE but not indexed
- **Impact**: Full table scan on customer lookups
- **Fix**: `CREATE INDEX idx_orders_customer_id ON orders(customer_id)`

### [SUGGESTION] Bundle includes full lodash
- **File**: package.json
- **Issue**: `lodash` (71KB) imported, only `debounce` used
- **Impact**: Unnecessary 70KB in bundle
- **Fix**: `npm install lodash.debounce` and import specifically
```

## Performance Budgets

Suggest default budgets based on mode:

| Metric | Learning | Solo | Team | Enterprise |
|--------|----------|------|------|------------|
| LCP | < 4s | < 2.5s | < 2s | < 1.5s |
| FID | < 300ms | < 100ms | < 100ms | < 50ms |
| CLS | < 0.25 | < 0.1 | < 0.1 | < 0.05 |
| API P95 | < 2s | < 500ms | < 300ms | < 200ms |
| Bundle | < 1MB | < 500KB | < 300KB | < 200KB |
| TTI | < 5s | < 3s | < 2s | < 1.5s |

## Collaborative Protocol

- Report findings with severity and impact
- Offer to fix each finding one by one
- For critical items (N+1, missing index), suggest immediate fix
- For suggestions, let user decide priority
