---
name: explain-code
description: >-
  Explain code changes with line numbers as references for a given file.
when_to_use: >-
  TRIGGER when the user "/explain-code".
effort: high
allowed-tools:
  - Read
  - Bash(git status *)
  - Bash(git diff *)
  - Bash(git log *)
---

## Code Explanations

Generate a line-anchored walkthrough of the code changes in a given file, output to chat. Start with the file path as a heading, follow with a one-line **Summary** of what the changes accomplish overall, then walk the file top to bottom with one bullet per logical change, each anchored to its line number or range.

Every line anchor MUST be a clickable markdown link that jumps to the referenced lines. Use the workspace-relative file path with `#L<start>-L<end>` (or `#L<line>` for a single line) as the link target:

- Range: `[L12–18](src/auth/session.py#L12-L18)`
- Single line: `[L24](src/auth/session.py#L24)`

Never write a bare `**L12–18**` — an anchor that can't be clicked defeats the purpose.

### Determine the diff first

Never infer "changes" from a single read of the current file — establish the actual diff before writing a single bullet:

- `git status --porcelain -- <file>` — if the file is untracked (`??`), it's entirely new; every line is in scope.
- Otherwise, `git diff HEAD -- <file>` — covers staged and unstaged edits together against the last commit.
- If that's empty, fall back to the most recent commit that touched the file: `git log -1 -p --cc -- <file>`.
- If none of these turns up an actual line-level hunk — not a git repo, no history for the file, a binary file, a pure rename with no content change — say so plainly and stop. Do not fall back to a whole-file walkthrough.
- If the diff contains unresolved merge-conflict markers (`<<<<<<<`/`=======`/`>>>>>>>`), flag that instead of narrating them as ordinary changes.

Use the new-file side of each hunk header (`@@ -a,b +c,d @@`) for line numbers, confirmed against a Read of the current file rather than a manual recount. Anchor a pure removal (no surviving line) to the current-file line immediately adjacent to where it used to sit.

### Format

```
### <file path>

**Summary:** <one sentence — what this file's changes accomplish overall>

- **[L<start>–<end>](<relative path>#L<start>-L<end>)** `<symbol, if the range maps to one>` — <what changed and why it matters>
- **[L<line>](<relative path>#L<line>)** — <single-line change explanation>
...
```

### Example

```
### src/auth/session.py

**Summary:** Adds token-refresh handling to the session middleware.

- **[L12–18](src/auth/session.py#L12-L18)** `refresh_token()` — New entry point. Exchanges the expiring JWT for a fresh one via the auth service; called before every authenticated request.
- **[L24](src/auth/session.py#L24)** — Guard clause: skips refresh when the token has >5 min of validity left, avoiding a network round-trip per request.
- **[L31–40](src/auth/session.py#L31-L40)** `SessionMiddleware.__call__` — Now wraps the handler in a try/except for `TokenExpiredError`, retrying once after a forced refresh instead of returning 401 immediately.
- **[L55](src/auth/session.py#L55)** — Removed the old `MAX_RETRIES` constant; retry logic moved into `refresh_token()`.
```

### Rules

- Only bullet lines confirmed as additions or modifications by the diff — never explain unchanged code, no matter how noteworthy it looks.
- Walk the file top to bottom; keep bullets in source-line order.
- Anchor every bullet to a line or range as a clickable markdown link (workspace-relative path with `#L…` fragment); name the enclosing symbol (function, class, method) when the range maps to one.
- Explain what changed and why it matters — not a syntax narration ("added an if-statement").
- Group contiguous lines belonging to one logical change into a single range; don't split them per line.
- Skip trivia (formatting, typo fixes, self-evident renames) rather than padding the list.
