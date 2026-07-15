# Document Ingestion Skill

A reusable workflow for converting documents into structured Markdown before knowledge extraction.

## Core Idea

Documents are not knowledge.

Documents must first be normalized into structured Markdown.

After ingestion, `knowledge-extraction-skill` determines whether the content becomes a reference, knowledge note, task, update, or discard result.

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
integration-candidate-skill if an existing target needs review
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
