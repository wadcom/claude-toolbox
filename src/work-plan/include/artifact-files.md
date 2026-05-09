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
