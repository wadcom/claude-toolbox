---
description: Create backlog for initiative
---

You are tasked with creating backlog for an existing initiative. Work
iteratively with the user to define and prioritize backlog items.

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


## Process Steps

1. Ask the user to provide a goal file (it should be named `goal.md`). Then 
read FULLY that file, and also files named `spec.md` and `status.md` located in 
the same directory.

For example, if user has provided a plan in file `a/b/c/goal.md`, also read 
files `a/b/c/spec.md` and `a/b/c/status.md`. It will provide you with the 
necessary context.

2. Think hard to understand the difference between the current state and the
desired state, as described by the goal file.

3. Formulate the discovered differences as backlog items (following the
guidance in "Principles" section above).

4. Work iteratively with user to define the rough priorities. We don't need to
get bogged in details: it's important to understand what the first 3 priorities
are.

5. Write out the backlog according to priorities. Make sure that the top
priority items are well understood and scoped (confirm this with the user).

6. Repeat from item 4 until the user is satisfied with the backlog.

7. Make sure again that the backlog follows the described principles.

8. Write out the backlog to file named `backlog.md` in the same directory where
`goal.md` is located.