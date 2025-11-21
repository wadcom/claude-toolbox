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
