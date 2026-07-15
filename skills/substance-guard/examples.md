# SubstanceGuard Examples

This file contains before/after and review examples for evolving SubstanceGuard. Add real examples from actual usage over time.

## Example 1: Generic AI Answer

### Before

```text
In today's fast-paced digital world, it is more important than ever to have a robust and scalable system that can help teams unlock productivity and streamline their workflows. This solution provides a seamless way to improve collaboration and ensure better outcomes.
```

### SubstanceGuard Review

Verdict: Reject  
Score: 1/5

Main issues:

- Generic opening
- No concrete system, user, workflow, or outcome
- Inflated adjectives without evidence
- No mechanism or actionability

### After

```text
The system should reduce manual coordination by making task ownership, current status, and blockers visible in one place. The first useful version needs three fields per task: owner, next action, and due date. Add automation only after the manual workflow is stable.
```

## Example 2: Fake Completeness in Technical Documentation

### Before

```text
The integration is production-ready and handles all edge cases. It provides a robust authentication layer and ensures seamless error handling across all scenarios.
```

### SubstanceGuard Review

Verdict: Revise  
Score: 2/5

Main issues:

- "Production-ready" is unsupported
- "All edge cases" is not credible without tests or a list of handled cases
- Authentication and error handling are named but not described
- No constraints, failure modes, or test evidence

### After

```text
The integration supports the tested happy path for authenticated requests. It validates the access token before calling the upstream API and returns an explicit error when the token is missing. Retry behavior, expired-token handling, rate limits, and upstream timeout behavior still need validation before this should be treated as production-ready.
```

## Example 3: PR Description Gate

### Before

```text
This PR improves the user experience and refactors the dashboard code to make it more maintainable.
```

### SubstanceGuard Review

Verdict: Revise  
Score: 2/5

Main issues:

- Says what kind of improvement, but not what changed
- No reason for the refactor
- No risk statement
- No test coverage
- No reviewer guidance

### After

```text
This PR splits the dashboard data loading logic from the rendering components.

Why:
- The dashboard component mixed API calls, loading state, and presentation logic, making it hard to test.

Changed:
- Moved API calls into `useDashboardData`.
- Kept rendering in `DashboardView`.
- Added loading and error states to the hook result.

Tested:
- Ran existing dashboard unit tests.
- Manually checked loading, success, and error states.

Risk:
- Medium. The rendered UI should be unchanged, but data-loading behavior moved to a new hook.
```

## Example 4: secondBrain Extraction

### Before

```text
We discussed that it might be useful to have some kind of process for reducing AI slop. This is important because AI outputs are sometimes too generic, and in the future it could be helpful to improve this. SubstanceGuard is a nice name and could become a skill.
```

### SubstanceGuard Extract Mode

```text
SubstanceGuard is a proposed operator skill for reducing AI slop before content is saved, published, committed, or reused.

Core goal:
- Increase substance, specificity, grounding, and actionability.

Primary use cases:
- AI answer review
- Documentation review
- PR description gating
- secondBrain note extraction
- Research summary cleanup

Operating loop:
- Use -> Observe -> Label -> Refine -> Example -> Commit
```

## Example 5: Research Summary Review

### Before

```text
The market is changing rapidly, and many companies are investing in AI. This creates both opportunities and challenges. Businesses need to adapt quickly to stay competitive.
```

### SubstanceGuard Review

Verdict: Reject  
Score: 1/5

Main issues:

- Could apply to almost any market
- No time period, companies, segment, evidence, or source
- No concrete opportunity, challenge, or decision criterion

### After

```text
This summary is not usable without evidence. Add at least:

- Market segment
- Time period
- Named companies or categories
- Source material
- Specific changes observed
- Implications for the user's decision

Do not claim that the market is changing rapidly unless the source material shows what changed and over what period.
```

## Adding New Examples

When adding a new example, include:

```text
## Example N: Short name

### Before

### SubstanceGuard Review

Verdict: Pass | Revise | Reject
Score: 1-5

Main issues:
- ...

### After

```

Prefer real examples from actual usage. Anonymize sensitive content before committing.
