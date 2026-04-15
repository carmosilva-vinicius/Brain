# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## About This Repository

This is a personal knowledge base (Obsidian vault) containing programming study notes in Markdown. There are no build, lint, or test commands — the "output" is the notes themselves.

## Content Structure

Top-level folders map to broad topics:

- `Algorithms/` — algorithm concepts
- `Data Structure/` — arrays, linked lists, trees, etc.
- `Database/` — relational (PostgreSQL, SQL Server), NoSQL, Redis, ORM, transactions
- `Desktop/` — SAP and desktop-specific topics
- `DevOps/` — Git, Docker, containers
- `Hardware/` — embedded systems
- `Network/` — DNS, networking
- `OS/` — Linux CLI, permissions, systemd, directory structure
- `Programming/` — Go, Rust, Java, Software Architecture (Clean Architecture, DDD, SOLID, Design Patterns)
- `Utils/` — CLI tools (jq, fzf, delta)
- `Web/` — HTTP, caching, message queues, Nginx, performance

## Obsidian Conventions

- **Internal links**: Use `[[Topic Name]]` syntax to cross-reference other notes (e.g., `[[Database]]`, `[[ORM]]`, `[[Structural]]`). These become clickable links in Obsidian.
- **Tags**: Obsidian tags use `#tag-name` syntax within note content.
- **No frontmatter required**: Notes typically start directly with content (no YAML frontmatter).

## Note Format Conventions

- Notes begin with a brief plain-text definition or explanation of the concept.
- Use `###` or `####` for section headers (avoid `#` and `##` for section headings within notes).
- Code examples are fenced with language identifiers (` ```java `, ` ```sql `, ` ```bash `, ` ```cs `, etc.).
- File path labels above code blocks use `###### path/to/File.ext` format.
- New topics should be placed in the most relevant existing folder, creating a subfolder if the topic is broad enough to warrant multiple notes.
