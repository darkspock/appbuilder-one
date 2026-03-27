# Check Security

Scan the codebase for security vulnerabilities and bad practices.
Adapts depth based on project mode.

## Usage

`/check-security` — Full scan
`/check-security [path]` — Scan specific file or directory

## Checks by Mode

### Learning Mode (basics)

1. **Secrets in code**
   - Scan for hardcoded API keys, passwords, tokens
   - Check `.env` files are in `.gitignore`
   - Tools: `grep` for patterns (API_KEY, SECRET, PASSWORD, token)

2. **SQL Injection**
   - Check for string concatenation in queries
   - Verify parameterized queries / ORM usage

3. **XSS**
   - Check for unsanitized user input in HTML output
   - Verify framework's auto-escaping is active

4. **.env exposure**
   - Verify `.env` is gitignored
   - Check no `.env` files are committed (`git log` check)

### Solo Mode (+ intermediate)

All Learning checks, plus:

5. **Dependency vulnerabilities**
   - Run `npm audit` / `pip audit` / `bundle audit`
   - Flag critical and high severity

6. **Auth bypass**
   - Check all API routes have auth middleware
   - Verify protected routes in frontend

7. **CORS configuration**
   - Check CORS settings aren't `*` in production
   - Verify allowed origins are explicit

8. **Security headers**
   - Check for: X-Content-Type-Options, X-Frame-Options,
     Content-Security-Policy, Strict-Transport-Security
   - Can test with `curl -I` against deployed app

9. **Rate limiting**
   - Check if auth endpoints have rate limiting
   - Check if API has general rate limiting

### Team Mode (+ advanced)

All Solo checks, plus:

10. **OWASP Top 10 scan**
    - Broken Access Control
    - Cryptographic Failures
    - Injection (SQL, NoSQL, OS, LDAP)
    - Insecure Design
    - Security Misconfiguration
    - Vulnerable Components
    - Auth Failures
    - Data Integrity Failures
    - Logging & Monitoring Failures
    - SSRF

11. **Input validation**
    - Check all API endpoints validate input
    - Verify validation on both client and server

12. **Error information leakage**
    - Check error responses don't expose stack traces
    - Verify generic error messages for users

13. **File upload security** (if applicable)
    - File type validation
    - Size limits
    - Storage outside webroot

### Enterprise Mode (+ compliance)

All Team checks, plus:

14. **GDPR data handling**
    - Personal data identified and classified
    - Deletion/anonymization capability exists
    - Consent tracking in place
    - Data export capability

15. **Audit logging**
    - Sensitive operations logged
    - Log tampering prevention
    - Retention policy in place

16. **Encryption**
    - Data at rest encryption
    - TLS for all connections
    - Sensitive fields encrypted in DB

17. **Session management**
    - Token expiration configured
    - Refresh token rotation
    - Session invalidation on password change

## Tools Used

| Check | Tool/Method | Auto-run |
|-------|------------|----------|
| Secrets in code | `grep` patterns, `gitleaks` (if installed) | Yes |
| Dependencies | `npm audit` / `pip audit` | Yes |
| Security headers | `curl -I [url]` | If deployed |
| OWASP patterns | Code analysis (grep + read) | Yes |
| Git history secrets | `git log --all -p \| grep` patterns | Yes |

## Output

Generate `security-report.md` with:

```markdown
# Security Report — [Date]

## Summary
- Critical: [N]
- High: [N]
- Medium: [N]
- Low: [N]

## Findings

### [CRITICAL] Finding title
- **File**: [path:line]
- **Issue**: [description]
- **Fix**: [how to fix]
- **OWASP**: [category if applicable]

### [HIGH] Finding title
...
```

## Collaborative Protocol

- Report findings, don't auto-fix without approval
- For critical findings, stop and alert immediately
- Offer to fix each finding one by one
- Never expose actual secrets in the report
