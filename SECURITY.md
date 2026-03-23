# Security

## Skill Architecture

This skill is **read-only declarative content** — it contains no executable code, no build steps, no dependencies, and no runtime network access. There is nothing to install or run.

When an agent loads this skill, it reads `SKILL.md` and optionally reads static markdown files from `references/`. This is identical to reading any other source file in a project.

## Reference Files

The `references/` directory contains curated markdown summaries of color science literature. These files are:

- **Static** — committed to the repo as plain text, not fetched at runtime
- **Human-curated** — reviewed and edited by the maintainer, not raw scrapes
- **Read-only** — the agent reads them for context; they contain no instructions, no tool calls, and no prompts

Sources include public domain books (archive.org, Project Gutenberg), academic publications, and educational websites. All sources are cited in each file.

## No Executable Permissions

This repo contains no `settings.json`, `settings.local.json`, or any configuration that grants shell, network, or filesystem permissions. The entire `.claude/` directory is gitignored.

## Reported False Positives

- **`colorwell.org`** (flagged as typosquatting) — This is a legitimate color/art education site by painter John Morfis. It appears as a citation in a reference file, not as a download target.
