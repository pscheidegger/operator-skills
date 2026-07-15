# SubstanceGuard Roadmap

This roadmap defines how SubstanceGuard should be improved after the initial skill file is created. It is intended for continued work with Codex, axet.plugin, Copilot, and other coding or operator agents.

## Current Status

Initial skill created with:

- Core purpose
- Review criteria
- Slop pattern list
- Output modes
- Scoring model
- Checklist
- Initial examples

The first version is intentionally practical rather than exhaustive. The next work should focus on real-world calibration.

## Guiding Principle

Improve SubstanceGuard from real failures, not theoretical preferences.

Every new rule should ideally come from one of these sources:

- A real AI output that looked polished but lacked substance
- A generated document that overstated evidence
- A PR or README that sounded complete but missed risk, tests, or constraints
- A secondBrain note that preserved too much temporary context
- A research summary that mixed facts, assumptions, and interpretation

## Improvement Loop

Use this loop for every meaningful update:

```text
Use -> Observe -> Label -> Refine -> Example -> Commit
```

Detailed steps:

1. Use SubstanceGuard on a real output.
2. Save the original and improved version when safe to do so.
3. Label the slop pattern.
4. Add or refine one rule.
5. Add one example or regression case.
6. Update `CHANGELOG.md`.
7. Commit the change with a specific message.

## Recommended Repository Structure

Target structure:

```text
skills/
  substance-guard/
    SKILL.md
    checklist.md
    examples.md
    ROADMAP.md
    CHANGELOG.md
    golden/
      001-readme-review.md
      002-pr-description-gate.md
      003-secondbrain-extract.md
      004-research-summary-review.md
      005-code-docs-review.md
```

## Phase Plan

### v0.1: Initial Text and Documentation Review

Goal:
- Make SubstanceGuard useful for reviewing and rewriting generic AI output.

Included:
- Review Mode
- Rewrite Mode
- Gate Mode
- Basic scoring
- Generic slop pattern detection

Done when:
- `SKILL.md`, `checklist.md`, and `examples.md` exist.
- At least five examples are documented.

### v0.2: Gate Mode Hardening

Goal:
- Make Pass / Revise / Reject decisions stricter and more consistent.

Tasks:
- Add clearer pass criteria.
- Add stricter reject criteria.
- Add examples where a fluent output must still be rejected.
- Add examples where a long output should pass because the detail is necessary.
- Add risk-of-overcorrection guidance.

Acceptance criteria:
- Gate Mode does not reward polish without substance.
- Gate Mode does not over-compress useful technical detail.

### v0.3: secondBrain Extract Mode

Goal:
- Make SubstanceGuard useful before saving notes into secondBrain.

Tasks:
- Define durable-knowledge extraction rules.
- Add examples for chat-to-note conversion.
- Add rules for separating facts, assumptions, decisions, and follow-ups.
- Add guidance for preserving links and source context.

Acceptance criteria:
- Extract Mode removes temporary conversation filler.
- Extract Mode preserves reusable knowledge, decisions, constraints, and references.

### v0.4: GitHub and PR Workflow Mode

Goal:
- Apply SubstanceGuard to repository work.

Tasks:
- Add PR description checklist.
- Add issue-quality checklist.
- Add README review checklist.
- Add generated-code-documentation checks.
- Add examples for PRs that are too vague, too confident, or missing test/risk details.

Acceptance criteria:
- A PR description should explain what changed, why, test coverage, risk, and review focus.
- README changes should describe actual behavior, not aspirational behavior.

### v0.5: Code and Implementation Slop

Goal:
- Detect fake completeness, overengineering, and documentation drift in code-related outputs.

Tasks:
- Add checks for unused abstractions.
- Add checks for comments that describe obvious syntax.
- Add checks for tests that do not assert meaningful behavior.
- Add checks for implementation plans that skip failure modes.

Acceptance criteria:
- Code Mode can flag code or implementation plans that look complete but are not operationally reliable.

### v0.6: Research and Evidence Mode

Goal:
- Improve summaries that depend on evidence, sources, or up-to-date information.

Tasks:
- Add rules for separating fact, inference, assumption, and speculation.
- Add source-quality checks.
- Add rules for avoiding unsupported trend claims.
- Add examples for weak market, product, and technical research summaries.

Acceptance criteria:
- Research summaries clearly identify source material, scope, date relevance, and uncertainty.

### v1.0: Stable Skill

Goal:
- Make SubstanceGuard stable enough for regular operator use.

Tasks:
- Review all examples.
- Remove duplicate rules.
- Add a concise quick-start section.
- Add golden examples.
- Add a changelog.
- Document known limitations.

Acceptance criteria:
- The skill can be used consistently by ChatGPT, Codex, Copilot, or another operator agent.
- The skill has examples for text, docs, PRs, secondBrain notes, code documentation, and research summaries.

## Continuous Improvement Mechanisms

### 1. Learning Log

Create `learning-log.md` if the skill starts producing repeated improvement insights.

Suggested entry format:

```text
## YYYY-MM-DD - Short title

Input type:
- README | PR | secondBrain note | research summary | implementation plan | other

Observed slop pattern:
- ...

Why the current skill missed or underweighted it:
- ...

Rule change:
- ...

Example added:
- ...
```

### 2. Golden Examples

Create the `golden/` directory once there are enough examples.

Golden examples should include:

- Input
- Expected diagnosis
- Expected output shape
- Known acceptable variations
- Anti-patterns to avoid

### 3. Regression Cases

Whenever a new rule is added, add an example that would fail without that rule.

Example:

```text
Rule: Flag fake completeness.
Problem: "Production-ready" was claimed without tests, rollback plan, or edge-case coverage.
Regression example: Add before/after case to `examples.md` or `golden/`.
```

### 4. PR Template for Skill Changes

Consider adding a pull request template for skill improvements:

```text
## What changed?

## Why?

## Which slop pattern does this address?

## Example before/after

## Risk of overcorrection

## Checklist
- [ ] Rule is concrete
- [ ] Example added
- [ ] Changelog updated
- [ ] Does not make output artificially casual
- [ ] Preserves useful nuance
- [ ] Does not remove necessary technical detail
```

### 5. Versioning

Suggested version progression:

```text
v0.1 = initial text/document review
v0.2 = hardened Gate Mode
v0.3 = secondBrain Extract Mode
v0.4 = GitHub/PR workflow mode
v0.5 = code and implementation slop checks
v0.6 = research and evidence mode
v1.0 = stable operator skill
```

## Suggested Next Tasks for Codex or Copilot

1. Create `CHANGELOG.md` with initial v0.1 entry.
2. Add `golden/001-pr-description-gate.md`.
3. Add `golden/002-secondbrain-extract.md`.
4. Add explicit pass/revise/reject examples to `examples.md`.
5. Add a PR template under `.github/pull_request_template.md` if this repo does not already have one.
6. Review existing skills in the repository and align formatting conventions.
7. Add a root README section linking to `skills/substance-guard/SKILL.md` if appropriate.

## Known Risks

### Over-compression

SubstanceGuard may become too aggressive and remove necessary context. Mitigation: preserve nuance and technical detail when they improve correctness.

### Artificial casualness

Making text sound less like AI can accidentally make it sound unprofessional. Mitigation: optimize for substance, not casual tone.

### Source blindness

The skill cannot verify facts unless source material or browsing/tooling is available. Mitigation: flag unsupported claims rather than pretending to verify them.

### Style-only usage

Users may apply the skill only to remove AI-sounding words. Mitigation: keep the core principle focused on signal, grounding, and actionability.
