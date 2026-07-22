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