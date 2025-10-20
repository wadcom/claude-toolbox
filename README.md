# claude-toolbox

## work-plan 

> Plan the work, work the plan.

A set of commands for Claude Code that help you manage software projects by 
planning incrementally, not all upfront. Specify your goal, create a backlog, 
then detail only the next step you'll actually work on. As you implement and 
learn, adjust your plans.

This approach works because detailed plans made far in advance don't survive 
contact with reality — whether you're coding yourself or working with AI. 
Instead of pretending you know everything from day one, `work-plan` helps you 
maintain just enough structure to move forward confidently while letting plans 
evolve as your understanding grows.

Quick workflow overview: 
 * `/work-plan:specify` to start a new initiative → `/work-plan:create-backlog`
 to prioritize work.
 * Repeat `/work-plan:prep-next` to plan the next step → `/work-plan:implement`
 to execute it. 
 * `/work-plan:adjust` when requirements/understanding change.
 * `/work-plan:groom-backlog` to keep your backlog manageable.

 I was inspired by [Advanced Context Engineering for Coding Agents](https://github.com/humanlayer/advanced-context-engineering-for-coding-agents/blob/main/ace-fca.md).

## Installation

Clone this repo, then `ln -s $LOCALREPO/commands/work-plan ~/.claude/commands/work-plan`.
