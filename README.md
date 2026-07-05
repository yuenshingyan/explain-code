# explain-code

A Claude Code skill that annotates code changes with structured WHY/HOW/WHEN comment blocks explaining the reasoning, approach, and runtime conditions of each non-trivial change.

## Features

- **Structured commentary**: Three labeled sections — WHY (the problem), HOW (the approach), WHEN (the runtime conditions)
- **Language-native syntax**: Uses correct comment syntax for Python, Ruby, JS/TS, Go, Rust, Java, CSS, HTML, and more
- **Multi-file handling**: Full block at the primary change site; concise cross-references at secondary sites
- **Smart omission rules**: Skips blocks for trivial changes (typo fixes, formatting, generated code, self-evident renames)
- **Specificity enforced**: Names real functions, endpoints, config keys, and ticket IDs — never vague labels like "the handler"

## Install

Clone this repo directly into your Claude Code skills directory:

**macOS / Linux:**

```bash
git clone https://github.com/yuenshingyan/explain-code-claude-skill ~/.claude/skills/explain-code
```

**Windows (PowerShell):**

```powershell
git clone https://github.com/yuenshingyan/explain-code-claude-skill "$env:USERPROFILE\.claude\skills\explain-code"
```

That's it. Claude Code auto-discovers skills in `~/.claude/skills/` (`%USERPROFILE%\.claude\skills\` on Windows).

### Update

**macOS / Linux:**

```bash
cd ~/.claude/skills/explain-code && git pull
```

**Windows (PowerShell):**

```powershell
cd "$env:USERPROFILE\.claude\skills\explain-code"; git pull
```

### Uninstall

**macOS / Linux:**

```bash
rm -rf ~/.claude/skills/explain-code
```

**Windows (PowerShell):**

```powershell
Remove-Item -Recurse -Force "$env:USERPROFILE\.claude\skills\explain-code"
```

## Usage

After making code changes, use one of:

- "explain this change"
- "add code commentary"
- "annotate my changes"
- "add WHY/HOW comments"
- "document why I changed this"

Claude will read the changed code, identify non-trivial changes, and add structured WHY/HOW/WHEN blocks directly above each change using the file's native comment syntax.

## License

MIT
