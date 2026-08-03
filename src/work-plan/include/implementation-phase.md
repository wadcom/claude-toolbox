### Implement

1. Implement the plan. Track your progress using the task tools. If the plan
specifies success criteria, make sure they are met before reporting completion.

2. Write a walkthrough of the changes to `step-XY-walkthrough.html` in the
work-plan directory, where XY is the step number from the backlog item (e.g.
`step-03-walkthrough.html`).
{% include 'linear-walkthrough.md' %}

3. **Fresh-eyes review of the walkthrough.** The author always has too much
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

4. Update `status.html` in the work-plan directory, marking what you've done
(see "Marking Completion" below).

5. If there **were** deviations from the plan, **briefly** describe them in
`status.html`. Be factual (what is the deviation) and provide a very short
rationale ("couldn't use X from Y because of circular dependency"). If there
were **no** deviations, do not add anything beyond the completion marker.
