---
description: Orient yourself at the top of every session — load project context and pick up from where you left off
argument-hint: "[project-name]"
---
# /start-session

Orient to the user's workspace before beginning work. Always confirm orientation before execution.

## Flow

1. Check whether the user named a specific project in their message.

   - **Named a project** → find the matching folder in `projects/`. Match on slug, ID, or name (fuzzy match is fine). Read that project's `CLAUDE.md`. Summarize: project name, current status/phase, what was last worked on, and next steps. Confirm orientation.

   - **Said they want to start something new** → tell them to run `/new-project`, or ask if they'd like to do that now.

   - **Didn't specify** → read `memory/projects.md`. List only projects whose status is 🔵 WIP or 🟢 Live (project ID, name, one-line description). Ask which one to resume. Once chosen, read that project's `CLAUDE.md` and confirm orientation as above.

2. Check for leftover checkpoints: if `projects/[project-slug]/.session-checkpoints.md` exists, read it and summarize what was captured. Ask the user if they want to incorporate those notes or discard them.

3. Confirm readiness — which project, where things left off, any open checkpoints. Do not start working until the user confirms.
