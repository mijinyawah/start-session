---
description: Save mid-session progress without ending the session
argument-hint: ""
---
# /checkpoint

Save progress mid-session without ending the session. Use this when the session is ongoing but something important should be preserved.

## Flow

1. Capture the current state: what's been decided, what's been built or changed, any open threads.

2. Write or append to `projects/[project-slug]/.session-checkpoints.md` in the active project folder. Each checkpoint entry should include the date/time and a brief summary of what was captured.

3. Confirm what was saved. The session continues normally.

## Note

`.session-checkpoints.md` is a temporary file. It is read and cleared when `/end-session` or the next `/start-session` runs. It is not a permanent record — that's what the project CLAUDE.md is for.
