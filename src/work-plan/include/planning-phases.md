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
