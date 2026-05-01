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

3. Provide a brief summary of the initiative context.
Use the **linear walkthrough** approach: present information as a guided
narrative where each piece builds naturally on what came before. The reader
should never encounter an unexplained concept — every idea is introduced before
it is referenced. Structure the material so it reads top-to-bottom without
requiring the reader to jump ahead or back.

This contrasts with a "reference" style that groups by category (e.g. all types,
then all functions). Instead, introduce concepts in the order a newcomer would
need them to build understanding incrementally.

**Be concise, but keep the walkthrough.** Its job is to show how the parts fit
together — the overall shape, the load-bearing decisions, and how the new
pieces connect to each other and to the existing code. Preserve that
connective tissue. What to cut: details a reader can pick up at a glance from
the code or diff, restatements of what function names already say, and
line-by-line narration of changes. Prefer one tight sentence over a paragraph.
   Cover the goal, current status (what's done, what's in progress), and note if
   step plans are available for reference.

4. Ask the user what they'd like to discuss or explore regarding this initiative.

## Guidelines

- This command is for open-ended discussion, not for executing a specific
  workflow
- If the user wants to implement, groom, or adjust the plan, suggest the
  appropriate command (`/work-plan:implement-next`, `/work-plan:groom-backlog`,
  `/work-plan:adjust`, etc.)
- Feel free to read `step-*.md` files or `backlog.md` during the discussion if
  they become relevant