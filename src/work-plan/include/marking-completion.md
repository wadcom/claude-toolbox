When marking item as completed, append a new entry to `status.html` in the
form `<p>COMPLETED step <X>: <SUMMARY></p>`.

`<X>` is the number of the completed step.

`<SUMMARY>` is a summary of the change, adhering to the following rules:
 * be 50 characters or shorter;
 * start with a capital letter;
 * be understandable without the context of the goal.

Examples:
 * GOOD: `<p>COMPLETED step 7: Extract helpers from Subscription tests</p>`
 * BAD: `<p>COMPLETED step 7: Extract _create_new()</p>` — not understandable
 without context.

Rule of thumb: everything after "step ..." should be usable as a good commit
title.
