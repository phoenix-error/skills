# skills

A collection of open agent skills for AI coding agents.

Works with **40+ agents** including Claude Code, Codex, Cursor, Windsurf, Copilot, Cline, Goose, Kiro, and more via the [open agent skills ecosystem](https://github.com/vercel-labs/skills).

## Skills

| Skill | Description | Install |
|-------|-------------|---------|
| [opensrc](./opensrc) | Fetch npm/GitHub source code for implementation-level context | `npx skills add phoenix-error/skills@opensrc` |

## Install

### Via the Skills CLI (recommended)

```bash
# Install a specific skill
npx skills add phoenix-error/skills@opensrc

# Install all skills
npx skills add phoenix-error/skills
```

### Manual install

Copy the `SKILL.md` from any skill folder into your agent's skills directory:

| Agent | Path |
|-------|------|
| Claude Code | `.claude/skills/<skill-name>/SKILL.md` |
| Codex | `.codex/skills/<skill-name>/SKILL.md` |
| Cursor | `.cursor/skills/<skill-name>/SKILL.md` |
| Windsurf | `.windsurf/skills/<skill-name>/SKILL.md` |
| Copilot | `.github/copilot/skills/<skill-name>/SKILL.md` |

## License

MIT
