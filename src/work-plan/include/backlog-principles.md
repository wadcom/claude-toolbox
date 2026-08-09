Backlog is a PRIORITIZED list of things to be done. Higher priority items are
at the top.

Backlog is a FLAT list, there is no nesting structure. Each item stands on its
own.

Backlog items are like rocks. When you break a rock, you get several rocks. So
are backlog items: they can be split into smaller items or grouped back into
larger ones.

Each backlog item should be a **vertical slice**: it delivers a small piece of
end-to-end functionality that can be checked or tested manually once
implemented. Prefer slicing that produces something observable (a new UI
element, an API response, a CLI output) over slicing by technical layer (e.g.
"add database schema", then "add service layer", then "add UI"). When vertical
slicing is not practical (e.g. pure infrastructure or foundational plumbing),
note explicitly why, and define what "done" looks like for that item.

A backlog item is a title. The default is NO description at all. Add one only
when the title alone would not recall what the item is about, and then keep it
to 3 sentences at most.

A description states WHAT to do. It never states why the item matters, how the
code works today, or which files to touch. That belongs in `goal`, `spec`, or
the step plan.

The highest priority items (the ones we will work on next), should be the
smallest (e.g. no more than 20 minutes of focused work of a senior engineer)
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
described well enough by its title, so it carries no description.

Before you write the backlog out, reread every description you wrote and
delete the ones the title already covers. Most of them.

