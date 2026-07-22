---
description: Adjust the goal/plan of an existing initiative
---

You are tasked with updating the goal or plan of an existing initiative. You
have to work with user iteratively and incrementally to understand required
changes and update the documents accodingly.

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
older initiatives). Then read FULLY the `backlog`, `spec` and `status`
artifacts located in the same directory as the plan. For example, if user
has provided a file `a/b/c/goal.html`, also read the `backlog`, `spec` and
`status` artifacts in `a/b/c/`. It will provide you with the necessary
context.

2. Ask the user what changes are needed to the current goal/spec. 

3. Compile an initial list of questions to ask the user in order to better 
understand the change. Use TodoWrite to track them.
  - **IMPORTANT**: each question should be put into a separate TODO item.

4. Iterate while the TODO list is not empty.
  - **IMPORTANT**: ALWAYS ask ONE question at a time
  - Take one item from the TODO list and ask the user this question. Then 
  remove it from the list with TodoWrite tool.
  - Assess user's input and all available information, decide if you need to 
  add more questions to the list. If so, use TodoWrite to update the list.

5. Once you are done, update `goal.html` to contain new business requirements
(if any). **IMPORTANT**: this file should not contain any technical details.

6. If needed, update `spec.html`. **IMPORTANT**: this file should contain
overall technical direction, without lower-level details and references to
volatile information (e.g. line numbers).

When rewriting `goal.html` or `spec.html`, maintain the linear walkthrough
structure.
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

7. Update `backlog.html`: remove obsolete items, add new ones, split/merge
items or update descriptions as appropriate. See backlog principles section
below.

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

## Backlog Principles

Backlog is a PRIORITIZED list of things to be done. Higher priority items are
at the top.

Backlog is a FLAT list, there is no nesting structure. Each item stands on its
own.

Backlog items are like rocks. When you break a rock, you get several rocks. So
are backlog items: they can be split into smaller items or grouped back into
larger ones.

Each backlog item should be a **vertical slice**: it delivers a small piece of
end-to-end functionality that can be checked or tested manually once
implemented. Prefer slicing that produces something observable (a new UI
element, an API response, a CLI output) over slicing by technical layer (e.g.
"add database schema", then "add service layer", then "add UI"). When vertical
slicing is not practical (e.g. pure infrastructure or foundational plumbing),
note explicitly why, and define what "done" looks like for that item.

Each backlog item can have a SHORT description (no more than 3 sentences).

The highest priority items (the ones we will work on next), should be the
smallest (e.g. no more than 20 minutes of focused work of a senior engineer)
and have more details.

Backlog must be comprehensible (no more than 15 items). To achieve this, 
lower-priority items may be grouped into more coarse ones. Alternatively, the
scope of the entire initiative may be reduced (with the approval of the user).

The most important is the order of the first few items. The further we go down
the list, the less important it is to precisely prioritize items against each
other.

### Backlog example

````html
<h1>[Initiative Name] Backlog</h1>

<h2>Highest priority item</h2>

<h2>Next priority item</h2>

<p>[May have up to 3 sentences of description]</p>

<h2>Another item</h2>

<h2>Low priority item which might need context</h2>

<p>[May have up to 3 sentences of description]</p>

...
````

**IMPORTANT**: if the item title is enough to recall what it is about, it 
SHOULD NOT have any description! In the example above, "Another item" is 
supposedly described well enough by its title, so it doesn't have any
description.
