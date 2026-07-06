# explain-code

A Claude Code skill that explains code changes as a line-anchored walkthrough in chat — every bullet links straight to the lines it describes.

## Features

- **Diff-first**: Never narrates a whole file from a single read — establishes the actual diff (`git status`/`git diff`/`git log -p`) before writing a single bullet, and says so plainly if there's no diff to explain
- **Clickable line anchors**: Every bullet links to its exact lines (`file.py#L12-L18`), so you can jump straight to the code
- **Top-to-bottom walkthrough**: One bullet per logical change, grouped by contiguous lines, in source order, with the enclosing function/class named when relevant
- **Explains why it matters**: Describes the effect of a change, not a syntax narration
- **Skips trivia**: Omits formatting, typo fixes, and self-evident renames rather than padding the list

## Install

Clone this repo directly into your Claude Code skills directory:

**macOS / Linux:**

```bash
git clone https://github.com/yuenshingyan/explain-code ~/.claude/skills/explain-code
```

**Windows (PowerShell):**

```powershell
git clone https://github.com/yuenshingyan/explain-code "$env:USERPROFILE\.claude\skills\explain-code"
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

Run `/explain-code` on a file to get a summary and a line-anchored bullet list of what changed in it.
