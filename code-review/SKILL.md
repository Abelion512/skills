---
name: code-review
description: >
  Code review skill for analyzing code quality, maintainability, and best
  practices. Use this skill when the user asks for a review of their own code
  before committing, or when reviewing someone else's code or PR. Provides
  structured feedback with severity levels and actionable suggestions.
  Covers both self-review and peer review scenarios.
---

# Code Review

Structured code review skill for TypeScript/React/Supabase projects.
Reviews are organized by category and severity, with actionable fixes.

## Severity Levels

- 🔴 **Critical** — Must fix before merge. Breaks functionality, security, or data integrity.
- 🟡 **Warning** — Should fix. Technical debt, maintainability risk, or bad practice.
- 🔵 **Suggestion** — Nice to have. Readability, performance, or style improvement.

## Review Categories

### 1. Type Safety
- Avoid `any` — use strict typing or generics
- Ensure function return types are explicit
- Validate external data (API responses, user input) before use

### 2. React Best Practices
- Components follow single responsibility principle
- Hooks used correctly (dependency arrays, cleanup in useEffect)
- State updates are immutable
- No unnecessary re-renders (useMemo, useCallback where needed)

### 3. Async & Error Handling
- Prefer `async/await` over raw Promises
- All async operations wrapped in try/catch
- Error states handled in UI (not just console.log)

### 4. Security Basics
- No sensitive data in client-side code or localStorage
- JWT stored in HTTP-only cookies, not localStorage
- User input sanitized before use (DOMPurify for HTML)
- Environment variables not exposed to client unnecessarily

### 5. Code Quality
- No dead code or commented-out blocks
- Functions do one thing only
- Variable names are descriptive, not abbreviated
- No magic numbers — use named constants

### 6. Supabase Specific
- RLS (Row Level Security) policies in place for all tables
- Queries use proper error handling (`const { data, error } = await supabase...`)
- No raw SQL in client code — use Supabase query builder

## Response Format

```
## Code Review — [filename or scope]

### Summary
[1-2 sentences: overall impression and main concerns]

---

### 🔴 Critical
[issue] — [why it matters] — [how to fix]

### 🟡 Warning
[issue] — [why it matters] — [how to fix]

### 🔵 Suggestion
[issue] — [why it matters] — [how to fix]

---

### ✅ What's Good
[Acknowledge what is done well — at least 1-2 points]

### Next Steps
[Prioritized list: fix criticals first, then warnings]
```

## Rules

- Always acknowledge what is done well before listing issues.
- Never rewrite the entire code unless explicitly asked.
- Suggest fixes with short code snippets where helpful.
- If scope is a full PR, review file by file.
- Respond in the same language the user writes in.

## Default Tech Stack Context

- **Frontend:** React + Vite + TypeScript + Tailwind CSS + shadcn/ui
- **Backend:** Supabase (PostgreSQL, Auth, Edge Functions)
- **Runtime:** Bun
- **State:** TanStack Query
- **Animation:** GSAP + Framer Motion
- **Deploy:** Vercel
