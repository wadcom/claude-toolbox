Write a walkthrough of the changes only when the user asks for one. Never
write it as part of the default flow.

1. Write the walkthrough to `step-XY-walkthrough.html` in the work-plan
directory, where XY is the step number of the plan artifact for this work (e.g.
`step-03-walkthrough.html`).
{% include 'linear-walkthrough.md' %}

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
