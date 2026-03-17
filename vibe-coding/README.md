# vibe-coding

> Flow state coding workflow skill for Abelion's development environment.

## What This Skill Does

Keeps you in flow state while coding by:
- Explaining context before writing any code
- Breaking tasks into small, verifiable steps
- Never touching files outside the current scope
- Confirming results before moving forward

## When to Use

| Scenario | Use |
|---|---|
| New feature implementation | `SKILL.md` |
| Debugging a specific issue | `SKILL.md` |
| Scaffolding / bulk refactor | `SKILL.agent.md` |
| Repetitive boilerplate tasks | `SKILL.agent.md` |

## Files

| File | Purpose |
|---|---|
| `SKILL.md` | Step-by-step mode — you stay in control |
| `SKILL.agent.md` | Agentic mode — delegate full task to agent |
| `references/stack.md` | Default tech stack reference |
| `references/conventions.md` | Code conventions and patterns |

## Usage

### Antigravity
Add this skill folder to your AG agent configuration via Settings → Skills.

### Zed
Reference in `~/.config/zed/settings.json`:
```json
{
  "context_servers": {
    "vibe-coding": {
      "command": "cat",
      "args": ["path/to/vibe-coding/SKILL.md"]
    }
  }
}
```

### Claude.ai / Claude Code
Upload the skill folder or reference SKILL.md directly in your project context.

## Default Stack

React 19 + Vite 6 + TypeScript 5 + Tailwind CSS 4 + shadcn/ui + Supabase + Bun
