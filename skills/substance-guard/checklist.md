# SubstanceGuard Checklist

Use this checklist for quick manual reviews before accepting, publishing, saving, or committing AI-generated or drafted content.

## Fast Gate

Choose one:

- **Pass**: The output is concrete, useful, grounded, and low on filler.
- **Revise**: The output is usable but needs targeted improvements.
- **Reject**: The output is polished but too vague, unsupported, redundant, misleading, or falsely complete.

## Substance Checks

- Does the output answer the actual user request?
- Does it contain concrete facts, mechanisms, examples, commands, criteria, or tradeoffs?
- Are important assumptions explicit?
- Are limitations or uncertainties visible where needed?
- Could a reader act on the output without guessing the missing steps?

## Specificity Checks

- Are vague adjectives replaced by observable details?
- Are recommendations tied to decision criteria?
- Are technical terms connected to responsibilities, inputs, outputs, or failure modes?
- Are claims precise enough to verify?

## Grounding Checks

- Are factual claims supported by source material, user-provided context, code, logs, tests, or stated assumptions?
- Are inferred points clearly marked as inference?
- Does the output avoid unsupported certainty?

## Redundancy Checks

- Are repeated bullets merged?
- Are circular explanations removed?
- Are empty introductions and summaries cut?
- Does each section add something new?

## Tone Discipline Checks

Remove or rewrite:

- Hype language
- Corporate filler
- Generic enthusiasm
- Synthetic transitions
- "Not only X but Y" rhetoric
- Overly polished but low-information phrasing

## Code and Documentation Checks

For READMEs, PR descriptions, implementation plans, and generated code explanations:

- Does the documentation describe actual behavior, not aspirational behavior?
- Are inputs, outputs, constraints, and failure modes clear?
- Are test coverage and known gaps stated?
- Are production-readiness claims backed by evidence?
- Are comments useful, or do they merely describe obvious syntax?
- Is there unnecessary abstraction or overengineering?

## secondBrain Extraction Checks

For durable knowledge notes:

- Keep reusable decisions, facts, patterns, links, and constraints.
- Remove temporary chat context.
- Remove obvious statements.
- Remove repetition.
- Separate facts, assumptions, and follow-up tasks.

## Required Output for Gate Mode

Use this structure:

```text
Verdict: Pass | Revise | Reject
Score: 1-5
Main issues:
- ...
Required fixes:
- ...
Optional improved version:
...
```
