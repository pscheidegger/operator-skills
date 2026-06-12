# Document Ingestion Skill

A reusable workflow for converting documents into structured Markdown before knowledge extraction.

## Core Idea

Documents are not knowledge.

Documents must first be normalized into structured Markdown.

After ingestion, downstream skills determine whether the content becomes a reference, knowledge, task or integration candidate.

## Workflow

```text
Document
  ↓
Document Ingestion
  ↓
Markdown
  ↓
knowledge-extraction-skill
  ↓
integration-candidate-skill
  ↓
action-first-skill
```

## Supported Sources

- PDF
- DOCX
- PPTX
- XLSX
- HTML
- text
- Markdown

## Parser Examples

- Docling
- Marker
- MinerU
- LiteParse
- PyMuPDF

See `SKILL.md` for the complete specification.