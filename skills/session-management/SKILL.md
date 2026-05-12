---
name: session-management
description: >
  Use this skill when working with the start-session plugin's workspace structure,
  file conventions, and session rules. Triggers on: starting a session, ending a session,
  checkpointing progress, working with project files, reading CLAUDE.md or memory files,
  or when the user asks how memory or tracking works.
version: 2.0.0
---
---
name: session-management
description: >
  Context layer for the start-session memory system. Load this skill whenever working within a
  start-session workspace — any folder containing a CLAUDE.md populated by /setup. Triggers include:
  references to projects, sessions, workspace files, memory files, the project index, or when
  the user mentions "start session", "end session", "new project", or "checkpoint". Also load when
  the user asks about their workspace structure, their project list, or how the memory system works.
---

# start-session — Memory System Context

This skill gives the assistant full context about how a start-session workspace is structured and how to navigate it.

## What this system is

start-session is a file-based memory scaffold. The user runs `/setup` once to generate a workspace — a folder of Markdown files the assistant reads at session start to stay oriented across sessions and projects.

The system has two layers:
- **Plugin (this)** — commands and protocols. Logic lives here and updates automatically.
- **Workspace files** — user data. Lives in the user's folder. The user owns and edits these.

## Workspace file structure

| File / Folder | Purpose |
|---|---|
| `CLAUDE.md` | User identity, tools, preferences, hard rules, references, custom agents table. The primary context file. |
| `AGENTS.md` | Thin pointer to `CLAUDE.md` for Codex auto-discovery. Same source, two entry points. |
| `memory/projects.md` | Single source of truth for all projects across all states. Read at session start when no project is named. |
| `memory/glossary.md` | Terms, tools, acronyms, and shorthand the assistant should recognize. |
| `templates/project-CLAUDE.md` | Template for new per-project context files. |
| `templates/project-CODEX.md` | Template for phased execution plans (optional). |
| `resources/example-agent.md` | Format reference for custom agent instruction files. |
| `resources/[agent-name].md` | Agent instruction files created by the assistant when the user adds a custom agent. |
| `projects/` | Contains per-project folders created during `/new-project`. |
| `projects/[id-slug]/CLAUDE.md` | Per-project context: status, decisions, next steps. Updated at session end. |

## Project index format

`memory/projects.md` uses a machine-readable line format:

```
- **[ID] — [Project Name]** [emoji] Status — one-line description
```

Status emoji key: 🔵 WIP · 🟢 Live · ✅ Complete · ⏸️ On Hold · 📦 Shelved · 💡 Idea

When reading the project index: list only 🔵 WIP and 🟢 Live projects by default. Skip ✅ ⏸️ 📦 💡 unless the user asks.

## Project naming convention

If the user set up a naming convention during `/setup`, it lives in their `CLAUDE.md` under "Our Projects." The format is typically:
- `[PREFIX]-[CategoryLetter][##]-[slug]`
- Example: `HS-V01-reel` or `BM-W02-site-redesign`

Respect whatever convention is in the user's CLAUDE.md. If none exists, ask the user what ID format to use during `/new-project`.

## Custom agents

Custom agents live in two places:
- `resources/[agent-name].md` — the instruction file (created and maintained by the assistant)
- Custom Agents table in `CLAUDE.md` — the index (name, trigger phrases, what it does)

When the user asks to add, change, or remove an agent, update both. The user never edits resource files directly.

## Hard rules (always apply)

These are system-level rules that apply in every session regardless of what the user's CLAUDE.md says:
- If source material is inaccessible, say so clearly. Don't infer or approximate.
- Distinguish recalled knowledge from verified knowledge.
- Don't promise compatibility without knowing the user's version or environment.
- Name at least one failure mode when proposing a solution.
- Cite sources for claims and recommendations where possible.
- For technical/software guidance, prioritize current documentation over training knowledge.

The user's `CLAUDE.md` may contain additional hard rules specific to their workflow. Always read and respect those too.
