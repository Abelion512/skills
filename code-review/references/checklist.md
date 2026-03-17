# Code Review Checklist

> Loaded as context for code-review skill.

## TypeScript & Type Safety

- [ ] No `any` type used
- [ ] All exported functions have explicit return types
- [ ] External data (API, user input) validated with Zod before use
- [ ] Union types preferred over boolean flags
- [ ] Generics used where appropriate instead of repetition

## React Best Practices (2025)

- [ ] Components follow single responsibility principle
- [ ] `useEffect` dependencies array is complete and correct
- [ ] `useEffect` has cleanup function if needed (subscriptions, timers)
- [ ] No unnecessary `useCallback` / `useMemo` (premature optimization)
- [ ] State updates are immutable (no direct mutation)
- [ ] Keys in lists are stable and unique (not array index)
- [ ] `useTransition` used for non-urgent state updates (React 19)
- [ ] `useOptimistic` considered for optimistic UI (React 19)

## Async & Error Handling

- [ ] All async operations have try/catch
- [ ] Error states are handled in UI (not just console.log)
- [ ] Loading states shown to user during async operations
- [ ] Race conditions handled (AbortController or TanStack Query)
- [ ] No unhandled Promise rejections

## Supabase Specific

- [ ] RLS policies exist for all queried tables
- [ ] `const { data, error } = await supabase...` pattern used
- [ ] `error` object checked before using `data`
- [ ] `supabase.auth.getUser()` used on server (not `getSession()`)
- [ ] Service role key only in Edge Functions, never client-side
- [ ] No raw SQL in client code

## Code Quality

- [ ] No dead code or commented-out blocks
- [ ] Functions do one thing only (< 50 lines as a guide)
- [ ] Variable names are descriptive
- [ ] No magic numbers — named constants used
- [ ] No console.log left in production code
- [ ] DRY — no copy-pasted logic (extract to utility/hook)

## Security Basics (Quick Check)

- [ ] No hardcoded credentials
- [ ] No sensitive data in `VITE_` env vars (only public values)
- [ ] JWT not stored in localStorage
- [ ] User input not rendered as raw HTML without sanitization

## Performance (Quick Check)

- [ ] Images have defined width/height (prevent layout shift)
- [ ] Heavy components lazy-loaded where appropriate
- [ ] No N+1 query patterns in Supabase calls
