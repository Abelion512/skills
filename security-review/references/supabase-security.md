# Supabase Security Reference

> Loaded as context for security-review skill.

## RLS (Row Level Security)

RLS is the most critical security layer. Every table must have it enabled.

```sql
-- Enable RLS on a table
ALTER TABLE posts ENABLE ROW LEVEL SECURITY;

-- Basic policy: users can only see their own data
CREATE POLICY "Users can view own posts"
ON posts FOR SELECT
USING (auth.uid() = user_id);

-- Insert policy
CREATE POLICY "Users can create own posts"
ON posts FOR INSERT
WITH CHECK (auth.uid() = user_id);

-- Update policy
CREATE POLICY "Users can update own posts"
ON posts FOR UPDATE
USING (auth.uid() = user_id);
```

## Auth Patterns

```typescript
// Always verify user server-side
const { data: { user }, error } = await supabase.auth.getUser()
// getUser() verifies with Supabase server — more secure

// Client-side only — DO NOT use for authorization decisions
const { data: { session } } = await supabase.auth.getSession()
// getSession() reads from local storage — can be spoofed
```

## Service Role Key

```typescript
// Only in Edge Functions (server-side)
import { createClient } from '@supabase/supabase-js'

const supabaseAdmin = createClient(
  process.env.SUPABASE_URL!,
  process.env.SUPABASE_SERVICE_ROLE_KEY!, // Never expose to client
)

// Never in client-side code
// const badClient = createClient(url, process.env.VITE_SERVICE_ROLE_KEY)
```

## Edge Function Security

```typescript
// Always validate request in Edge Functions
Deno.serve(async (req) => {
  // 1. Verify auth header
  const authHeader = req.headers.get('Authorization')
  if (!authHeader) return new Response('Unauthorized', { status: 401 })

  // 2. Verify JWT via Supabase
  const supabase = createClient(url, anonKey, {
    global: { headers: { Authorization: authHeader } }
  })
  const { data: { user }, error } = await supabase.auth.getUser()
  if (error || !user) return new Response('Unauthorized', { status: 401 })

  // 3. Process request safely
})
```

## Environment Variables

```bash
# Client-safe (public) — OK to expose via VITE_
VITE_SUPABASE_URL=...
VITE_SUPABASE_ANON_KEY=...

# Never expose to client — server/Edge Functions only
SUPABASE_SERVICE_ROLE_KEY=...
```

## Common Supabase Security Mistakes

| Mistake | Risk | Fix |
|---|---|---|
| RLS disabled | Anyone can read/write all data | Enable RLS + add policies |
| Using `getSession()` for auth | Session can be spoofed | Use `getUser()` instead |
| Service role key in client | Full database access exposed | Move to Edge Functions only |
| No expiry on tokens | Stolen tokens valid forever | Enable token rotation in dashboard |
| Anon key treated as secret | It is public by design | Use RLS to protect data, not the key |
