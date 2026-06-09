# Knowledge Extraction Skill

## Purpose

Transform transient information into durable knowledge.

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

knowledge
project
meeting
research

## Extraction Decision

discard
create-reference
create-knowledge
create-task
create-candidate
update-existing

## Existing Note Check

If relevant knowledge already exists, prefer update-existing and use the Integration Candidate Skill.

## Output Order

1. Decisions
2. Knowledge
3. Open Tasks
4. Architecture
5. Workflows
6. References
