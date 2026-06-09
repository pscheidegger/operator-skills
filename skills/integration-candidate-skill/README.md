# Integration Candidate Skill

A governance skill for safe, reviewable knowledge updates.

## Core Idea

Do not modify durable knowledge directly.

Create a reviewable integration candidate.

## Problem

Most AI agents either:

1. create duplicate notes
2. modify existing notes directly

Both approaches increase the risk of knowledge drift.

## Solution

```text
Existing Note
      ↓
New Information
      ↓
Integration Candidate
      ↓
Review
      ↓
Merge
```

## Typical Use Cases

- Knowledge bases
- Obsidian vaults
- Second Brain repositories
- Architecture documentation
- Task backlogs
- Governance documents

## Key Features

- Traceable updates
- Review workflow
- Explicit merge strategies
- Target note linking
- Human and agent friendly

See `SKILL.md` for the complete specification.