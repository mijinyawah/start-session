# Changelog

## v1.3.0 — Setup flow overhaul

### What changed

- `CLAUDE.md` — setup flow rebuilt from live testing with Claude and Codex:
  - `## Onboarding` renamed to `## Setup` to avoid assistant auto-naming the session as an onboarding process
  - Mode selection (Lite/Pro) removed entirely. Steps 4 and 5 are now conditional on user answers rather than gated behind an upfront mode choice
  - Step 2 expanded: each field includes a "Why:" note so the assistant explains purpose before asking. Project naming convention is now an explicit question
  - Step 3 (Hard Rules) opens with a preamble explaining why the rules exist
  - Step 4 question broadened to catch creative-technical users who wouldn't self-identify as developers. Adds a "sometimes / it depends" path
  - Step 5 (Agents) now conditional — asks before running, explicitly tells the user agents can be added later
  - Step 6 (Finalize) rewritten: closes with a user-facing message about what was saved and the three session commands
- `CLAUDE.md` — Session Behavior and Agents sections updated: protocols and agents are always available; assistant stays passive unless invoked
- `README.md` — "How setup adapts to you" section replaces Lite/Pro framing

---

## v1.2.1 — Initial public release

### What's included

- `CLAUDE.md` — canonical memory file with setup flow, session protocols, project kickoff agent, and custom agent support
- `AGENTS.md` — root-level entry point for Codex folder-based sessions; points at `CLAUDE.md` as the single source of truth
- `memory/glossary.md` — persistent shorthand and terminology reference, maintained by the assistant
- `memory/projects.md` — single-file project index using status emojis across all project states (WIP / Live / Complete / On Hold / Shelved / Idea)
- `templates/project-CLAUDE.md` — per-project context template
- `templates/project-CODEX.md` — optional phased execution plan template for Codex-based projects
- `resources/example-agent.md` — format reference for custom agent instruction files
- `projects/` — directory where project folders are created during kickoff

### Platform support

Works natively with Claude (CoWork, Claude Code) and Codex (folder-based sessions).

### License

MIT
