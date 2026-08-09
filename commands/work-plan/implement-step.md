---
description: Implement a backlog item from a previously approved plan
---

You are tasked with implementing a backlog item from a plan artifact that
`/work-plan:plan-next` produced and the user approved. Do not re-plan and do
not re-open the plan's decisions.

Step numbering restarts in each section; follow the sections in order.

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

## Execution Modes

Pick the wrap-up section based on where you run:

- **Local session** (default): the user reviews the result in this
  conversation. Do NOT commit — committing is the user's job.
- **Remote session** (environment variable `CLAUDE_CODE_REMOTE` is `true`):
  the user reviews the result as a pushed branch. Never wait for mid-run
  input; if required information is missing, stop and report the gap instead
  of asking.

## Process Steps

### Load Context

1. Determine the work-plan directory from the kickoff message, or ask the
user. Then read FULLY the `goal`, `spec`, `status` and `backlog` artifacts
from that directory.

2. Read the plan from `step-XY-plan.html`, where XY is the step number of the
top backlog item. If the file is missing, STOP and report that the item has
no approved plan (`/work-plan:plan-next` creates one).

### Implement

1. Implement the plan. Track your progress using the task tools. If the plan
specifies success criteria, make sure they are met before reporting completion.

2. Update `status.md` in the work-plan directory, marking what you've done
(see "Marking Completion" below).

3. If there **were** deviations from the plan, describe them in `status.md` as
ONE indented line per deviation. Be factual (what is the deviation) and give a
very short rationale ("couldn't use X from Y because of circular dependency").
If there were **no** deviations, do not add anything beyond the completion
line.

### Wrap Up (local session)

1. Present a brief summary of the changes to the user, then suggest a concise
commit message for the work.

2. Ask the user explicitly whether they want a walkthrough of the changes, or
any adjustments to the work just done. Write a walkthrough only if the user
asks for one (see "Walkthrough (On Request)" below).

3. If the user asks for adjustments, keep working until the user is satisfied.
When a walkthrough file already exists, update it to reflect the final state of
the changes. Repeat the fresh-eyes review only when the update names a concept
the file did not name before.

4. Remove the completed item from `backlog.md`.

### Wrap Up (remote session)

1. Remove the completed item from `backlog.md`.

2. Commit all changes — code, tests, `status.md`, `backlog.md` — on the
session branch. Use the completion summary as the commit title.

3. Push the branch so the user can review the changes as a pull request.

4. Present a brief summary: what changed, test results, and the branch name.

### Walkthrough (On Request)

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

### Marking Completion

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