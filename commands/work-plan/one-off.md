---
description: Implement a small change without formal backlog process
---

You are tasked with implementing a small, one-off change to an existing
initiative without going through the formal backlog/spec preparation process.

This command is ideal for quick fixes, minor improvements, or small features
that don't warrant a full planning cycle.

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

1. Ask the user to provide a goal file (named `goal.html`, or `goal.md` for
older initiatives). Then read FULLY the `spec`, `backlog` and `status`
artifacts located in the same directory as the goal. For example, if user
has provided a file `a/b/c/goal.html`, also read the `spec`, `backlog` and
`status` artifacts in `a/b/c/`. It will provide you with the necessary
context.

2. Ask the user what small change they want to implement.

3. Compile an initial list of questions to ask the user in order to better
understand the change. Use TodoWrite to track them.
  - **IMPORTANT**: each question should be put into a separate TODO item.

4. Iterate while the TODO list is not empty.
  - **IMPORTANT**: ALWAYS ask ONE question at a time
  - Take one item from the TODO list and ask the user this question. Then
  remove it from the list with TodoWrite tool.
  - Assess user's input and all available information, decide if you need to
  add more questions to the list. If so, use TodoWrite to update the list.

5. Write out the implementation plan to a file named `step-XY.html`
(`step-01.html` if there are no other `step-*` files yet, or the next
sequential number if there are).

The plan should contain important high level details without being overly
specific. A senior developer should be able to read this step plan and
review/verify overall design, key decisions etc. without being bogged down
by minutia.

The plan should be written so that if a developer reads `goal.html`,
`spec.html` and the plan, they would have complete context to immediately
implement the step.

6. Ask if the user is satisfied with the plan. If not, ask what needs to be
adjusted and iterate on the plan.

7. Implement the plan, following it exactly, step by step. Track your progress
using TodoWrite tool. If the plan specifies a success criteria, make sure that
is met before reporting completion.

8. Present a summary of what was done to the user.
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

9. Once you are done, create or update a file named `status.html` (located
in the same directory as `spec.html`), marking what you've done (see
"Marking Completion" below).

10. If there **were** changes to the original plan, **briefly** describe
them in `status.html` as well. Be factual (what is the deviation from the
plan) but provide a very short rationale ("couldn't use X from Y because of
circular dependency"). If there was **NO** changes, do not document anything
about deviations in the status.

11. Ask the user if they are satisfied with the result. If no, ask for the
feedback and keep working until the user is satisfied.

**IMPORTANT**: Do NOT update `backlog.html`. This is a one-off change that
bypasses the formal backlog process.

## Asking Questions

When asking questions, use the following guidelines:

1. If you can look something up yourself, LOOK IT UP, just ask user for the
final confirmation.

2. Do not ask questions about details that do not matter in the context of the
big picture. Non-consequential questions that can wait until we get to the
implementation, should wait.

3. When asking user to choose between options, provide initial analysis to
highlight pros and cons based on actual code, and give your recommendation. The
final decision should still be made by the user.

## Marking Completion

When marking item as completed, append a new entry to `status.html` in the
form `<p>COMPLETED step <X>: <SUMMARY></p>`.

`<X>` is the number of the completed step.

`<SUMMARY>` is a summary of the change, adhering to the following rules:
 * be 50 characters or shorter;
 * start with a capital letter;
 * be understandable without the context of the goal.

Examples:
 * GOOD: `<p>COMPLETED step 7: Extract helpers from Subscription tests</p>`
 * BAD: `<p>COMPLETED step 7: Extract _create_new()</p>` — not understandable
 without context.

Rule of thumb: everything after "step ..." should be usable as a good commit
title.