# Multi Format Ingestion Example

Sources:

- PDF
- DOCX
- PPTX
- XLSX

Parser:

```yaml
parser: docling
```

Output:

- Markdown
- Metadata

Decision:

```yaml
ingestion_decision: pass-to-knowledge-extraction
```

Workflow:

Documents → Markdown → Knowledge Extraction → Reference Decision
