---
name: security-review
description: >
  Security review skill for identifying common web application vulnerabilities.
  Use this skill when the user wants to audit their code for security issues.
  Covers OWASP Top 10 essentials: XSS, injection, auth flaws, insecure data
  handling, CORS misconfiguration, and environment variable exposure.
  Start with common vulnerabilities; specialized reviews (crypto, steganography)
  are handled in separate extended skills.
---

# Security Review

Security audit skill based on OWASP guidelines, adapted for the Abelion stack
(React + TypeScript + Supabase). Reviews are categorized by threat type and
severity.

## Severity Levels

- 🔴 **Critical** — Active security risk. Fix immediately, do not ship.
- 🟡 **Warning** — Potential vulnerability. Fix before production.
- 🔵 **Suggestion** — Hardening improvement. Reduces attack surface.

## Review Categories

### 1. XSS (Cross-Site Scripting)
- No raw `dangerouslySetInnerHTML` without sanitization
- User input sanitized with DOMPurify before rendering as HTML
- No dynamic `eval()` or `Function()` with user data
- Content Security Policy (CSP) header configured

### 2. Injection
- No string concatenation in queries — use parameterized queries
- Supabase query builder used (not raw SQL in client code)
- User input validated before use in any query or command
- No `eval()` with user-controlled data

### 3. Authentication & Session
- JWT stored in HTTP-only cookies, never localStorage or sessionStorage
- JWT signed with explicit algorithm (e.g., HS256) — never `none`
- Tokens have expiry (`expiresIn`)
- Supabase Auth RLS policies enforced on all tables
- No hardcoded credentials anywhere in code

### 4. Sensitive Data Exposure
- No API keys, secrets, or passwords in client-side code
- `.env` files not committed to git (check `.gitignore`)
- Only `VITE_` prefixed variables exposed to client — everything else server-side
- No sensitive data in `console.log` or error messages shown to user
- Supabase `anon` key used on client — `service_role` key only on server/edge functions

### 5. CORS & Headers
- CORS configured to specific origins — not wildcard `*` in production
- Security headers present: `X-Content-Type-Options`, `X-Frame-Options`,
  `Strict-Transport-Security`
- API routes validate `Content-Type`

### 6. Input Validation
- All user input validated on server side — client validation is UX only
- File uploads validated by type and size
- URL parameters sanitized before use

### 7. Dependency & Environment
- No known vulnerable packages (`npm audit`)
- Node.js version pinned in deployment config
- No development dependencies in production build

## Response Format

```
## Security Review — [filename or scope]

### Summary
[1-2 sentences: overall security posture and main concerns]

---

### 🔴 Critical
[vulnerability] — [attack scenario] — [fix]

### 🟡 Warning
[vulnerability] — [risk] — [fix]

### 🔵 Suggestion
[hardening] — [benefit] — [how]

---

### ✅ What's Secure
[Acknowledge good security practices found]

### Priority Fixes
[Top 3 most urgent items to address]
```

## Rules

- Always explain the attack scenario for Critical issues — not just "this is bad".
- Provide concrete fix with code snippet where possible.
- Never expose or log sensitive data found during review.
- If no issues found in a category, skip it — do not pad the report.
- Respond in the same language the user writes in.

## Default Tech Stack Context

- **Frontend:** React + Vite + TypeScript + Tailwind CSS + shadcn/ui
- **Backend:** Supabase (PostgreSQL, Auth, Edge Functions, RLS)
- **Runtime:** Bun
- **Auth:** Supabase Auth (JWT, HTTP-only cookies)
- **Deploy:** Vercel
