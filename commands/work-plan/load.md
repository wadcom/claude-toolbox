---
description: Load initiative context for free-form discussion
---

You are loading context for an existing initiative to enable free-form discussion
with the user.

## Process Steps

1. Ask the user to provide any file from the initiative directory (e.g.,
`goal.md`, `spec.md`, `backlog.md`, or any `step-*.md` file). Then read FULLY
the files named `goal.md`, `spec.md` and `status.md` located in that directory.
For example, if user mentioned file `a/b/c/goal.md`, also read files
`a/b/c/spec.md` and `a/b/c/status.md`.

2. Check if there are any `step-*.md` files in the directory. Do NOT read them
now, but note their existence. These contain detailed implementation plans for
individual backlog items and can be consulted if more details are needed during
the discussion.

3. Provide a brief summary of the initiative context:
   - The goal (1-2 sentences)
   - Current status (what's done, what's in progress)
   - Note if step plans are available for reference

4. Ask the user what they'd like to discuss or explore regarding this initiative.

## Guidelines

- This command is for open-ended discussion, not for executing a specific
  workflow
- If the user wants to implement, groom, or adjust the plan, suggest the
  appropriate command (`/work-plan:implement`, `/work-plan:groom-backlog`,
  `/work-plan:adjust`, etc.)
- Feel free to read `step-*.md` files or `backlog.md` during the discussion if
  they become relevant