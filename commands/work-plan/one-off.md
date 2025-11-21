---
description: Implement a small change without formal backlog process
---

You are tasked with implementing a small, one-off change to an existing
initiative without going through the formal backlog/spec preparation process.

This command is ideal for quick fixes, minor improvements, or small features
that don't warrant a full planning cycle.

## Process Steps

1. Ask the user to provide a goal file (it should be named `goal.md`). Then
read FULLY files named `spec.md`, `backlog.md` and `status.md` located in the
same directory as the goal. For example, if user has provided a file
`a/b/c/goal.md`, also read files `a/b/c/spec.md`, `a/b/c/backlog.md` and
`a/b/c/status.md`. It will provide you with the necessary context.

2. Ask the user what small change they want to implement.

3. Compile an initial list of questions to ask the user in order to better
understand the change. Use TodoWrite to track them.
  - **IMPORTANT**: each question should be put into a separate TODO item.

4. Iterate while the TODO list is not empty.
  - **IMPORTANT**: ALWAYS ask ONE question at a time
  - Take one item from the TODO list and ask the user this question. Then
  remove it from the list with TodoWrite tool.
  - Assess user's input and all available information, decide if you need to
  add more questions to the list. If so, use TodoWrite to update the list.

5. Write out the implementation plan to a file named `step-XY.md` (`step-01.md`
if there are no other `step-*.md` files yet, or the next sequential number if
there are).

The plan should contain important high level details without being overly
specific. A senior developer should be able to read this step plan and
review/verify overall design, key decisions etc. without being bogged down by
minutia.

The plan should be written so that if a developer reads `goal.md`, `spec.md`
and the plan, they would have complete context to immediately implement the
step.

6. Ask if the user is satisfied with the plan. If not, ask what needs to be
adjusted and iterate on the plan.

7. Implement the plan, following it exactly, step by step. Track your progress
using TodoWrite tool. If the plan specifies a success criteria, make sure that
is met before reporting completion.

8. Once you are done, create or update a file named `status.md` (located in the
same directory as `spec.md`), marking what you've done (see "Marking
Completion" below).

9. If there **were** changes to the original plan, **briefly** describe them in
`status.md` as well. Be factual (what is the deviation from the plan) but
provide a very short rationale ("couldn't use X from Y because of circular
dependency"). If there was **NO** changes, do not document anything about
deviations in the status.

10. Ask the user if they are satisfied with the result. If no, ask for the
feedback and keep working until the user is satisfied.

**IMPORTANT**: Do NOT update `backlog.md`. This is a one-off change that
bypasses the formal backlog process.

## Asking Questions

When asking questions, use the following guidelines:

1. If you can look something up yourself, LOOK IT UP, just ask user for the
final confirmation.

2. Do not ask questions about details that do not matter in the context of the
big picture. Non-consequential questions that can wait until we get to the
implementation, should wait.

3. When asking user to choose between options, provide initial analysis to
highlight pros and cons based on actual code, and give your recommendation. The
final decision should still be made by the user.

## Marking Completion

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