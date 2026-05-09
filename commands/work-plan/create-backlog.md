---
description: Create backlog for initiative
---

You are tasked with creating backlog for an existing initiative. Work
iteratively with the user to define and prioritize backlog items.

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
older initiatives). Then read FULLY that file, and also the `spec` and
`status` artifacts located in the same directory.

For example, if user has provided a plan in file `a/b/c/goal.html`, also read
the `spec` and `status` artifacts in `a/b/c/`. It will provide you with the
necessary context.

2. Think hard to understand the difference between the current state and the
desired state, as described by the goal file.

3. Formulate the discovered differences as backlog items (following the
guidance in "Principles" section above).

4. Work iteratively with user to define the rough priorities. We don't need to
get bogged in details: it's important to understand what the first 3 priorities
are.

5. Write out the backlog according to priorities. Make sure that the top
priority items are well understood and scoped (confirm this with the user).

6. Repeat from item 4 until the user is satisfied with the backlog.

7. Make sure again that the backlog follows the described principles.

8. Write out the backlog to file named `backlog.html` in the same directory
where the goal file is located.