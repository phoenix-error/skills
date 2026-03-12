---
name: opensrc
description: >
  Use opensrc to fetch npm package or GitHub repository source code whenever you need deeper
  context about how a library works internally — not just its types or docs. Trigger this skill
  whenever the user asks about implementation details, internals, or behavior of an npm package
  or GitHub repo; whenever you're unsure how a library actually works under the hood; whenever
  types/docs alone are insufficient to answer a question confidently; or whenever the user asks
  you to "look at", "check", "understand", or "explore" an npm package or GitHub repository.
  Also trigger proactively when you're about to give an answer about a package's internals and
  you haven't fetched its source yet. Don't wait for the user to ask — if source code would help,
  fetch it.
---

# opensrc Skill

Fetch npm package or GitHub repository source code to gain implementation-level context.

## Installation check

Before using, verify `opensrc` is globally available:

```bash
opensrc --version 2>/dev/null || echo "not installed"
```

If not installed, detect the project's package manager and install globally:

1. Check for lockfiles in the project root:
   - `pnpm-lock.yaml` → pnpm
   - `bun.lockb` / `bun.lock` → bun
   - `yarn.lock` → yarn
   - `package-lock.json` → npm
2. If ambiguous or no lockfile found, ask the user which package manager to use.
3. Install globally with the detected/chosen manager:

```bash
pnpm add -g opensrc
# or
bun add -g opensrc
# or
yarn global add opensrc
# or
npm install -g opensrc
```

After installing, verify with `opensrc --version` before proceeding.

## Usage

### Fetch npm packages

```bash
# Single package (auto-detects version from lockfile if present)
opensrc <package-name>

# Specific version
opensrc <package-name>@<version>

# Multiple packages at once
opensrc <pkg1> <pkg2> <pkg3>
```

### Fetch GitHub repositories

```bash
# owner/repo shorthand
opensrc owner/repo

# Full GitHub URL
opensrc https://github.com/owner/repo

# Specific branch or tag
opensrc owner/repo@v1.0.0
opensrc owner/repo#main

# github: prefix
opensrc github:owner/repo
```

### List / remove fetched sources

```bash
opensrc list
opensrc remove <package-or-repo>
```

## Output location

Source is stored at `opensrc/<package-name>/` or `opensrc/owner--repo/` in the current working directory.

An index file at `opensrc/sources.json` lists all fetched packages with their versions and paths.

## Workflow

1. **Identify** what package(s) or repo(s) are relevant to the user's question.
2. **Check** if source is already fetched: look for `opensrc/sources.json` or the relevant directory.
3. **Fetch** if not already present using the appropriate command above.
4. **Read** the relevant source files — focus on `src/`, entry points, and files relevant to the question.
5. **Answer** based on actual implementation, not just types or documentation.

## File modification prompt

On first run, opensrc asks permission to modify `.gitignore`, `tsconfig.json`, and `AGENTS.md`.
Use `--modify` to allow or `--modify=false` to deny without interactive prompt:

```bash
opensrc <package> --modify
```

In automated/agent contexts, prefer `--modify` to avoid blocking on stdin.

## When to fetch vs. skip

**Fetch source when:**
- User asks how a library works internally
- Types/docs don't explain the behavior
- Debugging unexpected behavior of a dependency
- Comparing implementations across packages
- User says "look at", "check", "explore", "understand" a package/repo

**Skip if:**
- Source already fetched and in `opensrc/sources.json`
- Question is purely about the public API (types are sufficient)
- Package is a well-known standard (e.g., `fs`, `path` — no source needed)
