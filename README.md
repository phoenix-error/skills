# opensrc skill

An open agent skill that gives AI coding agents the ability to fetch and read npm package or GitHub repository source code — so they can answer questions based on actual implementation, not just types or docs.

Works with **40+ AI coding agents** including Claude Code, Codex, Cursor, Windsurf, Copilot, Cline, Goose, Kiro, and more via the [open agent skills ecosystem](https://github.com/vercel-labs/skills).

## Install

### Via the Skills CLI (recommended)

```bash
npx skills add user/opensrc-skill
```

This auto-detects your installed agents and installs the skill for all of them.

### Manual install

Copy `SKILL.md` into your agent's skills directory:

| Agent | Path |
|-------|------|
| Claude Code | `.claude/skills/opensrc/SKILL.md` |
| Codex | `.codex/skills/opensrc/SKILL.md` |
| Cursor | `.cursor/skills/opensrc/SKILL.md` |
| Windsurf | `.windsurf/skills/opensrc/SKILL.md` |
| Copilot | `.github/copilot/skills/opensrc/SKILL.md` |

Or install globally by placing it in `~/<agent>/skills/opensrc/SKILL.md`.

The `AGENTS.md` file at the repo root provides cross-agent compatibility for agents that follow the AGENTS.md standard (Codex, OpenHands, etc.).

## Prerequisites

The skill requires the [`opensrc`](https://www.npmjs.com/package/opensrc) CLI tool:

```bash
npm install -g opensrc
```

The skill will auto-detect if `opensrc` is missing and prompt for installation.

## What it does

When activated, the skill instructs the agent to:

1. **Detect** when source code would help answer a question about a library
2. **Fetch** the actual source using `opensrc <package>` or `opensrc owner/repo`
3. **Read** relevant source files (entry points, `src/`, etc.)
4. **Answer** based on real implementation — not guesswork

### Examples

- "How does `zod` validate nested objects?" → fetches zod source, reads the parsing logic
- "What does `next/image` do under the hood?" → fetches Next.js, reads the Image component
- "Compare how `express` and `fastify` handle middleware" → fetches both, reads the middleware chains

## License

MIT
