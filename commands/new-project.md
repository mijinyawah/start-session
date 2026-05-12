---
description: Kick off a new tracked project with a context file and project index entry
argument-hint: "<project-name>"
---
# /new-project

Kick off a new project. Creates a tracked project folder with a populated context file and registers it in the project index.

## Flow

1. Ask for: project name, type (Tool / Website / Bot / Video / Design / Experiment / Other), one-line description, and whether a phased CODEX execution plan is needed.

2. Read `memory/projects.md` to determine the next project ID. Find the highest valid ID number across all category sections (ignore template placeholders like `[ID-01]`). Increment by 1. If no valid IDs exist yet, start at 01. Apply the user's naming convention from `CLAUDE.md` (under "Our Projects"). If no convention exists, ask the user what ID format to use.

3. Check if a folder already exists in `projects/` matching the new slug. If one exists, ask the user if they meant to resume it instead.

4. Create the project folder: `projects/[id-slug]/`

5. Create `projects/[id-slug]/CLAUDE.md` from the template at `${CLAUDE_PLUGIN_ROOT}/scaffold/templates/project-CLAUDE.md`. Pre-fill: project name, ID, type, owner (from the user's CLAUDE.md), one-line description, and started date. Leave Tech Stack, Architecture, Design Direction, and Conventions as TBD.

6. If a CODEX plan was requested, create `projects/[id-slug]/CODEX.md` from `${CLAUDE_PLUGIN_ROOT}/scaffold/templates/project-CODEX.md`. Pre-fill the project name.

7. Add a line to `memory/projects.md` under the appropriate category section:
   `- **[ID] — [Project Name]** 🔵 WIP — [one-line description].`
   If the category doesn't exist yet, create a new section for it.

8. Confirm the project is set up and ask what to work on first.
