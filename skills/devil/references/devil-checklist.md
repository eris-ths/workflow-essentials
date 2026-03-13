# Devil's Advocate — Security Checklist

Full checklist used by `/devil` during security review.

## OWASP Top 10 (2021) Mapping

### A01: Broken Access Control
- [ ] Endpoints enforce authentication
- [ ] Authorization checks on resource access (IDOR prevention)
- [ ] Directory traversal prevention on file paths
- [ ] CORS properly configured

### A02: Cryptographic Failures
- [ ] No secrets in source code (API keys, passwords, tokens)
- [ ] No secrets in logs or error messages
- [ ] HTTPS enforced for external communication
- [ ] Sensitive data not stored in plain text

### A03: Injection
- [ ] SQL: Parameterized queries / ORM (no string concatenation)
- [ ] Command: No shell execution with user input (or proper escaping)
- [ ] Path: User input not used in file paths (or validated)
- [ ] Template: No unescaped user input in templates

### A04: Insecure Design
- [ ] Input validation at system boundaries
- [ ] Rate limiting on public endpoints
- [ ] Fail-safe defaults (deny by default)

### A05: Security Misconfiguration
- [ ] Debug mode disabled in production
- [ ] Default credentials changed
- [ ] Error messages don't leak stack traces
- [ ] Unnecessary features/endpoints disabled

### A06: Vulnerable Components
- [ ] Dependencies up to date (no known CVEs)
- [ ] Lock file committed (package-lock.json, etc.)

### A07: Authentication Failures
- [ ] Password/token comparison uses constant-time comparison
- [ ] Session tokens are sufficiently random
- [ ] Failed login doesn't reveal user existence

### A08: Data Integrity Failures
- [ ] Deserialization of untrusted data is validated
- [ ] CI/CD pipeline integrity maintained

### A09: Logging Failures
- [ ] Security events are logged
- [ ] Logs don't contain sensitive data
- [ ] Log injection prevented

### A10: SSRF
- [ ] Server-side requests validate destination (no internal network access)
- [ ] URL schemes restricted (https only)
- [ ] Redirect targets validated
