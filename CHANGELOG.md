# Changelog

## Unreleased

- Remove the WHERE section from comment blocks; blast-radius commentary overlapped with HOW and was often filler on isolated changes

## 1.0.0 — 2026-06-26

Initial public release.

- WHY/HOW/WHEN/WHERE structured comment blocks for code changes
- Language-native comment syntax (Python/Ruby/Shell, JS/TS/Go/Rust/Java, CSS/SCSS, HTML/XML)
- Multi-file change handling with primary/secondary site cross-references
- Rules for when to omit blocks (trivial changes, formatting, generated code, self-evident renames)
- One block per logical change, 1–3 sentences per section
