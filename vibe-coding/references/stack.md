# Abelion Default Tech Stack Reference

> Loaded as context for vibe-coding skill. Updated: 2026.

## Runtime & Package Manager

| Tool | Version | Notes |
|---|---|---|
| Bun | 1.x latest | Primary runtime & package manager |
| Node.js | 22 LTS | Fallback / CI compatibility |

## Frontend

| Tool | Version | Notes |
|---|---|---|
| React | 19 | Concurrent features, use `useTransition`, `useDeferredValue` |
| Vite | 6 | Build tool, dev server |
| TypeScript | 5.x | Strict mode always on |
| Tailwind CSS | 4 | New CSS-first config (no tailwind.config.js) |
| shadcn/ui | latest | Component library — add via `bunx shadcn add` |

## State & Data

| Tool | Version | Notes |
|---|---|---|
| TanStack Query | 5 | Server state, caching |
| Zustand | 5 | Client state (if needed) |
| React Hook Form | 7 | Form state + validation |
| Zod | 3 | Schema validation |

## Backend

| Tool | Version | Notes |
|---|---|---|
| Supabase | latest | PostgreSQL + Auth + Edge Functions + RLS |
| Supabase JS | 2 | `@supabase/supabase-js` |

## Animation

| Tool | Notes |
|---|---|
| GSAP 3 | Complex animations, scroll effects |
| Framer Motion 11 | Component-level transitions |

## Deployment

| Tool | Notes |
|---|---|
| Vercel | Primary deployment platform |
| Supabase | Database + Auth hosting |

## Key Patterns

```typescript
// Supabase query pattern
const { data, error } = await supabase
  .from('table')
  .select('*')
  .eq('user_id', user.id)

// TanStack Query pattern
const { data, isLoading } = useQuery({
  queryKey: ['key', id],
  queryFn: () => fetchData(id),
})

// Zod + React Hook Form
const schema = z.object({
  email: z.string().email(),
})
const form = useForm<z.infer<typeof schema>>({
  resolver: zodResolver(schema),
})
```
