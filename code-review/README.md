# code-review

> Structured code review skill for TypeScript/React/Supabase projects.

## What This Skill Does

Reviews code for quality, maintainability, and best practices with:
- Severity-based feedback (🔴 Critical / 🟡 Warning / 🔵 Suggestion)
- Category-based analysis (types, React, async, security, quality, Supabase)
- Actionable fixes with code snippets
- Both self-review and peer review support

## When to Use

| Scenario | Use |
|---|---|
| Review your own code before commit | `SKILL.md` |
| Review a specific file or function | `SKILL.md` |
| Review an entire PR or module | `SKILL.agent.md` |
| Pre-deployment audit | `SKILL.agent.md` |

## Files

| File | Purpose |
|---|---|
| `SKILL.md` | Step-by-step review mode |
| `SKILL.agent.md` | Full autonomous review report |
| `references/checklist.md` | Complete review checklist |
| `references/react-patterns.md` | React/TypeScript pattern reference |

## Usage

### Antigravity
Add skill folder to AG agent settings → Skills.

### Zed / Claude Code
Reference `SKILL.md` in your project context before requesting a review.

## Severity Guide

| Level | Meaning | Action |
|---|---|---|
| 🔴 Critical | Breaks functionality, security, or data | Fix before merge |
| 🟡 Warning | Technical debt, bad practice | Fix before production |
| 🔵 Suggestion | Readability, style improvement | Nice to have |
