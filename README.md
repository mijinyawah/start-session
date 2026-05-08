# Engram—An AI Memory Engine (v1.3.0)

Engram provides persistent, file-based memory for a non-technical user's AI-assisted workflows. Give your AI assistant lasting context about who you are, how you work, and the projects you work on. By pointing your AI at this memory system structure, you can mitigate missed/hallucinated context, or having to re-explain to the AI where you last left off on a project. 

Designed for Claude CoWork, but also works with Codex.

---

## Who this is for

- People running multiple ongoing projects with an AI assistant like Claude Cowork or Codex
- Creative-technical users who want better project management structure and AI "memory" that isn't overkill
- Solo builders or small teams that value continuity between AI working sessions

---

## Platform compatibility

| Platform | How it works |
|----------|-------------|
| **Claude** (CoWork, Claude Code) | Auto-discovers `CLAUDE.md` |
| **Codex** (folder-based sessions) | Auto-discovers `AGENTS.md`, which points at `CLAUDE.md` |

`AGENTS.md` is a thin pointer so Codex finds the system without duplicating content. Both platforms read from the same canonical source.

> **Note:** trigger phrases in `CLAUDE.md` are protocol instructions, not hardcoded automations. If an expected behavior doesn't trigger with natural language, type the command directly in chat (e.g. `run onboarding now`, `start session`).

---

## Quick start

1. Copy this folder to a location you control.
2. Open this folder as your working directory in CoWork or Codex.
3. In chat, type `run onboarding now` to begin setup.

### How setup adapts to you

Setup is a single flow that covers your identity, tools, projects, and behavior preferences. Two steps are conditional based on your answers:

- **Technical calibration** runs if you do any coding, scripting, or technical troubleshooting — including creative-technical work like expressions or self-hosted tools.
- **Agent setup** runs if you want custom behavior modes (e.g. a research mode, a debug mode). You can skip this and add agents later just by asking.

Session commands (`start session`, `end session`, `new project`) are available to everyone regardless of how setup goes.

---

## Folder structure

| Path | Purpose |
|------|---------|
| `CLAUDE.md` | Global memory, setup flow, session protocols, agent behavior (canonical) |
| `AGENTS.md` | Codex-side pointer to `CLAUDE.md` |
| `memory/glossary.md` | Terms, tools, acronyms, shorthand |
| `memory/projects.md` | Single source of truth for all projects across every state (WIP / Live / Complete / On Hold / Shelved / Idea) |
| `templates/project-CLAUDE.md` | Per-project context template |
| `templates/project-CODEX.md` | Optional phased execution plan template |
| `resources/example-agent.md` | Format reference for agent instruction files |
| `projects/` | Contains project folders created during kickoff |

---

## How to keep context clean across sessions

The system stays current through three commands you can use in chat at any time:

**`start session`** — tells the assistant to orient itself before you begin work. It reads your active projects, confirms where things stand, and asks what you want to focus on. Use this at the top of any working session so nothing gets assumed.

**`end session`** — triggers a context save. The assistant updates your project file with decisions made, notes any open questions, rewrites the "next session" section with clear next steps, and updates the project status in `memory/projects.md` if anything changed. This is how continuity carries forward — run it before you close out.

**`new project`** — kicks off a new project. The assistant asks for a name, type, and description, creates the project folder and files, and adds it to the project index. You don't create or touch any files manually.

Everything else — adding shorthand to the glossary, keeping project files in sync — happens in the background as you work. The three commands above are the only thing you need to remember.

---

## Release notes

See `CHANGELOG.md` for what's included in this release.

---

## License

MIT
