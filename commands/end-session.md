# /end-session

Save session progress and set up clear next steps. Run before closing out a working session.

## Flow

1. Update the active project's `projects/[project-slug]/CLAUDE.md`:
   - Current status and phase
   - Any decisions made this session (add to Decisions Log)
   - Any open questions that surfaced
   - Anything that changed

2. Update the `Last updated` date in the project CLAUDE.md header to today's date.

3. If the project's status changed this session (new phase, completed, blocked, shelved) — update its line in `memory/projects.md`. Change the status emoji (🔵/🟢/✅/⏸️/📦) and update the description if needed. Do not move it between sections; there is only one file.

4. Rewrite the `## Next Session` section in the project CLAUDE.md with precise, actionable next steps — specific enough that the next session can resume without re-explanation.

5. If a `.session-checkpoints.md` file exists in the project folder, incorporate any relevant notes into the above and then delete it.

6. Confirm what was saved — list the files updated and the key things captured.
