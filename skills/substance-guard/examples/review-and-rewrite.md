# Review and Rewrite Examples

## Unsupported Technical Claim

### Input

```text
The integration is production-ready and handles all edge cases.
```

### Review

```text
Verdict: Revise
Score: 2/5
Main issues:
- Production readiness is unsupported.
- Handled failure modes and test evidence are missing.
Required fixes:
- State the tested paths, known gaps, and remaining validation.
```

## Knowledge Extraction Quality Gate

### Input

```text
We had a great discussion and thought it could maybe be useful to create a review process someday.
```

### Improved Draft

```text
Decision: Use a reviewable integration-candidate workflow for proposed updates to existing durable notes.
```

SubstanceGuard improves the draft but preserves the upstream extraction decision and storage target.
