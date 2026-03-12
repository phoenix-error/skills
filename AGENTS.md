# opensrc

Fetch npm package or GitHub repository source code to gain implementation-level context about how libraries work internally.

## When to use

Use `opensrc` whenever you need deeper context about how a library works — not just its types or docs. Trigger it when:

- The user asks about implementation details, internals, or behavior of an npm package or GitHub repo
- You're unsure how a library actually works under the hood
- Types/docs alone are insufficient to answer a question confidently
- The user asks you to "look at", "check", "understand", or "explore" a package or repo
- You're about to give an answer about a package's internals and you haven't fetched its source yet

## Setup

```bash
# Check if installed
opensrc --version 2>/dev/null || npm install -g opensrc
```

## Commands

```bash
# Fetch npm package source (auto-detects version from lockfile)
opensrc <package-name>
opensrc <package-name>@<version>
opensrc <pkg1> <pkg2> <pkg3>

# Fetch GitHub repository source
opensrc owner/repo
opensrc https://github.com/owner/repo
opensrc owner/repo@v1.0.0
opensrc owner/repo#main

# List / remove fetched sources
opensrc list
opensrc remove <package-or-repo>
```

Use `--modify` flag in automated/agent contexts to avoid interactive prompts.

## Output

Source is stored at `opensrc/<package-name>/` or `opensrc/owner--repo/` in the current working directory. An index at `opensrc/sources.json` tracks all fetched packages.

## Workflow

1. Identify relevant package(s) or repo(s)
2. Check if source is already fetched (`opensrc/sources.json`)
3. Fetch if not present
4. Read the relevant source files (focus on `src/`, entry points)
5. Answer based on actual implementation
