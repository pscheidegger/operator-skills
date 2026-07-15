---
name: integration-candidate-skill
description: Create a focused, traceable proposal for updating an existing durable note, backlog, architecture document, or governance file when review is required. Use after an update-existing or create-candidate decision, or when repository rules require proposed changes instead of direct edits. Do not use for new standalone notes or when the user or repository explicitly authorizes a direct edit.
---

# Integration Candidate Skill

## Purpose

Protect durable knowledge by turning proposed updates into reviewable integration candidates instead of modifying existing notes directly.

This skill is a governance workflow for knowledge bases, documentation repositories, task backlogs, architecture notes, and agent-managed Markdown systems.

It is typically used after `knowledge-extraction-skill` and before `action-first-skill`.

## Use When

- A target note already exists.
- New information should be merged into that note later.
- A task should be proposed for an existing backlog.
- Governance files such as `README.md` or `AGENTS.md` should be changed.
- A human or another agent should review the change before merge.

## Do Not Use When

- Creating a completely new durable note.
- The user explicitly asked to directly modify the target file.
- The update is trivial and direct edits are allowed by the repository rules.

## Core Rules

1. Search before creating.
2. Do not modify durable target notes directly unless explicitly allowed.
3. Create an integration candidate instead.
4. Link the target note in frontmatter and body.
5. Store the target path in frontmatter and body.
6. Explain why the update is proposed.
7. Preserve sources and traceability.
8. Require review before merge unless direct modification is explicitly allowed.
9. Choose the most precise merge strategy.
10. Keep the candidate focused on the proposed change.

## Naming Pattern

```text
<target>_YYYY-MM-DD-HHmm.md
```

Examples:

```text
local-llms_2026-06-09-1430.md
backlog_2026-06-09-1440.md
AGENTS_2026-06-09-1450.md
```

Use the target repository's naming convention when one exists. Use the underscore pattern above only as the portable fallback.

## Required Frontmatter

```yaml
---
type: integration-candidate
status: proposed
candidate_type: knowledge-update
generated_by_skill:
  - integration-candidate-skill

target_note: [[target]]
target_path: path/to/target.md

merge_strategy: review-required
source_notes: []

created: YYYY-MM-DD
updated: YYYY-MM-DD

tags:
  - candidate
---
```

## Candidate Types

Use one of these values:

```yaml
candidate_type: knowledge-update
candidate_type: task-proposal
candidate_type: governance-update
candidate_type: architecture-update
candidate_type: reference-update
```

## Status Values

Use one of these values:

```yaml
status: proposed
status: reviewed
status: approved
status: merged
status: rejected
```

## Merge Strategies

Use the most precise strategy available.

### append

Append the proposed content to the end of the target note.

```yaml
merge_strategy: append
```

### prepend

Insert the proposed content near the beginning of the target note.

```yaml
merge_strategy: prepend
```

### replace-section

Replace a specific section in the target note.

```yaml
merge_strategy: replace-section
target_section: "## Existing Section"
```

### insert-at-anchor

Insert the proposed content before or after a specific anchor.

```yaml
merge_strategy: insert-at-anchor
target_anchor: "## Architecture"
insert_position: after
```

Allowed `insert_position` values:

```yaml
insert_position: before
insert_position: after
insert_position: end-of-section
```

### review-required

Require manual review before deciding how to merge.

```yaml
merge_strategy: review-required
```

## Required Body Sections

```markdown
# Integration Candidate

## Target

- Target note: [[target]]
- Target path: `path/to/target.md`

## Reason

## Sources

## Proposed Addition
```

## Optional Body Sections

```markdown
## Merge Guidance

## Review Notes
```

## Direct Modification Escape Hatch

Modify the target file directly when the user explicitly requests it or repository rules clearly authorize it. Otherwise create an integration candidate.

```yaml
allow_direct_modification: true
```

The optional field is useful for automated handoffs. An explicit user instruction or repository rule takes precedence over a missing field.

When used together with `knowledge-extraction-skill`:

- Do not create a candidate when `extraction_decision: discard`.
- Prefer a candidate for `extraction_decision: update-existing` unless `allow_direct_modification: true` is explicitly set.
- Candidates must include `integration-candidate-skill` in `generated_by_skill`. Include upstream skills in the list when they materially contributed:

```yaml
generated_by_skill: integration-candidate-skill
```

```yaml
generated_by_skill:
  - knowledge-extraction-skill
  - integration-candidate-skill
```
