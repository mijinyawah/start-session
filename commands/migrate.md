---
description: Add missing sections from newer versions without overwriting existing content
argument-hint: ""
---
# /migrate

Add new sections and files to an existing start-session workspace after a plugin update. Always additive — never removes or overwrites existing user content.

## When to run

Run this after a plugin update that introduces new template sections or files. The plugin's changelog or update notes will say when a migration is needed.

## Flow

1. Read the user's existing `CLAUDE.md`. Check which sections are present.

2. Check for missing sections by comparing against the current scaffold template at `${CLAUDE_PLUGIN_ROOT}/scaffold/CLAUDE.md`. Sections to check:
   - My User
   - My User's Work
   - My User's Tools
   - Our Projects
   - References ← added in v1.4.0; may be missing for older users
   - My User's Workflow
   - User Communication Preferences
   - Technical Experience
   - Hard Rules
   - Custom Agents table

3. For each missing section: append it to the user's `CLAUDE.md` with a placeholder value and a comment noting it was added by migration. Tell the user to fill it in.

4. Check for missing workspace files:
   - `memory/glossary.md` — create from scaffold if missing
   - `resources/example-agent.md` — create from scaffold if missing
   - `templates/project-CLAUDE.md` — create from scaffold if missing
   - `templates/project-CODEX.md` — create from scaffold if missing
   - `projects/` directory — create with `.gitkeep` if missing

5. Do not modify any section that already exists. Do not remove any content, even if it's now handled by the plugin (e.g. Session Behavior, Agents protocols). Existing content is always preserved.

6. Confirm what was added. List each section and file created, and prompt the user to fill in any placeholders.
