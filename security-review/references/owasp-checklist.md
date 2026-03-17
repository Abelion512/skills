# OWASP Security Checklist

> Loaded as context for security-review skill.
> Adapted from OWASP Top 10 for React + TypeScript + Supabase stack.

## A01 — Broken Access Control

- [ ] RLS (Row Level Security) enabled on ALL Supabase tables
- [ ] RLS policies tested — not just enabled
- [ ] `supabase.auth.getUser()` used to verify identity server-side
- [ ] Role-based access enforced at database level, not just UI
- [ ] API routes validate user permissions before returning data
- [ ] No direct object references exposed without authorization check

```typescript
// ✅ Always verify user server-side
const { data: { user }, error } = await supabase.auth.getUser()
if (!user) return { error: 'Unauthorized' }
```

## A02 — Cryptographic Failures

- [ ] HTTPS enforced in production (Vercel handles this)
- [ ] No sensitive data in URL parameters or logs
- [ ] Passwords never stored — use Supabase Auth
- [ ] JWT stored in HTTP-only cookies, not localStorage
- [ ] Sensitive fields encrypted at rest if needed (Supabase Vault)

## A03 — Injection

- [ ] Supabase query builder used (parameterized queries)
- [ ] No raw SQL string concatenation with user input
- [ ] User input validated with Zod before any query
- [ ] No `eval()` with user-controlled data

```typescript
// ✅ Parameterized via Supabase query builder
const { data } = await supabase
  .from('posts')
  .select()
  .eq('user_id', userId) // parameterized, safe

// ❌ Never do this
await supabase.rpc(`SELECT * FROM posts WHERE user_id = '${userId}'`)
```

## A05 — Security Misconfiguration

- [ ] No debug/development endpoints in production
- [ ] Error messages don't expose stack traces to users
- [ ] CORS configured to specific origins (not `*` in production)
- [ ] Security headers present (Vercel config or middleware)
- [ ] `.env` in `.gitignore` — never committed

```typescript
// Vercel: vercel.json security headers
{
  "headers": [
    {
      "source": "/(.*)",
      "headers": [
        { "key": "X-Content-Type-Options", "value": "nosniff" },
        { "key": "X-Frame-Options", "value": "DENY" },
        { "key": "Strict-Transport-Security", "value": "max-age=31536000" }
      ]
    }
  ]
}
```

## A06 — Vulnerable Components

- [ ] `bun audit` / `npm audit` run regularly
- [ ] Dependencies updated — no critical CVEs
- [ ] Unused dependencies removed

## A07 — Authentication Failures

- [ ] Supabase Auth used — no custom auth implementation
- [ ] JWT algorithm explicitly set (HS256) — never `none`
- [ ] Tokens have expiry set
- [ ] Refresh token rotation enabled in Supabase dashboard
- [ ] No hardcoded credentials anywhere in codebase

## A09 — Security Logging Failures

- [ ] Auth failures logged (Supabase handles this)
- [ ] No sensitive data in console.log (email, tokens, passwords)
- [ ] Error boundaries in React catch and log (not expose) errors

## XSS Specific

- [ ] No `dangerouslySetInnerHTML` without DOMPurify sanitization
- [ ] User-generated content sanitized before render
- [ ] CSP header configured if handling rich user content

```typescript
// ✅ Sanitize before dangerouslySetInnerHTML
import DOMPurify from 'dompurify'

function UserContent({ html }: { html: string }) {
  return (
    <div
      dangerouslySetInnerHTML={{
        __html: DOMPurify.sanitize(html)
      }}
    />
  )
}
```

## Supabase Env Variables

```bash
# ✅ Client-safe (public)
VITE_SUPABASE_URL=...
VITE_SUPABASE_ANON_KEY=...

# ❌ Never expose to client
SUPABASE_SERVICE_ROLE_KEY=...  # Server/Edge Functions only
```
