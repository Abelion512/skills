# Abelion Code Conventions

> Loaded as context for vibe-coding skill.

## TypeScript

- Always use strict mode (`"strict": true` in tsconfig)
- No `any` — use `unknown` + type guards, or generics
- Explicit return types on all exported functions
- Use `type` for unions/intersections, `interface` for object shapes

```typescript
// ✅ Good
interface UserProfile {
  id: string
  email: string
  role: 'admin' | 'user'
}

// ✅ Good
type ApiResponse<T> = {
  data: T | null
  error: string | null
}

// ❌ Bad
const doSomething = (data: any) => data
```

## React Components

- Functional components only — no class components
- One component per file
- Props interface named `[ComponentName]Props`
- Export at bottom of file (named export preferred)

```typescript
// ✅ Good
interface CardProps {
  title: string
  description?: string
  onClick?: () => void
}

export function Card({ title, description, onClick }: CardProps) {
  return (...)
}
```

## File Naming

| Type | Convention | Example |
|---|---|---|
| Component | PascalCase | `UserCard.tsx` |
| Hook | camelCase with `use` prefix | `useAuth.ts` |
| Utility | camelCase | `formatDate.ts` |
| Types | camelCase | `types.ts` or `user.types.ts` |
| Page | camelCase (Next.js) / PascalCase | `dashboard.tsx` |

## Folder Structure

```
src/
├── components/     # Reusable UI components
│   └── ui/         # shadcn/ui components
├── hooks/          # Custom React hooks
├── lib/            # Utilities, helpers
├── types/          # TypeScript type definitions
├── contexts/       # React contexts
├── pages/          # Route pages
└── integrations/   # Supabase client, external services
```

## Tailwind CSS 4

- Use CSS variables for theme values
- Prefer composition over custom classes
- Dark mode via `dark:` prefix

```css
/* tailwind.config approach is gone in v4 */
/* Use @theme in CSS instead */
@import "tailwindcss";

@theme {
  --color-brand: oklch(0.7 0.15 200);
}
```

## Error Handling

- All async operations in try/catch
- User-facing errors go to toast/notification
- Technical errors go to console.error (dev only)
- Never expose stack traces to users

```typescript
try {
  const { data, error } = await supabase.from('users').select()
  if (error) throw error
  return data
} catch (err) {
  console.error('Failed to fetch users:', err)
  toast.error('Something went wrong. Please try again.')
}
```
