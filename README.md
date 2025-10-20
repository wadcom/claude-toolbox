# claude-toolbox

## work-plan 

> Plan the work, work the plan.

A set of commands for Claude Code that help you manage software projects by 
planning incrementally, not all upfront. Specify your goal, create a backlog, 
then detail only the next step you'll actually work on. As you implement and 
learn, adjust your plans.

Detailed plans made far in advance rarely survive contact with reality — 
whether you're coding yourself or working with AI. `work-plan` helps you 
maintain just enough structure to move forward while letting plans evolve as 
your understanding grows.

### Philosophy: The Middle Path

This workflow sits between two extremes in AI-assisted development:

**Spec-driven development** creates comprehensive specifications upfront. By 
the time you reach implementation, requirements have shifted and understanding 
has deepened. You end up maintaining two things that drift apart: specs and 
code. This is expensive with human teams and wastes precious context with AI.

**Vibe coding** is pure improvisation with no structure. It feels productive 
initially but projects become chaotic without any roadmap to maintain coherent 
goals and architecture.

`work-plan` takes a different approach: maintain clear business goals and a 
roughly prioritized backlog, but **only detail the very next item** you'll 
implement. After completing it, groom the backlog based on what you learned, 
adjust priorities, then detail the next one. You always know your next couple 
steps clearly, plus a rough sense of direction.

This is the same insight that emerged when software teams moved from 
big-upfront-design approaches to iterative methods—planning incrementally based 
on learning works better than pretending to know everything from day one. That 
principle applies equally well to AI-assisted development.

## Quick workflow overview 
 * `/work-plan:specify` to start a new initiative → `/work-plan:create-backlog`
 to prioritize work.
 * Repeat `/work-plan:prep-next` to plan the next step → `/work-plan:implement`
 to execute it. 
 * `/work-plan:adjust` when requirements/understanding change.
 * `/work-plan:groom-backlog` to keep your backlog manageable.

 I was inspired by [Advanced Context Engineering for Coding Agents](https://github.com/humanlayer/advanced-context-engineering-for-coding-agents/blob/main/ace-fca.md).

## Installation

Clone this repo, then `ln -s $LOCALREPO/commands/work-plan ~/.claude/commands/work-plan`.
