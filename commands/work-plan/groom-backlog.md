---
description: Groom initiative's backlog
---

You are tasked with grooming backlog for an existing initiative.

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

1. Ask the user to provide a backlog file (named `backlog.md`, or
`backlog.html` for older initiatives). Then read FULLY that file, and also the
`goal`, `spec` and `status` artifacts located in the same directory.

For example, if user has provided a plan in file `a/b/c/backlog.md`, also
read the `goal`, `spec` and `status` artifacts in `a/b/c/`. It will provide
you with the necessary context.

2. Go through each item of the backlog one by one. Make sure you understand
what each item is about. Track your progress using TodoWrite tool. Note which
items seem obsolete. Note which items seem to be too small (requiring less 
than 15 minutes worth of senior engineer's work).

3. Provide your recommendations to the user to: a) drop obsolete items; b) 
group small items into larger ones; c) change the order. Explain your reasons
for each recommendation. Ask user ONE QUESTION AT A TIME. When presenting
results, always refer to backlog items by titles ("Create documentation")
rather than their positions ("items 4 and 5").

4. Process user's feedback. Present the resulting backlog to the user and ask
if they are satisfied. If no, go back to item 2 and repeat. 

5. Write out the updated backlog. Make sure that you follow the backlog
principles outlined below. Specifically, make sure that there are no redundant
details.

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

A backlog item is a title. The default is NO description at all. Add one only
when the title alone would not recall what the item is about, and then keep it
to 3 sentences at most.

A description states WHAT to do. It never states why the item matters, how the
code works today, or which files to touch. That belongs in `goal`, `spec`, or
the step plan.

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

````markdown
# [Initiative Name] Backlog

## Highest priority item

## Next priority item

[May have up to 3 sentences of description]

## Another item

## Low priority item which might need context

[May have up to 3 sentences of description]

...
````

**IMPORTANT**: if the item title is enough to recall what it is about, it
SHOULD NOT have any description! In the example above, "Another item" is
described well enough by its title, so it carries no description.

Before you write the backlog out, reread every description you wrote and
delete the ones the title already covers. Most of them.
