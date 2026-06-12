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
ingestion_decision: create-reference
```

Workflow:

Documents → Markdown → Reference Note