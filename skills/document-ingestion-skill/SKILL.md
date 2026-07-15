---
name: document-ingestion-skill
description: Convert PDFs, office documents, HTML, plain text, or parser output into traceable, structured Markdown for downstream processing. Use when source material must be parsed, OCRed, normalized, or have tables and metadata preserved. Do not use when the input is already clean Markdown and no normalization is needed, or when the user only wants semantic knowledge extraction.
---

# Document Ingestion Skill

## Purpose

Transform documents into structured Markdown that can be processed by downstream knowledge workflows.

This skill handles ingestion, parsing and normalization. It does not decide whether content becomes a reference, knowledge note, task, or integration candidate. Use `knowledge-extraction-skill` after ingestion when a durable knowledge decision is needed.

## Use When

- A PDF should be converted into Markdown.
- A DOCX, PPTX, XLSX or HTML document should be prepared for knowledge extraction.
- A document should be imported into a Markdown-first knowledge base.
- Parser output should be normalized before analysis.

## Do Not Use When

- The user only wants to store the original file.
- The source is already clean Markdown and needs no normalization.
- The task is pure knowledge extraction without document parsing.
- The document contains secrets or private data that should not be processed.

## Supported Source Types

- PDF
- DOCX
- PPTX
- XLSX
- HTML
- plain text
- Markdown

## Parser Options

The skill is tool-neutral. Use the parser that best fits the document.

```yaml
parser: docling
parser: marker
parser: mineru
parser: liteparse
parser: pymupdf
```

### Recommended Defaults

Use `docling` as the default parser for mixed office documents and structured PDF conversion.

Use `pymupdf` for lightweight PDF text extraction.

Use `marker` or `mineru` for complex scientific PDFs, scanned documents, formulas, tables or layout-heavy content.

## Output

The primary output is Markdown.

Optional outputs:

- metadata JSON
- extracted images
- tables as CSV
- raw parser output

## Core Rules

1. Preserve document structure when possible.
2. Prefer Markdown output.
3. Preserve headings, lists, tables and source metadata.
4. Do not treat parser output as final knowledge.
5. Do not create durable knowledge directly from raw parser output.
6. Pass normalized Markdown to `knowledge-extraction-skill` when the user wants analysis or durable knowledge.
7. Preserve traceability to the source document.
8. Keep original files separate from extracted knowledge.
9. Do not create duplicate notes for the same source.
10. Use `action-first-skill` only after ingestion and extraction decisions are made.

## Standard Workflow

```text
Document
  ↓
Document Ingestion
  ↓
Structured Markdown
  ↓
knowledge-extraction-skill
  ↓
integration-candidate-skill if needed
  ↓
action-first-skill response
```

## Metadata

Generated Markdown should include source metadata when available.

```yaml
source_file:
source_type:
parser:
generated_by_skill: document-ingestion-skill
```

For multi-skill workflows:

```yaml
generated_by_skill:
  - document-ingestion-skill
  - knowledge-extraction-skill
```

## Ingestion Decisions

Use one of these values when documenting the result:

```yaml
ingestion_decision: discard
ingestion_decision: convert-only
ingestion_decision: pass-to-knowledge-extraction
```

## Decision Rules

```text
ingestion_decision: discard
```

No Markdown note and no downstream extraction should be created.

```text
ingestion_decision: convert-only
```

Create normalized Markdown but do not extract durable knowledge yet.

```text
ingestion_decision: pass-to-knowledge-extraction
```

Run `knowledge-extraction-skill` on the normalized Markdown.

## Quality Checks

Before passing Markdown downstream, check:

- headings are preserved
- text order is coherent
- tables are usable
- images or figures are referenced if important
- obvious OCR errors are noted
- source metadata is present

## Anti-Patterns

Avoid:

- dumping unreadable extracted text into the knowledge base
- storing raw parser output as durable knowledge
- creating a new note for every document without classification
- losing source file references
- silently ignoring failed table or OCR extraction
