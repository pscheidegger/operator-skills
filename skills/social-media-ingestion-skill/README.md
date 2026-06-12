# Social Media Ingestion Skill

A reusable skill for converting social media content into durable knowledge.

## Core Idea

Do not store videos as knowledge.

Convert:

```text
Video
  ↓
Transcript
  ↓
Knowledge Extraction
  ↓
Integration Candidate
  ↓
Knowledge Base
```

## Primary Tooling

- yt-dlp
- Whisper or equivalent speech-to-text
- Markdown
- knowledge-extraction-skill

## Optional Analysis Layer

NotebookLM may be used for reports, mind maps and visualization, but is not required.

## Supported Sources

- YouTube
- Instagram

See `SKILL.md` for the complete specification.
