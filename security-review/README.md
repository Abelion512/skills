# security-review

> Web application security audit skill based on OWASP guidelines.

## What This Skill Does

Audits code for common security vulnerabilities including:
- XSS (Cross-Site Scripting)
- Injection attacks
- Authentication & session flaws
- Sensitive data exposure
- CORS misconfiguration
- Input validation gaps

Specialized reviews (cryptography, steganography) handled in extended skills.

## When to Use

| Scenario | Use |
|---|---|
| Review a specific component for vulnerabilities | `SKILL.md` |
| Pre-deployment security check | `SKILL.agent.md` |
| Full codebase security audit | `SKILL.agent.md` |
| After adding new auth/API features | `SKILL.md` |

## Files

| File | Purpose |
|---|---|
| `SKILL.md` | Guided security review |
| `SKILL.agent.md` | Autonomous full audit |
| `references/owasp-checklist.md` | OWASP Top 10 adapted for Abelion stack |
| `references/supabase-security.md` | Supabase-specific security patterns |

## Severity Guide

| Level | Meaning | Action |
|---|---|---|
| 🔴 Critical | Active exploit risk | Do not ship. Fix immediately. |
| 🟡 Warning | Potential vulnerability | Fix before production |
| 🔵 Suggestion | Hardening | Reduces attack surface |

## References

- [OWASP Top 10](https://owasp.org/www-project-top-ten/)
- [OWASP Cheat Sheet Series](https://cheatsheetseries.owasp.org/)
- [Supabase Security Guide](https://supabase.com/docs/guides/auth/security)
