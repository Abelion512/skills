---
name: code-review-agent
description: >
  Agentic code review skill. Autonomously reviews all files in a given scope
  and produces a complete structured review report without step-by-step
  confirmation. Best for reviewing an entire folder, module, or PR diff.
---

# Code Review — Agent Mode

Reviews all files in scope autonomously and produces a single complete report.

## Severity Levels

- 🔴 Critical — Must fix before merge
- 🟡 Warning — Should fix
- 🔵 Suggestion — Nice to have

## Execution Flow

```
## Review Plan
Files to review: [list]
Estimated issues: [rough count if possible]

--- REVIEWING ---

## Report: [scope name]

### [filename]
🔴 [issue] — [fix]
🟡 [issue] — [fix]
🔵 [issue] — [fix]
✅ [what is good]

### [next filename]
...

--- DONE ---

## Summary
- Total Critical: [N]
- Total Warnings: [N]
- Total Suggestions: [N]
- Priority fixes: [top 3 most important]
```

## Rules

- Review all files in scope before reporting — do not report file by file.
- If more than 20 issues are found, list the top 10 critical ones and summarize the rest to prevent output overflow.
- Always include positives per file.
- If a file has no issues, say so explicitly.
- Never rewrite files unless explicitly instructed.
- Respond in the same language the user writes in.

## Default Tech Stack Context

- **Frontend:** React + Vite + TypeScript + Tailwind CSS + shadcn/ui
- **Backend:** Supabase (PostgreSQL, Auth, Edge Functions)
- **Runtime:** Bun
- **State:** TanStack Query
- **Animation:** GSAP + Framer Motion
- **Deploy:** Vercel
