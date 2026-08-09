---
description: Plan the next backlog item without implementing it
---

You are tasked with planning the next backlog item for an initiative:
evaluate readiness, produce an implementation plan, and persist the approved
plan so a separate session can implement it. Do NOT implement anything in
this session.

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

## Process Steps

### Load Context

1. Ask the user to provide the work-plan directory. Then read FULLY the
`goal`, `spec`, `status` and `backlog` artifacts from that directory. This
will provide you with the necessary context.

2. Identify the top item in the backlog. This is what you will work on.

### Evaluate Readiness

1. Evaluate whether the top item has enough details to be worked on immediately.
It is expected that the item doesn't spell out every single detail — only reject
it if ambiguity is so significant that it can't be resolved with a few simple
questions. If the item needs refinement, explain which aspects are unclear and
STOP HERE.

2. Evaluate effort. If the item would take a senior engineer more than 20
minutes of focused work, recommend splitting it and STOP HERE.

3. If there are details that need clarification, work with the user iteratively
to get the required clarity. Ask ONE question at a time.

### Plan

1. You **MUST** enter Plan mode by calling the `EnterPlanMode` tool before
drafting the plan. Do not describe the plan in regular chat output — the plan
must be presented via `ExitPlanMode` so the user can explicitly approve or
reject it.

2. Create an implementation plan for the item using the context from goal, spec,
and status. The plan should contain important high-level details without being
overly specific. A senior developer should be able to review the overall design
and key decisions without being bogged down by minutia.

3. **HARD GATE**: Do NOT call `Edit`, `Write`, `NotebookEdit`, or any other
file-modifying tool until the user has explicitly approved the plan (e.g.
"approve", "yes", "go ahead", "lgtm"). Silence, a thumbs-up emoji alone, or a
question about the plan are NOT approval. If the user requests changes, revise
the plan and re-submit via `ExitPlanMode` — keep iterating until approval is
explicit.

### Persist the Plan

1. After approval, write the plan to `step-XY-plan.html` in the work-plan
directory, where XY is the step number from the backlog item (e.g.
`step-03-plan.html`).

A separate session with no access to this conversation may implement from this
file, so write it for a cold reader:

- Open with the backlog item text, quoted verbatim.
- Fold the answers from the clarification questions into the plan text. A
  decision that lives only in this conversation is lost.
- Keep the approved altitude: key decisions and design shape, not minutiae.
- State the success criteria, if the plan has any.

### Wrap Up

1. Tell the user the plan artifact path and stop. Remind them:

- to make the plan available to remote sessions, commit and push it;
- `/work-plan:implement-step` implements it, locally or in a cloud session.