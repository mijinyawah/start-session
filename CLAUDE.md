# Memory

## Setup

<!--
If this section exists, setup is not complete.
Run the flow below once, then delete this entire Setup section.
-->

### Setup flow

Note for the assistant: session commands (start session, end session, new project) are available to all users — no mode selection needed. Steps 4 and 5 are conditional; ask before running each one. Agents can always be added later even if skipped here.

Step 0 - Orientation
- Introduce the Memory Engine: this file stores context about who the user is, how they work, and where their projects stand — so they don't have to re-explain it each time.
- Tell the user setup covers identity, tools, projects, and a few behavior preferences. It takes about 5–10 minutes.

Step 1 - Confirm known context
- Summarize anything already known from this session.
- Ask the user to confirm or correct it.

Step 2 - Fill sections one at a time
Before asking for each section, briefly tell the user what the information enables — so questions feel purposeful, not interrogative.

- My User: name, role, location.
  Why: role calibrates explanation depth and vocabulary; location helps if the user references time zones or region-specific tools.

- My User's Work: employer or primary work context, one-line description.
  Why: helps orient to the nature and constraints of their projects (freelance vs. internal, audience, scope).

- My User's Tools: the tools they use regularly and what for.
  Why: this is the most directly useful field — knowing their stack shapes every troubleshooting response, suggestion, and shortcut.

- Our Projects: ask whether they want a project naming convention (e.g. initials + category letter + number, like HS-V01-reel). Explain it's optional but makes project kickoff and tracking cleaner. If yes, document the format they choose. If no, note that and remove the convention guidance from this section.

- My User's Workflow: primary machine, OS, storage/backup setup, typical project types.
  Why: OS and machine affect file paths, terminal commands, and compatibility advice.

- User Communication Preferences: directness, formatting, tone.
  Why: shapes how every future response is structured and delivered.

Step 3 - Hard Rules review
- Before reviewing, explain the purpose of this section: these rules exist to reduce hallucination, drift, and inconsistency across sessions and projects. They tell the assistant how to behave when uncertain, what to prioritize, and when to push back.
- Explain each rule briefly.
- Ask what to keep, change, remove, or add.

Step 4 - Technical calibration (conditional)
- Ask: "Do you ever work in a terminal, write code or scripts, or troubleshoot software at a technical level?"
- If yes: ask what kind of technical work, how comfortable they are, and what OS and tools they use. Write a calibrated summary in Technical Experience.
- If sometimes / it depends: ask what that looks like for them (expressions in creative tools, self-hosted setups, hardware troubleshooting, etc.). Write a light summary in Technical Experience noting the context.
- If no: note "No technical work planned" in Technical Experience and move on.

Step 5 - Agents (conditional)
- Ask: "Do you want to set up any custom behavior modes? For example — a research mode that cites every source, or a debug mode that goes step by step. You can always add these later just by asking."
- If yes: ask for a name, trigger phrase(s), and what the agent should do. Create the instruction file at `resources/[agent-name].md` (follow the format in `resources/example-agent.md`). Add a row to the Custom Agents table in this file.
- If no: skip. No further explanation needed.
- The user never edits `resources/` files directly. The assistant maintains them — "add a research agent" or "tweak the debug mode" is enough.

Step 6 - Finalize
- Summarize what was captured and confirm with the user.
- Populate all sections below with the information gathered.
- Delete this entire Setup section.
- Close with this message to the user:
  "Your context is saved in this folder and will be available every time we work together. You can ask me to update or change anything at any time. When you're ready to bring a project into the system, just say new project and I'll set it up.

  A few commands worth knowing:
  - start session — I'll orient to your active projects and ask what you want to work on
  - end session — I'll save your progress and set up clear next steps for next time
  - new project — I'll create a tracked project folder with all the context I need"

Fallback command if this does not trigger automatically: `run onboarding now`

<!-- END SETUP -->

---

## My User

**[Your name]** - [Role / title]
Based in [City, State/Country]
Contact: [email or preferred handle]

---

## My User's Work

**[Employer or main context]** - [One-line description]

---

## My User's Tools

| Tool | What I use it for |
|------|-------------------|
| **[Tool name]** | [Use case] |

---

## Our Projects

Suggested naming convention for projects (optional — adapt or remove if you don't want one):
- **[PREFIX]** = your initials or a team abbreviation
- **[category letter]** = A/App, W/Web, B/Bot, V/Video, D/Design, etc.
- **[number]** = two-digit sequential ID inside category
- **[slug]** = short kebab-case name

Example IDs:
- `[PREFIX]-A01-[short-slug]`
- `[PREFIX]-W02-[short-slug]`

Project index file: `memory/projects.md` — single source of truth for all projects across all states (WIP, Live, Complete, On Hold, Shelved, Idea). Update the status emoji on a project's line when its state changes; don't move it between files.

If you don't want a naming convention, remove this entire section.

---

## My User's Workflow

- **Primary machine:** [device]
- **OS:** [macOS / Windows / Linux]
- **Storage / backup:** [NAS / cloud / external]
- **Project types:** [what they usually build]

---

## User Communication Preferences

- [Directness/detail preferences]
- [Formatting preferences]
- [Tone preferences]

---

## Technical Experience

[Fill during setup. If no technical work is planned, state that explicitly.]

---

## Hard Rules

These apply to every session:

- If source material is inaccessible, say so clearly.
- Distinguish recalled knowledge from verified knowledge.
- Do not promise compatibility without version/environment context.
- Name at least one failure mode when proposing a solution.
- Confidence must track evidence.
- Cite sources for claims and recommendations whenever possible.
- For technical/software guidance, prioritize current documentation.

---

## Session Behavior

These are protocol instructions for session handling.

Mode note: These protocols are always available. The assistant runs them when invoked — it does not proactively prompt for session start/end unless the user has established that habit. Run them when asked; otherwise stay passive.

Reliability note:
- Trigger phrases are protocol instructions, not hard automations. If a flow doesn't trigger, type the command directly in chat: `run onboarding now` / `start session` / `end session` / `new project`.

### Session Start

Triggers:
- `start session`
- any equivalent phrase requesting session startup

Flow:
1. If user names a project: read `projects/[project-name]/CLAUDE.md` and confirm orientation.
2. If user wants something new: run Project Kickoff flow.
3. If user does not specify: read `memory/projects.md`, list projects whose status is 🔵 WIP or 🟢 Live, and ask which one to resume.

Always confirm orientation before execution.

### Session End

Triggers:
- `end session`
- `session end`
- `save session`
- `save progress`
- `wrap up`

Flow:
1. Update active project `CLAUDE.md` (status, decisions, open questions, changes).
2. Update `Last updated` date in project header.
3. Update project status in `memory/projects.md` if it changed — change the status emoji (🔵/🟢/✅/⏸️/📦) on that project's line. Don't move it between files; there's only one file.
4. Rewrite `## Next Session` with precise next actions.
5. Confirm what was saved.

---

## Agents

Agents are optional behavior modes activated by trigger phrases.

Mode note: Agents are always available on demand. If none were set up during setup, the user can request one at any time — "add a research agent" or "add a debug mode" is enough. The assistant creates the instruction file and adds a row to the Custom Agents table.

### Project Kickoff Agent

Triggers:
- `new project`
- `start a new project`
- `kick off [X]`
- `I want to build [X]`

Flow:
1. Ask for project name, type, one-line description, and whether `CODEX.md` is needed.
2. Read `memory/projects.md` to determine the next project ID. Find the highest valid ID number (ignoring template placeholders like `[ID-01]`) across all category sections including Ideas / Queue, and increment by 1. If no valid IDs exist yet, start at `01`.
3. Create new folder under `projects/` using the naming convention.
4. Create `CLAUDE.md` from `templates/project-CLAUDE.md` and prefill known fields.
5. If requested, create `CODEX.md` from `templates/project-CODEX.md`.
6. Add a line to `memory/projects.md` under the appropriate category section: `- **[ID] — [Name]** 🔵 WIP — [one-line description].`
7. Confirm setup and ask for first task.

### Custom Agents

| Agent | Triggers | What the assistant should do |
|-------|----------|-----------------------|
| | | |
