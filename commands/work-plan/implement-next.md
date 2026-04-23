---
description: Implement the next backlog item
---

You are tasked with implementing the next backlog item for an initiative. This
includes evaluating readiness, planning, and implementing — all in one flow.

## Process Steps

### Phase 1: Load Context

1. Ask the user to provide the work-plan directory. Then read FULLY the files
`goal.md`, `spec.md`, `status.md` and `backlog.md` from that directory. This
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

10. Write a walkthrough of the changes to `step-XY-walkthrough.md` in the
work-plan directory, where XY is the step number from the backlog item (e.g.
`step-03-walkthrough.md`).
Use the **linear walkthrough** approach: present information as a guided
narrative where each piece builds naturally on what came before. The reader
should never encounter an unexplained concept — every idea is introduced before
it is referenced. Structure the material so it reads top-to-bottom without
requiring the reader to jump ahead or back.

This contrasts with a "reference" style that groups by category (e.g. all types,
then all functions). Instead, introduce concepts in the order a newcomer would
need them to build understanding incrementally.
Present a brief summary to the user and point them to the walkthrough file.

11. Once done, update `status.md` in the work-plan directory, marking what you've
done (see "Marking Completion" below).

12. If there **were** deviations from the plan, **briefly** describe them in
`status.md`. Be factual (what is the deviation) and provide a very short
rationale ("couldn't use X from Y because of circular dependency"). If there
were **no** deviations, do not add anything beyond the completion marker.

13. Ask the user if they are satisfied with the result. If not, ask for feedback
and keep working until the user is satisfied. When follow-up adjustments are
made, update `step-XY-walkthrough.md` to reflect the final state of the changes.

14. Remove the completed item from `backlog.md`.

### Marking Completion

When marking item as completed, write the following line to `status.md`:
`COMPLETED step <X>: <SUMMARY>`

`<X>` is the number of the completed step.

`<SUMMARY>` is a summary of the change, adhering to the following rules:
 * be 50 characters or shorter;
 * start with a capital letter;
 * be understandable without the context of the goal.

Examples:
 * GOOD: "COMPLETED step 7: Extract helpers from Subscription tests"
 * BAD: "COMPLETED step 7: Extract _create_new()" - not understandable without
 context.

Rule of thumb: everything after "step ..." should be usable as a good commit
title.