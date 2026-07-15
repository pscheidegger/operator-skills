---
name: knowledge-extraction-skill
description: Turn transient source material into classified, durable knowledge decisions such as discard, create-reference, create-knowledge, create-task, or update-existing. Use for meetings, chats, research, repositories, articles, transcripts, and normalized documents when the user wants reusable knowledge rather than a plain summary. Do not use for file parsing, unchanged archival, or response formatting alone.
---

# Knowledge Extraction Skill

## Purpose

Transform transient information into durable knowledge.

This skill is the first semantic decision step. Source-specific ingestion may run before it. It runs before `integration-candidate-skill`, quality gating, and final response formatting.

## Use When

- Chat analysis
- Meeting analysis
- Repository analysis
- Article analysis
- Video analysis
- Research consolidation

## Do Not Use When

- A plain summary is requested
- Raw transcripts must be preserved unchanged
- Archival without knowledge extraction is the goal

## Core Rules

1. Extract knowledge, not conversation.
2. Remove smalltalk.
3. Remove intermediate reasoning.
4. Preserve decisions.
5. Preserve architecture assumptions.
6. Preserve workflows.
7. Preserve configuration.
8. Preserve open tasks.
9. Search before creating.
10. Prefer updating existing knowledge.
11. Preserve traceability.
12. Classify every extraction result.

## Quality Filter

Discard information that is unlikely to remain relevant in six months.

## Extraction Mode

Use exactly one mode:

- `knowledge`
- `project`
- `meeting`
- `research`

## Extraction Decision

Use exactly one decision:

- `discard`
- `create-reference`
- `create-knowledge`
- `create-task`
- `create-candidate`
- `update-existing`

```text
extraction_decision: discard
→ no file
→ no integration candidate
```

```text
extraction_decision: update-existing
→ use integration-candidate-skill
```

```text
extraction_decision: create-candidate
→ use integration-candidate-skill
```

## Existing Note Check

If relevant knowledge already exists, prefer `update-existing` and use the `integration-candidate-skill`.

## Output Order

1. Decisions
2. Knowledge
3. Open Tasks
4. Architecture
5. Workflows
6. References

End the extraction with explicit machine-readable handoff fields:

```yaml
extraction_mode: knowledge
extraction_decision: update-existing
target_note: optional-target
sources: []
```

## Shared Metadata

When this skill generates files, prefer setting:

```yaml
generated_by_skill: knowledge-extraction-skill
```
