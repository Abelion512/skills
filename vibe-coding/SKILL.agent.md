---
name: vibe-coding-agent
description: >
  Agentic workflow skill for flow state coding. Use this skill when the user
  wants to delegate a full task to the agent without step-by-step confirmation.
  The agent plans all steps, executes autonomously, and reports results at the end.
  Best for repetitive tasks, scaffolding, and bulk refactoring.
---

# Vibe Coding — Agent Mode

This skill runs coding tasks autonomously from start to finish. The user
delegates the entire task; the agent plans, executes, and reports.

## Core Principles

1. **Plan before acting** — Before any execution, output a complete plan
   listing all steps and files that will be affected.
2. **Execute fully** — Complete all steps without interruption unless a
   blocking error occurs.
3. **Report on completion** — Summarize what was done, what files were
   changed, and any issues encountered.
4. **Minimal footprint** — Only touch files required for the task.

## Execution Flow

## Plan
[Numbered list of all steps]
[Files that will be created or modified]

--- EXECUTING ---
[Silent execution]

--- DONE ---

## Summary
[What was completed]
[Files created/modified]
[Warnings if any]
copy



## Rules

- Always output the plan first and wait for user approval before executing.
- If a blocking error occurs mid-execution, stop and report immediately.
- Never delete files unless explicitly instructed.
- Never modify .env files without explicit instruction.
- Respond in the same language the user writes in.

## Default Tech Stack Context

- **Frontend:** React + Vite + TypeScript + Tailwind CSS + shadcn/ui
- **Backend:** Supabase (PostgreSQL, Auth, Edge Functions)
- **Runtime:** Bun
- **State:** TanStack Query
- **Animation:** GSAP + Framer Motion
- **Deploy:** Vercel
