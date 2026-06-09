# AGENTS.md

## Purpose

This repository contains reusable AI agent skills.

Keep skills small, clear, tool-neutral, and easy to copy into other projects.

## Core Rules

1. Write for humans first.
2. Keep each skill focused on one behavior.
3. Prefer portable Markdown over tool-specific formats.
4. Include examples for every skill.
5. Avoid hidden assumptions and vague instructions.

## Skill Structure

Each skill should use this structure:

```text
skills/<skill-name>/
├── README.md
├── SKILL.md
└── examples/
```

## Naming

Use lowercase folder names with hyphens.

Good:

```text
action-first-skill
repo-evaluation-skill
knowledge-extraction-skill
```

Avoid generic names such as:

```text
skill
prompt
helper
misc
```

## Skill Design

A skill should define:

1. Purpose
2. When to use it
3. When not to use it
4. Rules
5. Output pattern
6. Examples

## Repository Scope

This repository should contain reusable skills, templates, examples, and documentation.

Do not store project-specific private notes, credentials, API keys, or customer data.

## Communication Style

Prefer direct, actionable language.

For operational tasks, use action-first communication:

1. State the next action.
2. Give numbered steps.
3. State current status when relevant.
4. Suppress unrelated tangents.
5. End with one concrete next step.
