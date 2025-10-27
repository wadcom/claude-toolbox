---
description: Gather and document goal requirements
---

You are tasked with creating detailed specification of an initiative goal 
through an interactive, iterative process. You should be thorough and work 
collaboratively with the user to produce high-quality specifications.

## Process Steps

1. Ask the user for high-level description of the goal, and relevant context, 
constraints, or specific requirements.

2. **Read all mentioned files immediately and FULLY**:
   - Research documents
   - Related implementation plans
   - Any data files mentioned
   - **IMPORTANT**: Use the Read tool WITHOUT limit/offset parameters to read 
   entire files
   - **CRITICAL**: DO NOT spawn sub-tasks before reading these files yourself 
   in the main context
   - **NEVER** read files partially - if a file is mentioned, read it 
   completely

3. Compile an initial list of questions to ask the user. Use TodoWrite to track 
them.
  - **IMPORTANT**: each question should be put into a separate TODO item.
  - Check out the "Things To Consider" section below to guide the creation of
  the initial questions list.

4. Iterate while the TODO list is not empty.
  - **IMPORTANT**: ALWAYS ask ONE question at a time
  - Take one item from the TODO list and ask the user this question. Then 
  remove it from the list with TodoWrite tool.
  - Assess user's input and all available information, decide if you need to 
  add more questions to the list. If so, use TodoWrite to update the list.

**CRITICAL**: all questions must be in TODO lists, you must ask ONE question at
a time and tick the corresponding item.

5. Write out the specification to files (see locations and format below), let
the user review it and ask if the user wants to improve this specification. If
the user wants to improve it, repeat from step 1 using all information gathered
by this point as a context.

## Output Location And Format

Produce two files located in the directory `work-plan/YYYY-MM-DD-SUMMARY`:
`goal.md` and `spec.md`.

The directory name should contain the today's date (`YYYY-MM-DD`) and a short 
(less than 30 characters) summary of the goal (`SUMMARY`), formatted as 
lowercase with hyphens, e.g. `improve-mobile-app`.

## Relationship Between Goal and Spec Files

**Goal File (`goal.md`):**
- Contains business requirements and objectives
- Describes WHAT needs to be achieved and WHY
- Written for product stakeholders
- Focuses on user experience, business logic, success criteria
- Avoids technical implementation details

**Spec File (`spec.md`):**
- Contains technical architecture and approach
- Describes HOW to achieve the goals technically
- Written for senior developers
- Focuses on architecture, data models, integration points
- Provides technical direction without prescribing exact implementation steps

**Critical Distinction:** Spec files provide overall technical direction, NOT 
detailed implementation steps. They enable senior developers to review the goal 
+ spec + next backlog item to determine exact technical requirements for 
immediate work.

**Key principle:** Goal + Spec + Backlog Item = enough info for a senior 
developer to implement autonomously.

## Goal File

The goal file `goal.md` should contain business-focused explanation of the 
initiative's goal. It should contain no technical details (unless the goal is
inherently technical).

**Use this template structure for goal.md**:

````markdown
# [Feature/Task Name]

## Purpose

[Brief description of what we're implementing and why]

## Problem Statement

[Brief explanation of the problem]

## Solution

[Brief, high-level description of the solution]

## Use Case Example

[Examples of how the solution solves the problem]

## Scope

[High-level description of all system parts that need work to implement the
solution]

[Things explicitly out of scope]

## Success Criteria

[How success looks, besides what's listed in Use Case Example]

## References

[Any documents, files or links that provide context for the initiative]

````

## Spec File

### Every Spec Must Include:
1. **Overview** - 2-4 sentences linking to goal.md
2. **Current State** - What exists today OR "Greenfield project. No existing 
implementation."
3. **Technical Architecture/Approach** - Architectural decisions, patterns, key 
components
4. **Verification** - Success criteria, test commands, how to confirm it works
5. **Out of Scope** - What won't be done in this phase

### Include When Relevant:
- **Architectural Principles** - Fundamental design decisions for complex 
systems (name, key decisions, benefits)
- **Data Model** - Entities, fields, relationships, state management
- **File Organization** - Module structure, dependencies, public API vs 
internal
- **Integration Points** - How components connect, data flow, triggers
- **Implementation Strategy** - For refactoring: critical first step, phased 
approach
- **Implementation Gaps** - For greenfield: what needs to be built (high-level 
areas)
- **Configuration** - Settings location, key parameters, defaults

### Structure by Project Type

**Greenfield:**
Overview → "Greenfield" → Tech Stack → Architecture → Key Decisions → 
Implementation Gaps → Verification → Out of Scope

**Refactoring:**
Overview → Current State (what exists, issues) → Architecture Pattern → Desired 
End State → Implementation Strategy (critical first step) → Verification → Out 
of Scope

**Enhancement:**
Overview → Architectural Principles → Current State (what exists, what's 
missing) → Technical Architecture → Integration Points → Verification → Out of 
Scope

### Level of Detail

**Right level (✅):**
- "UserSubscription stores billing timestamps with hour-level precision using 
DateTimeField"
- "Main FSM checks shared conditions first, then delegates on :state field"
- "FileSystemLoader for includes, allowing standard Jinja2 syntax"

**Too vague (❌):**
- "The system handles subscriptions"
- "Use best practices for data modeling"

**Too detailed (❌):**
- Complete function implementations
- Exact variable names and loop structures
- Step-by-step procedures

**Target:** Senior developer knows (1) what architectural pattern to follow, 
(2) what key entities/components exist, (3) how they relate, (4) what critical 
decisions have been made. But NOT how to write their code.

## Things To Consider

When gathering requirements, ensure you discuss these aspects with the user:

### Documentation & Communication
- **Changelog**: Does this initiative require entries in CHANGELOG.md or release
notes?
- **External Documentation**: Are there user-facing docs (README, wiki, help
pages) that need updates?
- **Internal Documentation**: Does internal documentation (architecture docs,
runbooks, troubleshooting guides) need updates?
- **API Documentation**: If APIs are affected, do OpenAPI specs, docstrings, or
API reference docs need updates?
- **Migration Guides**: Are there breaking changes requiring migration
instructions for users?
- **Examples & Tutorials**: Do code examples, sample projects, or tutorials
need updates to reflect changes?

## Writing Style

- Technical and precise
- Declarative (state what IS, not what to do)
- Present tense
- Direct, not verbose
- **Bold** for entity/component names
- `inline code` for fields, methods, paths, technical terms
- Code blocks for patterns (not full implementations)

## Quality Check

- [ ] Links to goal.md
- [ ] Current state accurate
- [ ] Architectural decisions clear with rationale
- [ ] Code shows patterns, not implementations
- [ ] Verification specific and testable
- [ ] Out of scope explicit
- [ ] No business requirements (→ goal.md)
- [ ] No step-by-step instructions (→ backlog)
- [ ] Senior dev could implement without constant questions

## Common Pitfalls

1. Mixing business rationale with technical details (business → goal.md)
2. Prescribing exact implementation (give direction, not code)
3. Incomplete current state baseline
4. Vague principles ("be modular" is not useful)
5. Missing integration points
6. No verification criteria
7. Scope creep (future work → Out of Scope)
