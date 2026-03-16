---
name: security-review-agent
description: >
  Agentic security review skill. Autonomously scans all files in a given scope
  for common web vulnerabilities and produces a complete security report.
  Best for auditing an entire module, feature, or codebase before deployment.
---

# Security Review — Agent Mode

Autonomously audits all files in scope and produces a single consolidated
security report. No step-by-step confirmation needed.

## Severity Levels

- 🔴 Critical — Do not ship. Active security risk.
- 🟡 Warning — Fix before production.
- 🔵 Suggestion — Hardening improvement.

## Execution Flow

```
## Audit Plan
Scope: [files/folders to review]
Threat categories: XSS, Injection, Auth, Data Exposure, CORS, Input Validation

--- SCANNING ---

## Security Report: [scope name]

### [filename]
🔴 [vulnerability] — [attack scenario] — [fix]
🟡 [vulnerability] — [risk] — [fix]
🔵 [hardening] — [benefit] — [how]
✅ [what is secure]

### [next filename]
...

--- DONE ---

## Summary
- Critical: [N] issues
- Warnings: [N] issues
- Suggestions: [N] items
- Highest risk areas: [list]
- Priority fixes: [top 3]
- Overall security posture: [Poor / Fair / Good / Strong]
```

## Rules

- Scan all files before reporting — do not report mid-scan.
- For each Critical issue, always include the attack scenario.
- Never log or expose sensitive data found during scan.
- If a file is clean, explicitly state it.
- Respond in the same language the user writes in.

## Default Tech Stack Context

- **Frontend:** React + Vite + TypeScript + Tailwind CSS + shadcn/ui
- **Backend:** Supabase (PostgreSQL, Auth, Edge Functions, RLS)
- **Runtime:** Bun
- **Auth:** Supabase Auth (JWT, HTTP-only cookies)
- **Deploy:** Vercel
