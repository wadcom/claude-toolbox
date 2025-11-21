# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This repository is a collection of Claude Code slash commands. Currently includes work-plan commands for incremental project planning, but may expand to include other command sets.

## Template System Architecture

Commands are defined using a Jinja2 template system:

- **Source templates**: `src/{command-set}/*.md.j2`
- **Generated commands**: `commands/{command-set}/*.md`
- **Shared content**: `src/{command-set}/include/` directory for reusable fragments

Templates use `{% include 'include/filename.md' %}` syntax to embed shared content. This allows consistent content across multiple commands without duplication.

## Development Workflow

**Manual Generation Process**: There is no automated build system. When modifying commands:

1. Edit the Jinja2 template in `src/{command-set}/*.md.j2`
2. Regenerate the corresponding markdown file in `commands/{command-set}/*.md`
3. Commit both the source template and generated file together

Both `.j2` and `.md` files are committed to the repository.

## Installation

Slash commands are installed by symlinking command directories to `~/.claude/commands/`:

```bash
ln -s $PWD/commands/work-plan ~/.claude/commands/work-plan
```

This makes commands like `/work-plan:specify`, `/work-plan:implement`, etc. available in Claude Code.

## Directory Structure

```
claude-toolbox/
├── src/                    # Source templates
│   └── {command-set}/
│       ├── *.md.j2        # Jinja2 templates
│       └── include/       # Shared content fragments
└── commands/              # Generated commands (symlink targets)
    └── {command-set}/
        └── *.md          # Final slash command definitions
```

## Version Control

This repository uses both Git and Jujutsu (jj) version control systems. The `.jj/` directory contains Jujutsu metadata and is gitignored. Development primarily happens via jj and is synced to git.
