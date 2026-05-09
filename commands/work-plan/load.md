---
description: Load initiative context for free-form discussion
---

You are loading context for an existing initiative to enable free-form discussion
with the user.

## Artifact Files

Initiative artifacts (`goal`, `spec`, `backlog`, `status`, `step-XY`,
`step-XY-walkthrough`) are stored as HTML files in the work-plan directory.

### Reading

When asked to read an artifact named `NAME`, check the target directory for
both `NAME.html` and `NAME.md`. Prefer `.html` if both exist; otherwise read
whichever is present. References like `goal.md` from the user should be
treated as the `goal` artifact regardless of extension — locate it the same
way.

### Writing

Always write artifacts as `.html`. When writing an artifact, if its `.md`
sibling exists in the same directory (legacy from before the HTML
migration), delete the `.md` file in the same step so only the HTML version
remains.

### Format

Use semantic markup:

- `<h1>` for the document title; `<h2>`/`<h3>` for sections.
- `<p>` for paragraphs.
- `<ul>`/`<ol>` with `<li>` for lists.
- `<strong>` for entity/component names.
- `<code>` for fields, methods, paths, and other technical terms.
- `<pre><code>` for multi-line code or pattern blocks.
- `<a href="...">` for links.

Do not include `<html>`, `<head>`, or `<body>` wrappers — the artifacts are
content fragments, not full pages.

## Process Steps

1. Ask the user to provide any file from the initiative directory (e.g., the
`goal`, `spec`, `backlog`, or any `step-*` artifact). Then read FULLY the
`goal`, `spec` and `status` artifacts located in that directory. For example,
if user mentioned file `a/b/c/goal.html`, also read the `spec` and `status`
artifacts in `a/b/c/`.

2. Check if there are any `step-*.html` (or legacy `step-*.md`) files in the
directory. Do NOT read them now, but note their existence. These contain
detailed implementation plans for individual backlog items and can be
consulted if more details are needed during the discussion.

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
- Feel free to read `step-*` files or the `backlog` artifact during the
  discussion if they become relevant