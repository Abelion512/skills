# Contributing to abelion-skills

## Skill Structure Standard

Every skill follows this structure (based on Anthropic skills standard):

```
skill-name/
├── SKILL.md              ← Required. Step-by-step mode.
├── SKILL.agent.md        ← Agentic mode (Abelion extension).
├── README.md             ← Skill documentation.
└── references/           ← Context files loaded by the agent.
    ├── [topic].md
    └── ...
```

### SKILL.md Frontmatter

```yaml
---
name: skill-name           # lowercase, hyphens
description: >
  One paragraph. Explain WHAT the skill does and WHEN to use it.
  Be specific — this is what the agent uses to decide when to activate.
---
```

### SKILL.agent.md Frontmatter

Same format as SKILL.md but with `-agent` suffix in name.

## How to Add a New Skill

1. Create folder: `mkdir skill-name`
2. Create `SKILL.md` with frontmatter + instructions
3. Create `SKILL.agent.md` for agentic version
4. Create `README.md` with usage docs
5. Create `references/` with relevant cheatsheets
6. Update root `README.md` skill table
7. Verify all files are valid UTF-8: `file skill-name/*.md`

## How to Use Skills

### Antigravity (AG)
Settings → Skills → Add Folder → point to skill folder.

### Zed
```json
// ~/.config/zed/settings.json
{
  "context_servers": {
    "skill-name": {
      "command": "cat",
      "args": ["/path/to/skill-name/SKILL.md"]
    }
  }
}
```

### Claude.ai
Upload skill folder or paste SKILL.md content in project knowledge.

### Claude Code
```bash
/skill add /path/to/skill-name
```

## Versioning

Skills follow semantic versioning in commit messages:
- `feat(skill-name): add X` — new feature
- `fix(skill-name): fix Y` — bug fix
- `ref(skill-name): update Z` — reference update

## Stack Updates

When updating `references/stack.md` or any reference file, always verify
against official docs before updating. Include the date of update in the file.
