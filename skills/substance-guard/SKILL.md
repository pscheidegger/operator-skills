# SubstanceGuard

**Tagline:** Less slop. More substance.

## Purpose

SubstanceGuard is a quality-control skill for reducing AI slop and improving the usefulness of generated or drafted content. It removes filler, generic phrasing, unsupported claims, redundancy, synthetic-sounding prose, and fake completeness. It improves output by increasing specificity, clarity, evidence-awareness, and practical value.

SubstanceGuard does not merely make text sound more human. It makes the work more useful, easier to verify, and easier to act on.

## When to Use

Use SubstanceGuard when reviewing, rewriting, or approving:

- AI-generated answers
- documentation
- README files
- GitHub issues and pull requests
- technical explanations
- implementation plans
- research summaries
- meeting notes
- strategy documents
- product concepts
- secondBrain notes
- emails, messages, and long-form prose

Use it especially before accepting AI-generated content as final, saving it into a knowledge base, publishing it, committing it, or sending it to another person.

## Core Principle

Optimize for signal, not polish.

A good output is not one that merely sounds fluent. A good output helps the user understand, decide, build, verify, or act.

## Review Criteria

Evaluate the content against these criteria:

1. **Substance**
   - Does the content contain useful information, concrete reasoning, examples, constraints, tradeoffs, or decision criteria?

2. **Specificity**
   - Are claims precise enough to be verified or acted on?

3. **Grounding**
   - Are facts, assumptions, sources, evidence, implementation details, or limitations made clear?

4. **Actionability**
   - Does the content help the user do something, decide something, or understand something more clearly?

5. **Redundancy control**
   - Are repeated points merged or removed?

6. **Tone discipline**
   - Is the language free from hype, generic enthusiasm, corporate filler, and synthetic-sounding transitions?

7. **Completeness**
   - Does the output actually solve the user's request, or does it only appear complete?

## Common Slop Patterns

Flag and remove:

- Generic introductions
- Empty summary paragraphs
- Repeated bullet points
- Unnecessary disclaimers
- Unsupported certainty
- Abstract recommendations without examples
- Inflated adjectives
- Marketing language
- "Not only X but Y" rhetoric
- Fake nuance
- Over-structured answers with little content
- Polished wording that hides missing reasoning
- Lists where several bullets say the same thing
- Code comments that describe obvious syntax
- Documentation that promises behavior not present in the implementation

## Required Behavior

When applying SubstanceGuard:

1. Preserve all useful information.
2. Remove or compress low-value text.
3. Replace vague language with concrete wording.
4. Mark unsupported claims instead of pretending they are verified.
5. Keep necessary caveats, constraints, and tradeoffs.
6. Prefer concise, direct, operational language.
7. Avoid making the output artificially casual.
8. Do not remove technical precision to make text friendlier.
9. Do not over-summarize if detail is required for correctness.
10. Return a result that is easier to trust and easier to use.

## Output Modes

### Review Mode

Use when the user wants critique before editing.

Return:

- Overall verdict
- Substance score from 1 to 5
- Main slop patterns found
- Unsupported or vague claims
- Redundant sections
- Required fixes

### Rewrite Mode

Use when the user wants improved text.

Return:

- Rewritten version
- Optional short note listing major changes

### Gate Mode

Use before publishing, committing, sending, or saving content.

Return one of:

- **Pass**: acceptable with no material changes
- **Revise**: usable, but needs targeted fixes
- **Reject**: too vague, unsupported, redundant, misleading, or falsely complete

Include required fixes for Revise or Reject.

### Extract Mode

Use for knowledge-base or secondBrain workflows.

Return only durable, reusable knowledge. Remove:

- Generic context
- Temporary phrasing
- Obvious statements
- Repetition
- Unsupported speculation
- Stylistic filler

### Code and Documentation Mode

Use when reviewing implementation notes, generated code explanations, READMEs, comments, or PR descriptions.

Flag:

- Fake completeness
- Over-engineered abstractions
- Comments that describe obvious syntax
- Documentation that promises behavior not implemented
- Missing inputs, outputs, constraints, failure modes, test coverage, or rollback notes
- Claims such as "production-ready" without evidence

## Scoring

Use this scale:

- **5**: High signal, concrete, grounded, useful
- **4**: Mostly strong, minor fluff or missing specificity
- **3**: Partially useful but too generic or padded
- **2**: Polished but shallow
- **1**: Mostly slop, little usable substance

Optional dimension scores:

- Substance: 1-5
- Specificity: 1-5
- Grounding: 1-5
- Actionability: 1-5
- Redundancy control: 1-5
- Tone discipline: 1-5

## Default Output Format

When no mode is specified, use Review Mode first.

Return:

1. Verdict
2. Score
3. Main issues
4. Required improvements
5. Improved version, only if the fix is straightforward

## Style Target

The final output should be:

- Direct
- Specific
- Evidence-aware
- Concise where possible
- Detailed where necessary
- Free of filler
- Free of unsupported certainty
- Useful for the user's actual task

## Operating Heuristics

Use these heuristics during review:

- A claim is weak if it contains adjectives but no mechanism.
- A recommendation is weak if it has no decision criterion.
- A summary is weak if every bullet could apply to almost any project.
- A technical explanation is weak if it names components but not their responsibilities, inputs, outputs, constraints, or failure modes.
- A PR description is weak if it says what changed but not why, risk, test coverage, or rollback path.
- A knowledge-base note is weak if it preserves temporary conversation filler instead of durable insight.

## Development Loop

Improve this skill through real usage:

1. Use SubstanceGuard on real output.
2. Save the original and improved version.
3. Label the slop pattern.
4. Add or refine one rule.
5. Add one regression example.
6. Update the changelog.
7. Commit the change.

Short form: **Use -> Observe -> Label -> Refine -> Example -> Commit**.
