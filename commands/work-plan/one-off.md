---
description: Implement a small change without formal backlog process
---

You are tasked with implementing a small, one-off change to an existing
initiative without going through the formal backlog/spec preparation process.

This command is ideal for quick fixes, minor improvements, or small features
that don't warrant a full planning cycle.

## Artifact Files

Initiative artifacts live in the work-plan directory. Each artifact has one
fixed format:

| Artifact | Format |
| --- | --- |
| `backlog` | Markdown (`.md`) |
| `goal` | HTML (`.html`) |
| `spec` | HTML (`.html`) |
| `status` | Markdown (`.md`) |
| `step-XY`, `step-XY-plan` | HTML (`.html`) |
| `step-XY-walkthrough` | HTML (`.html`) |

`backlog` and `status` are terse working files, not documents. `goal`, `spec`,
`step-XY-plan` and `step-XY-walkthrough` are the documents — put the narrative
there.

### Brevity of `backlog` and `status`

A reader scans `backlog` and `status` in a few seconds. Every sentence you add
costs that reader time, so write the fewest that still carry the fact.

- Never explain WHY in these two files. The reason belongs in `goal` or
  `spec`. A `status` line records what happened, not what motivated it.
- Never restate context the reader already has from `goal` or `spec`.
- Never add a section, a preamble, a summary, or a table of contents.
- Never carry code, file path lists, or design detail into these two files.

Reread every line you wrote into these two files before you save. Delete each
one that a reader could have guessed from the title above it.

### Reading

When asked to read an artifact named `NAME`, check the target directory for
both `NAME.html` and `NAME.md`. Prefer the format the table gives; otherwise
read whichever file is present. A reference like `goal.md` from the user means
the `goal` artifact regardless of extension — locate it the same way.

### Writing

Always write an artifact in the format the table gives. If a sibling file with
the other extension exists in the same directory (legacy from an earlier
format), delete that sibling in the same step, so only one version remains.

### HTML format

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

### Markdown format

Use plain CommonMark: `#` for the document title, `##`/`###` for sections,
`-` for lists, backticks for technical terms, and fenced blocks for code. Do
not embed HTML in a Markdown artifact.

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

8. Present a brief summary of what was done, then suggest a concise commit
message for the change.

9. Once you are done, create or update a file named `status.md` (located
in the same directory as `spec.html`), marking what you've done (see
"Marking Completion" below).

10. If there **were** changes to the original plan, describe them in
`status.md` as ONE indented line per deviation. Be factual (what is the
deviation from the plan) and give a very short rationale ("couldn't use X from
Y because of circular dependency"). If there were **NO** changes, do not
document anything about deviations in the status.

11. Ask the user explicitly whether they want a walkthrough of the change, or
any adjustments to the work just done. Write a walkthrough only if the user
asks for one (see "Walkthrough (On Request)" below). If the user asks for
adjustments, keep working until the user is satisfied.

**IMPORTANT**: Do NOT update `backlog.md`. This is a one-off change that
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

## Walkthrough (On Request)

Write a walkthrough of the changes only when the user asks for one. Never
write it as part of the default flow.

1. Write the walkthrough to `step-XY-walkthrough.html` in the work-plan
directory, where XY is the step number of the plan artifact for this work (e.g.
`step-03-walkthrough.html`).
Use the **linear walkthrough** approach: present information as a guided
narrative where each piece builds naturally on what came before. The reader
should never encounter an unexplained concept — every idea is introduced before
it is referenced. Structure the material so it reads top-to-bottom without
requiring the reader to jump ahead or back.

This contrasts with a "reference" style that groups by category (e.g. all types,
then all functions). Instead, introduce concepts in the order a newcomer would
need them to build understanding incrementally.

**Length follows the difficulty of the idea, not the size of the change.** Ask
how hard the change is to understand, then spend words on that alone:

- A mechanical change — a new flag, a moved function, a renamed field — needs a
  few paragraphs. Do not spell it out to the smallest detail.
- A hard concept — a new algorithm, a subtle invariant, a non-obvious tradeoff
  — gets as many words as it takes. Do not compress it to hit a length.

Most steps fall in the first group, so most walkthroughs are short. When you
write a long one, be able to name the difficult idea that earned the length.

**Write at the level of behavior, not implementation.** State what the code now
does that it did not do before, and what decision made it work that way. The
reader who wants line-by-line detail opens the diff. Do not tour the call
chain. Do not narrate each function in file order.

When a walkthrough runs long for any other reason, cut whole topics in this
order:

1. Tests. Name what they cover in one sentence. Do not list cases.
2. Helper functions that serve one caller. Fold them into the caller's
   paragraph or drop them.
3. Mechanics the code shows at a glance: renames, argument threading, import
   changes, moved code.
4. Any sentence that restates what a name already says.

**Write for a cold reader.** The reader has not seen the plan, the backlog, or
this conversation, and did not watch the work happen. Concretely:

- Never reference the process: no "the next backlog item", "as planned", "the
  existing X", "as discussed".
- Gloss every named function, term, or concept at first mention, in plain
  words: "`clear-hop?` (checks that a straight line between two points crosses
  no obstacle)".
- Do not coin shorthand ("the outline gate") without defining it first — and
  prefer not coining it at all.

**Problem before mechanism.** Open each change with one or two sentences on
the situation it handles: what exists, what goes wrong or is missing. Only
then describe how the code addresses it. A mechanism without its motivation is
unreadable.

**One change per section or paragraph.** A change is one function, one
behavior, one decision. Never chain two changes into one paragraph.

**Concise means fewer ideas, never denser sentences.** Keep the connective
tissue — the overall shape, the load-bearing decisions, how the pieces fit
together. Cut whole topics instead, in the order listed above. Write what
remains in short active sentences, one idea each. A plain paragraph the reader
understands beats a tight sentence they must decode.

**Show, don't abstract.** For algorithmic or geometric material, give one tiny
concrete scenario ("the goal sits inside a closed room; the search stops at
the doorway node") — it explains more than any abstract description.

Example — wrong: dense, coined jargon, references to the process:

> slide-along-incident-edges refines the winning node: each incident edge
> contributes the goal's perpendicular foot as a candidate, accepted only when
> it beats the current best distance and lies on an obstacle outline; the
> outline gate keeps the endpoint off tangent edges that cross open terrain.

Example — right: problem first, one idea per sentence, terms glossed:

> Problem: when the goal is unreachable, the search stops at the closest
> reachable graph node. Graph nodes sit on obstacle corners. The truly closest
> point often lies partway along an edge between corners.
>
> The fix: `slide-along-incident-edges` looks at every edge touching the
> winning node. For each edge it finds the point on that edge nearest to the
> goal. That point becomes the new endpoint only if it is closer to the goal
> and lies on an obstacle outline. The outline check matters because some
> edges cross open ground; a point there would leave the endpoint standing in
> the open, away from any wall.

**Use SVG diagrams when they help.** When the walkthrough is written to an
HTML artifact, embed inline `<svg>` diagrams wherever they convey structure,
flow, or relationships more clearly than prose — e.g. component dependencies,
state machines, before/after layouts, data flow. Keep each diagram small and
focused, and pair it with a sentence saying what to look at. A diagram often
replaces three paragraphs; prefer it when it does. Skip diagrams when prose is
just as clear; do not include them in chat summaries.

2. **Fresh-eyes review of the walkthrough.** The author always has too much
context to judge their own writing, so a subagent with none is the only honest
"cold reader" test. Run it once.

Launch one subagent on the Sonnet model. Its ONLY input is the walkthrough file
path — give it no diff, no plan, and no conversation context. Instruct it to
read the file and report **only blockers**, as a flat list:

- a term, name, or phrase it cannot unpack from the file alone;
- a reference to context the file does not contain.

Tell it to report at most eight items, to skip style opinions and suggested
rewrites, and to return an empty list when it finds none. Do not ask it to
restate paragraphs.

Fix what it reports. Do not run a second pass.

3. Point the user to the walkthrough file path.

## Marking Completion

When marking item as completed, append a new line to `status.md` in the form
`COMPLETED step <X>: <SUMMARY>`.

`<X>` is the number of the completed step.

`<SUMMARY>` is a summary of the change, adhering to the following rules:
 * be 50 characters or shorter;
 * start with a capital letter;
 * be understandable without the context of the goal.

Examples:
 * GOOD: `COMPLETED step 7: Extract helpers from Subscription tests`
 * BAD: `COMPLETED step 7: Extract _create_new()` — not understandable
 without context.

Rule of thumb: everything after "step ..." should be usable as a good commit
title.

`status.md` is a log of these lines and nothing else. Do not add headings,
prose, or a running narrative of the initiative.