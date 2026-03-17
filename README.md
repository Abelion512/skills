# abelion-skills

> Personal AI agent skills for Abelion's development workflow.
> Based on [Anthropic Skills](https://github.com/anthropics/skills) standard.

Modular skills that extend AI agent capabilities with context, conventions,
and structured workflows — built for the Abelion stack.

## Skills

| Skill | Status | Description |
|---|---|---|
| [vibe-coding](./vibe-coding/) | ✅ Ready | Flow state coding workflow |
| [code-review](./code-review/) | ✅ Ready | Code quality & best practices |
| [security-review](./security-review/) | ✅ Ready | OWASP-based security audit |
| [performance](./performance/) | 🔜 Planned | Performance optimization |
| [design-review](./design-review/) | 🔜 Planned | UI/UX & accessibility |

## Structure

Each skill follows Anthropic's standard structure:

```
skill-name/
├── SKILL.md              ← Step-by-step mode (you stay in control)
├── SKILL.agent.md        ← Agentic mode (delegate to agent)
├── README.md             ← Skill documentation
└── references/           ← Context files: cheatsheets, patterns, docs
```

## Compatible IDEs

| IDE | Support |
|---|---|
| Antigravity | ✅ Via Skills settings |
| Zed | ✅ Via context_servers |
| Claude.ai | ✅ Via project knowledge |
| Claude Code | ✅ Via /skill command |
| Cursor / Windsurf | ✅ Via MCP or context |

## Default Stack

All skills are optimized for:

- **Runtime:** Bun 1.x
- **Frontend:** React 19 + Vite 6 + TypeScript 5 + Tailwind CSS 4 + shadcn/ui
- **Backend:** Supabase (PostgreSQL + Auth + Edge Functions + RLS)
- **State:** TanStack Query 5 + Zustand 5
- **Validation:** Zod 3
- **Animation:** GSAP 3 + Framer Motion 11
- **Deploy:** Vercel

## Usage

See [CONTRIBUTING.md](./CONTRIBUTING.md) for how to use and add skills.

---

Built by [Abelion512](https://github.com/Abelion512) · Inspired by [anthropics/skills](https://github.com/anthropics/skills)
