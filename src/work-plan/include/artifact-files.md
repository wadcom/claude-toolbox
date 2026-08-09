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
