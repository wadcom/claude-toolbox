---
description: Prepare to work on the next item from backlog
---

You are tasked to examine the top item in the current backlog and evaluate 
whether it is sufficiently small and specific to be worked on immediately. 

If the item is ready, you will create a detailed implementation plan for it. If 
the item is not ready, explain why it needs further refinement before work can 
begin.

## Process Steps

1. Ask the user to provide a backlog file (it should be named `backlog.md`). 
Then read FULLY that file, as well as files named `goal.md`, `spec.md` and 
`status.md` located in the same directory. For example, if user has a file 
`a/b/c/backlog.md`, also read files `a/b/c/goal.md`, `a/b/c/spec.md` and 
`a/b/c/status.md`. It will provide you with the necessary context.

2. Evaluate thoroughly the very first item in the backlog. Think hard and 
decide whether it has enough details to be worked on immediately, or needs
refinement. If it does need refinement, provide a summary to the user of which
aspects are unclear and STOP HERE.

It it expected that the item doesn't complete every single little detail about
what needs to be done. You have to reject items as needing refinement only if
they are so ambiguous that it's not possible to clear the ambiquity with a few
simple questions.

3. Evaluate how much effort is required to implement the item. If it would take
a senior engineer more than 30 minutes of focused work to implement it, 
recommend to split the item and STOP HERE.

4. If there are some details that need clarification, work with the user
iteratively (use TodoWrite tool) to get the required clarity.

5. Write out the implementation plan to a file named `step-XY.md` (`step-01.md`
if there are no other `step-*.md` files yet, or the next sequential number if 
there are).

The plan should contain important high level details without being overly 
specific. A senior developer should be able to read this step plan and
review/verify overall design, key decisions etc. withough being bogged down by
minutia.

The plan should be written so that if a developer reads `goal.md`, `spec.md`
and the plan, they would have complete context to immediately implement the
step.

6. Ask if the user if satisfied with the plan. If not, ask what needs to be
adjusted and return to step 4.