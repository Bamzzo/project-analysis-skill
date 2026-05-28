# Debugging-Oriented Project Analysis

Use this reference when the user's goal is to understand a bug, failed setup, broken integration, flaky workflow, or confusing runtime behavior.

## Debug First Principles

- Reproduce before fixing.
- Reduce the problem to the smallest failing path.
- Separate symptoms from causes.
- Change one major variable at a time.
- Verify the fix against the original symptom.
- Preserve user changes and avoid unrelated refactors.

## Failure Boundary Questions

- Did the request/action start?
- Did it reach the first boundary?
- Did each layer receive the expected input?
- Did each layer produce the expected output?
- Where is the first observed divergence?
- Is the failure deterministic?
- Did it ever work before?
- What changed recently?

## Common Layers

```text
User input
UI/client
Network
API route
Controller/service
Data/model layer
External dependency
Runtime environment
Output/renderer
```

For each layer, ask:

- Input present?
- Input shape correct?
- Handler invoked?
- Output present?
- Error logged?
- Timeout or cancellation?

## Evidence to Collect

- Exact command
- Exact error
- Logs around failure time
- Config values with secrets redacted
- Environment versions
- Branch and working tree state
- Minimal input
- Expected vs actual output
- Recent changes

## Hypothesis Table

Use when there are multiple likely causes:

| Hypothesis | Evidence For | Evidence Against | Test | Result |
|---|---|---|---|---|

## Isolation Plan

1. Verify environment and config.
2. Run health checks.
3. Call the failing API/tool directly.
4. Replace real external dependencies with a mock if possible.
5. Test the smallest internal function.
6. Reconnect layers one by one.
7. Run the original end-to-end path.

## Fix Strategy

Prefer:

- Minimal targeted changes.
- Better diagnostics when root cause is uncertain.
- Tests that fail before the fix and pass after.
- Documentation updates for setup/config issues.

Avoid:

- Broad rewrites during debugging.
- Suppressing errors without understanding them.
- Treating successful command exit as proof that user-visible behavior works.
- Blaming the model/framework before checking local configuration and data flow.

## Verification Plan

Include:

- Command/test run
- Manual smoke test if needed
- Expected observable outcome
- Regression risk
- Residual unknowns
