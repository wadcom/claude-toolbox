---
description: Implement the next backlog item
---

You are tasked with implementing the next backlog item for an initiative. This
includes evaluating readiness, planning, and implementing — all in one flow.

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

### Phase 1: Load Context

1. Ask the user to provide the work-plan directory. Then read FULLY the
`goal`, `spec`, `status` and `backlog` artifacts from that directory. This
will provide you with the necessary context.

2. Identify the top item in the backlog. This is what you will work on.

### Phase 2: Evaluate Readiness

3. Evaluate whether the top item has enough details to be worked on immediately.
It is expected that the item doesn't spell out every single detail — only reject
it if ambiguity is so significant that it can't be resolved with a few simple
questions. If the item needs refinement, explain which aspects are unclear and
STOP HERE.

4. Evaluate effort. If the item would take a senior engineer more than 20
minutes of focused work, recommend splitting it and STOP HERE.

5. If there are details that need clarification, work with the user iteratively
to get the required clarity. Ask ONE question at a time.

### Phase 3: Plan

6. You **MUST** enter Plan mode by calling the `EnterPlanMode` tool before
drafting the plan. Do not describe the plan in regular chat output — the plan
must be presented via `ExitPlanMode` so the user can explicitly approve or
reject it.

7. Create an implementation plan for the item using the context from goal, spec,
and status. The plan should contain important high-level details without being
overly specific. A senior developer should be able to review the overall design
and key decisions without being bogged down by minutia.

8. **HARD GATE**: Do NOT call `Edit`, `Write`, `NotebookEdit`, or any other
file-modifying tool until the user has explicitly approved the plan (e.g.
"approve", "yes", "go ahead", "lgtm"). Silence, a thumbs-up emoji alone, or a
question about the plan are NOT approval. If the user requests changes, revise
the plan and re-submit via `ExitPlanMode` — keep iterating until approval is
explicit.

### Phase 4: Implement

9. Implement the plan. Track your progress using the task tools. If the plan
specifies success criteria, make sure they are met before reporting completion.

10. Write a walkthrough of the changes to `step-XY-walkthrough.html` in the
work-plan directory, where XY is the step number from the backlog item (e.g.
`step-03-walkthrough.html`).
Use the **linear walkthrough** approach: present information as a guided
narrative where each piece builds naturally on what came before. The reader
should never encounter an unexplained concept — every idea is introduced before
it is referenced. Structure the material so it reads top-to-bottom without
requiring the reader to jump ahead or back.

This contrasts with a "reference" style that groups by category (e.g. all types,
then all functions). Instead, introduce concepts in the order a newcomer would
need them to build understanding incrementally.

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
together. Cut whole topics instead: line-by-line narration, details visible in
the code at a glance, restatements of what names already say. Write what
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
focused, and pair it with a sentence saying what to look at. Skip diagrams
when prose is just as clear; do not include them in chat summaries.

11. **Fresh-eyes review of the walkthrough.** Launch a subagent whose ONLY
input is the walkthrough file — give it no diff, no plan, and no conversation
context. Instruct it to read the file and, for each paragraph, either restate
the meaning in its own words or flag it: list every term it cannot unpack and
every reference to context it does not have. Rewrite the flagged passages and
re-run the review until nothing is flagged. This is the only honest "cold
reader" test — the author always has too much context to perform it.

12. Present a brief summary to the user and point them to the walkthrough
file.

13. Once done, update `status.html` in the work-plan directory, marking what
you've done (see "Marking Completion" below).

14. If there **were** deviations from the plan, **briefly** describe them in
`status.html`. Be factual (what is the deviation) and provide a very short
rationale ("couldn't use X from Y because of circular dependency"). If there
were **no** deviations, do not add anything beyond the completion marker.

15. Ask the user if they are satisfied with the result. If not, ask for
feedback and keep working until the user is satisfied. When follow-up
adjustments are made, update `step-XY-walkthrough.html` to reflect the final
state of the changes and repeat the fresh-eyes review.

16. Remove the completed item from `backlog.html`.

### Marking Completion

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