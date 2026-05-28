# Analysis Checklists

Use these checklists during repository analysis. Do not dump them verbatim unless the user asks for a checklist; use them to avoid missing important areas.

## Repository Surface

- What is the project name and stated purpose?
- What languages and package managers are present?
- What are the top-level directories?
- Are there docs, examples, tests, scripts, CI, or deployment files?
- Is there an environment template such as `.env.example`?
- Are generated files, caches, virtualenvs, build outputs, logs, or secrets ignored?
- Does the repository appear clean, incomplete, forked, or heavily modified?
- Is this a single project, monorepo, nested project, or mixed-language system?
- Which directories should be skipped during analysis because they are generated, vendored, cached, or build output?

## Scale and Sampling

- Is the repository small enough to inspect directly?
- If not, what sampling strategy is being used?
- Which package/service/app boundaries are in scope?
- Which areas are explicitly out of scope for this pass?
- What files establish the source of truth for scripts, builds, tests, and deployment?
- Are there duplicate or stale docs that conflict with code/config?

## Entry Points

- How is the project started locally?
- What command runs the main service/app?
- What file creates the app/server/CLI?
- What routes or handlers receive user/API requests?
- What background workers, queues, or scheduled tasks exist?
- What commands run tests, builds, linting, or packaging?

## Architecture

- What are the main layers?
- What module handles input?
- What module dispatches work?
- What module contains core domain logic?
- What module talks to external systems?
- Where is state stored?
- How are errors represented and propagated?
- Which components are replaceable adapters?
- Which boundaries are real runtime boundaries versus directory organization only?
- Which components are public/stable contracts and which are internal details?

## Data and Control Flow

- What is the most important user or system request?
- What path does it take through the code?
- What data is transformed at each step?
- What ids, paths, handles, or state references are passed forward?
- What external side effects occur?
- How does the result return to the caller?

## State and Contracts

- What configuration is required?
- Which environment variables are read?
- What schemas or models define inputs/outputs?
- What files or database records are read/written?
- What runtime state is kept in memory?
- What cache or persistence layer exists?
- What data can become stale?
- What state must be refreshed before writes?

## External Dependencies

- Third-party APIs
- Model providers
- Databases
- Message queues
- Filesystem locations
- Desktop software
- Browser/runtime dependencies
- OS-specific features
- Cloud services

For each dependency, identify:

- Required configuration
- Authentication method
- Failure modes
- Timeout/retry behavior
- Local development substitute or mock

## Testing and Verification

- Are there unit tests?
- Are there integration tests?
- Are there end-to-end tests?
- Are there smoke tests or examples?
- Are tests runnable in the current environment?
- What core path has no test?
- How can a human manually verify the system?
- What command proves the project is basically healthy?
- What command was actually run during this analysis?
- What command should be run next if current execution is unsafe, slow, or blocked?
- What does a passing result prove, and what does it not prove?

## Evidence Quality

- Which claims are observed from code?
- Which claims come only from documentation?
- Which claims are runtime-verified?
- Which claims are inferred from names or structure?
- Which important claims lack evidence?
- Are file paths, commands, outputs, and line references included where useful?
- Are secrets redacted while still describing their presence and role?

## Risk Scan

- Configuration ambiguity
- Hardcoded paths or ports
- Missing error handling
- Hidden external state
- Non-idempotent writes
- Destructive operations
- Weak validation
- Stale documentation
- Missing tests
- Large untyped payloads
- Model hallucination or nondeterminism
- Concurrency or race conditions
- Platform-specific assumptions
- Over-broad public API surface
- Unclear package/service ownership
- Build or deployment scripts with side effects
- Runtime behavior hidden in generated code
- Production-like defaults in local commands

## Newcomer Orientation

- First file to read
- First command to run
- First API or UI flow to test
- First small safe change
- Files to avoid changing initially
- Concepts to learn before modifying core logic
- Safest module for a first contribution
- Highest-risk module to avoid until architecture is understood
