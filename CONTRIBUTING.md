# Contributing

Thanks for your interest in improving this skill.

## Reporting bugs

Open an issue using the **Bug report** template. Include:

- What code you asked Claude Code to annotate (language, type of change)
- What went wrong (wrong comment syntax, missing block, block placed incorrectly, wrong section content)
- Your Claude Code version (`claude --version`)

## Suggesting features

Open an issue using the **Feature request** template. Describe the use case and any alternatives you considered.

## Making changes

The skill is defined entirely in **SKILL.md**. Edit this to change the annotation procedure, comment structure, or omission rules.

### Testing locally

1. Clone the repo into your skills directory:
   ```bash
   git clone https://github.com/yuenshingyan/explain-code-claude-skill ~/.claude/skills/explain-code
   ```
2. Make your changes to `SKILL.md`.
3. Open any project in Claude Code, make some code changes, and ask Claude to annotate them.
4. Verify that blocks appear above each non-trivial change with correct language syntax and accurate section content.

### Pull requests

- Keep PRs focused — one change per PR.
- Test annotation across at least two different languages to confirm syntax handling.
- Update `CHANGELOG.md` with a summary under an "Unreleased" heading.

## License

By contributing, you agree that your contributions will be licensed under the MIT License.
