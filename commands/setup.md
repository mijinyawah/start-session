# /setup

Run first-time onboarding for the start-session memory system. This command scaffolds the user's workspace and populates it with their context.

## When to run

Run this command once — the first time the user sets up start-session in a new workspace. If a populated `CLAUDE.md` already exists in the working directory, confirm before overwriting.

## Branching directive

Whenever a step branches based on the user's answer, use the platform's native multi-choice UI (e.g. AskUserQuestion in Claude CoWork) with multi-select where appropriate and a free-text "other / type your own" option. Fall back to a numbered list with a final "other" option if no native multi-choice UI is available.

---

## Onboarding flow

Note: session commands (/start-session, /end-session, /new-project) are available to all users immediately after setup. Steps 5, 6, and 7 are conditional — ask before running each one.

### Step 0 — Orientation

Introduce the memory system:

> "This setup creates a workspace the assistant reads at the start of every session — so you never have to re-explain who you are, how you work, or where your projects stand. Setup covers your identity, the tools you use, where your work lives, and any projects you want to bring in now. It takes about 10–15 minutes."

### Step 1 — Confirm known context

Summarize anything already known from this session (name, role, tools mentioned, etc.). Ask the user to confirm or correct it.

### Step 2 — Fill identity sections

Before asking for each section, briefly explain what the information enables.

**My User** — name, role/title, location, contact.
_Why: role calibrates explanation depth and vocabulary; location helps with time zones and region-specific tools._

**My User's Work** — employer or primary work context, one-line description.
_Why: orients the assistant to the nature and constraints of their projects (freelance vs. internal, audience, scope)._

**My User's Tools** — two-step capture:
- Step 1: ask their primary occupation (e.g. "motion designer," "product manager," "systems engineer").
- Step 2: show a curated list of tools commonly used in that occupation, plus a free-text option for custom tools. User selects from list and adds their own.
_Why: knowing their stack shapes every troubleshooting response, suggestion, and shortcut._

**Our Projects — naming convention** — present the default convention format with examples:
- Format: `[PREFIX]-[CategoryLetter][##]-[slug]` (e.g. `HS-V01-reel`, `BM-W02-site-redesign`)
- Multi-choice: keep the default / modify it / skip having one entirely.
- If "modify": ask what format they want and document it.
- If "skip": note no convention in use.
_Why: consistent naming makes project tracking and kickoff much cleaner._

**My User's Workflow** — primary machine, OS, storage/backup, typical project types.
_Why: OS and machine affect file paths, terminal commands, and compatibility advice._

**User Communication Preferences** — directness, formatting, tone.
_Why: shapes how every future response is structured and delivered._

### Step 3 — Reference memory

Tell the user:
> "Quick capture — where does most of your project work live? Knowing this lets me point you back to your own systems instead of guessing."

Multi-select options: Notion · Google Drive · Local folder(s) · Slack · Specific dashboards/tools · Other (free text).

For each selected option, ask a brief follow-up:
- Notion → workspace URL or main page
- Google Drive → folder name or link
- Local folder(s) → root path(s)
- Slack → channel names
- Specific dashboards/tools → URL and one-line purpose
- Other → free text

### Step 4 — Hard Rules review

Explain before asking:
> "These rules tell the assistant how to behave when uncertain — what to prioritize, when to push back, and how to handle missing information. They exist to reduce hallucination and drift across sessions."

Present the default rules (see scaffold/CLAUDE.md for the list). Ask what to keep, change, remove, or add.

### Step 5 — Technical calibration (conditional)

Ask: "Do you ever work in a terminal, write code or scripts, or troubleshoot software at a technical level?"

Multi-choice options: Yes · Sometimes / it depends · No · Other (free text).

- If yes: ask what kind of technical work, how comfortable they are, and what OS/tools they use. Write a calibrated summary.
- If sometimes: ask what that looks like (e.g. expressions in creative tools, self-hosted setups, hardware troubleshooting). Write a light summary noting the context.
- If no: note "No technical work planned" and move on.

### Step 6 — Custom agents (conditional)

Ask: "Do you want to set up any custom behavior modes? For example — a research mode that cites every source, or a debug mode that goes step by step. You can always add these later just by asking."

Multi-choice options: Yes — let's set one up now · Not now / I'll add later · Tell me more first · Other (free text).

- If yes: ask for a name, trigger phrase(s), and what the agent should do. Create `resources/[agent-name].md` using the format in `resources/example-agent.md`. Add a row to the Custom Agents table in CLAUDE.md.
- If no: skip. No further explanation needed.

### Step 7 — Project intake (conditional)

Ask: "Are there any projects you're already working on that you want to bring in? I'll set them up so you can pick up right where you left off."

Multi-choice options: Yes — one project · Yes — multiple · Not right now / I'll add later · Other.

- If yes (one or multiple): cap at 3 projects in this first session. Tell the user they can add more anytime via `/new-project`.
- For each project, ask: "Do you have a brief, doc, or notes, or should we walk through it together?"
  - Multi-choice: I have a doc or link · Walk me through it · Skip this one.
  - **Doc-import path**: user pastes or shares the doc/link. Extract: project name, type, current phase, key decisions already made, what's next, where it lives. Confirm extraction. Then run the `/new-project` flow with prefilled fields.
  - **Interview path**: ask 6 short questions covering the same fields. Then run `/new-project` with the answers.

### Step 8 — Finalize and write workspace

Summarize everything captured across all steps, including any projects. Confirm with the user.

Then write the following files to the current working directory:

1. **CLAUDE.md** — populate with all user data from this session. Use the template at `${CLAUDE_PLUGIN_ROOT}/scaffold/CLAUDE.md`. Fill every section; remove placeholder text. Do not include session protocols or agent flow instructions (those live in the plugin commands). The Setup section is not included in the output.

2. **AGENTS.md** — copy from `${CLAUDE_PLUGIN_ROOT}/scaffold/AGENTS.md` as-is.

3. **memory/projects.md** — copy from `${CLAUDE_PLUGIN_ROOT}/scaffold/memory/projects.md`. If projects were onboarded in Step 7, they should already be added via the /new-project flow.

4. **memory/glossary.md** — copy from `${CLAUDE_PLUGIN_ROOT}/scaffold/memory/glossary.md` as-is.

5. **resources/example-agent.md** — copy from `${CLAUDE_PLUGIN_ROOT}/scaffold/resources/example-agent.md` as-is.

6. **templates/project-CLAUDE.md** — copy from `${CLAUDE_PLUGIN_ROOT}/scaffold/templates/project-CLAUDE.md` as-is.

7. **templates/project-CODEX.md** — copy from `${CLAUDE_PLUGIN_ROOT}/scaffold/templates/project-CODEX.md` as-is.

8. **projects/.gitkeep** — create an empty file to preserve the projects directory.

After writing all files, close with:

> "Your context is saved in this folder and will be available every time we work together here. You can ask me to update or change anything at any time.
>
> [If projects were brought in:] I've also set up [N] project[s] so you can pick up right where you left off — just say their name or run /start-session and we'll resume.
>
> [If no projects yet:] When you're ready to bring a project in, run /new-project and I'll set it up.
>
> A few commands worth knowing:
> - /start-session — I'll orient to your active projects and ask what you want to work on
> - /end-session — I'll save your progress and set up clear next steps for next time
> - /new-project — I'll create a tracked project folder with everything I need"
