# OWASP Security Checklist (Web)

## A01: Broken Access Control
- [ ] Enforce RLS on all Supabase tables.
- [ ] Validate user permissions on server/Edge functions.
- [ ] Deny by default.

## A02: Cryptographic Failures
- [ ] Use HTTPS everywhere.
- [ ] No hardcoded keys/secrets.
- [ ] Salt & Hash passwords (Supabase handles this).

## A03: Injection
- [ ] Use parameterized queries (Supabase JS client does this automatically).
- [ ] Validate all inputs against a schema (Zod).

## A04: Insecure Design
- [ ] Rate limit API endpoints.
- [ ] Threat model critical flows.

## A05: Security Misconfiguration
- [ ] Production build settings (no debug mode).
- [ ] Correct CORS headers.
- [ ] Security headers (CSP, HSTS).

## A07: Identification and Authentication Failures
- [ ] Use Supabase Auth (don't roll your own).
- [ ] Enforce strong passwords or magic links.
- [ ] Implement MFA where possible.
