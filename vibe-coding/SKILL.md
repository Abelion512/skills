---
name: vibe-coding
description: >
  Workflow skill for flow state coding. Use this skill when the user starts
  a new coding session, requests feature implementation, debugging, or
  refactoring. Prioritizes context explanation before code, and breaks work
  into small executable steps confirmed one at a time.
---

# Vibe Coding

This skill is designed to maintain flow state while coding — staying focused,
not overwhelmed, and always knowing what is being done and why.

## Core Principles

1. **Context first, code second** — Before writing any code, explain what will
   be done, why, and its impact on the codebase.
2. **Small steps** — Every task is broken into the smallest executable unit
   that can be independently verified.
3. **Single focus** — Only work on one thing at a time. No changes outside
   the current scope.
4. **Verify each step** — After every step, confirm the result before moving
   to the next.

## Response Format

Every response follows this structure:

## Context
[Brief explanation of what will be done and why]

## Step [N] of [Total]
[Explanation of this step]
[code]

## Verification
[How to confirm this step succeeded]

## Next
[Preview of the next step — one sentence only]

## Rules

- Never write more than one step at a time without user confirmation.
- Never modify files outside the current task scope.
- If there is ambiguity, ask before making assumptions.
- If there is a risk of breaking changes, warn in the Context section.
- Respond in the same language the user writes in.

## Default Tech Stack Context

- **Frontend:** React + Vite + TypeScript + Tailwind CSS + shadcn/ui
- **Backend:** Supabase (PostgreSQL, Auth, Edge Functions)
- **Runtime:** Bun
- **State:** TanStack Query
- **Animation:** GSAP + Framer Motion
- **Deploy:** Vercel

Adjust to the active project stack if different.
