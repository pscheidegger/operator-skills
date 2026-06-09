# Skill Composition

## Purpose

Define how the skills in this repository work together.

## Skill Priority

When multiple skills apply, use this order:

1. `knowledge-extraction-skill`
2. `integration-candidate-skill`
3. `action-first-skill`

Reason:

1. First decide what knowledge exists.
2. Then decide how knowledge should be stored or proposed.
3. Then format the response for action.

## Shared Metadata

Generated artifacts should include this field when useful:

```yaml
generated_by_skill: knowledge-extraction-skill
```

For multi-skill workflows, use a list:

```yaml
generated_by_skill:
  - knowledge-extraction-skill
  - integration-candidate-skill
```

## Required Decision Flow

```text
Input
  ↓
Knowledge Extraction
  ↓
Extraction Decision
  ↓
Integration Candidate if needed
  ↓
Action-First Response
```

## Decision Rules

```text
extraction_decision: discard
```

No file and no integration candidate should be created.

```text
extraction_decision: update-existing
```

Create an integration candidate unless direct modification is explicitly allowed.

```text
extraction_decision: create-candidate
```

Create an integration candidate.

## Response Formatting

Use `action-first-skill` for user-visible status and next actions after the knowledge and governance decisions are made.
