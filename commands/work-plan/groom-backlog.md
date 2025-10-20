---
description: Groom initiative's backlog
---

You are tasked with grooming backlog for an existing initiative.

## Process Steps

1. Ask the user to provide a backlog file (it should be named `backlog.md`). 
Then read FULLY that file, and also files named `goal.md`, `spec.md` and 
`status.md` located in the same directory.

For example, if user has provided a plan in file `a/b/c/backlog.md`, also read 
files `a/b/c/goal.md`, `a/b/c/spec.md` and `a/b/c/status.md`. It will provide 
you with the necessary context.

2. Go through each item of the backlog one by one. Make sure you understand
what each item is about. Track your progress using TodoWrite tool. Note which
items seem obsolete. Note which items seem to be too small (requiring less 
than 15 minutes worth of senior engineer's work).

3. Provide your recommendations to the user to: a) drop obsolete items; b) 
group small items into larger ones; c) change the order. Explain your reasons
for each recommendation. Ask user ONE QUESTION AT A TIME. When presenting
results, always refer to backlog items by titles ("Create documentation")
rather than their positions ("items 4 and 5").

4. Process user's feedback. Present the resulting backlog to the user and ask
if they are satisfied. If no, go back to item 2 and repeat. 

5. Write out the updated backlog. Make sure that you follow the backlog
principles outlined below. Specifically, make sure that there are no redundant
details.

## Backlog Principles

Backlog is a PRIORITIZED list of things to be done. Higher priority items are
at the top.

Backlog is a FLAT list, there is no nesting structure. Each item stands on its
own.

Backlog items are like rocks. When you break a rock, you get several rocks. So
are backlog items: they can be split into smaller items or grouped back into
larger ones.

Each backlog item can have a SHORT description (no more than 3 sentences).

The highest priority items (the ones we will work on next), should be the
smallest (e.g. no more than 30 minutes of focused work of a senior engineer)
and have more details.

Backlog must be comprehensible (no more than 15 items). To achieve this, 
lower-priority items may be grouped into more coarse ones. Alternatively, the
scope of the entire initiative may be reduced (with the approval of the user).

The most important is the order of the first few items. The further we go down
the list, the less important it is to precisely prioritize items against each
other.

### Backlog example

````markdown
# [Initiative Name] Backlog

## Highest priority item

## Next priority item

[May have up to 3 sentences of description]

## Another item

## Low priority item which might need context

[May have up to 3 sentences of description]

...
````

**IMPORTANT**: if the item title is enough to recall what it is about, it 
SHOULD NOT have any description! In the example above, "Another item" is 
supposedly described well enough by its title, so it doesn't have any
description.
