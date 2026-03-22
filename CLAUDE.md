# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a **skill definition** for Claude Code's superpowers system, not a traditional software project. It contains a single `SKILL.md` file that serves as a color expertise knowledge base, automatically loaded when Claude handles color-related tasks (naming, theory, spaces, accessibility, perception).

## Architecture

- `SKILL.md` — The skill definition file with YAML frontmatter (`name`, `description`) and structured color knowledge. This file is registered in the superpowers skill system and invoked via the `Skill` tool when color work is detected.

## No Build/Test/Lint

There are no commands to run. This project is purely declarative content consumed by the Claude Code harness.

## Editing Guidelines

- Keep SKILL.md frontmatter `description` field accurate — it controls when the skill triggers.
- The skill is referenced by name (`color-expert`) in the superpowers skill registry.
- Content should be concise reference material, not exhaustive documentation — Claude already has broad color knowledge; the skill should guide *how* to approach color tasks and highlight non-obvious resources/standards.
