# Skill Composition

## Purpose

Define how the skills in this repository work together.

## Skill Pipeline

Select only the stages needed for the task and use this order:

1. Source ingestion, using at most one primary ingestion skill:
   - `document-ingestion-skill` for files and parser output
   - `social-media-ingestion-skill` for social-media and podcast sources
2. `knowledge-extraction-skill` when durable knowledge must be classified
3. `integration-candidate-skill` when an existing target requires a reviewable proposal
4. `substance-guard` when drafted content needs a quality gate
5. `action-first-skill` when the user-facing response is operational

Reason:

1. First obtain a usable, traceable source representation when needed.
2. Then decide what durable knowledge exists.
3. Then decide whether an update needs a reviewable candidate.
4. Then check the drafted content for substance and grounding.
5. Finally format operational responses for action.

Do not run every skill by default. A clean Markdown note does not need ingestion, a new note does not need an integration candidate, and an explanatory answer may not need Action First.

## Shared Metadata

Generated artifacts should name the skill that produced them:

```yaml
generated_by_skill: document-ingestion-skill
```

For multi-skill workflows, include only skills that materially produced or transformed the artifact:

```yaml
generated_by_skill:
  - document-ingestion-skill
  - knowledge-extraction-skill
  - integration-candidate-skill
```

## Required Decision Flow

```text
Input
  ↓
Source Ingestion if needed
  ↓
Knowledge Extraction
  ↓
Extraction Decision
  ↓
Integration Candidate if needed
  ↓
SubstanceGuard if needed
  ↓
Action-First Response if operational
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

## Decision Ownership

| Decision | Owning skill |
|---|---|
| Parse, OCR, transcribe, or normalize a source | Ingestion skill |
| Discard or create reference, knowledge, task, or update | `knowledge-extraction-skill` |
| Create and shape a reviewable update proposal | `integration-candidate-skill` |
| Pass, revise, or reject drafted content for quality | `substance-guard` |
| Present status, procedure, and next action | `action-first-skill` |
