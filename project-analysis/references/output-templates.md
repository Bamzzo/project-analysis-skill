# Output Templates

Use these templates as starting points. Adapt section order to the user's goal.

## Standard Project Analysis

```markdown
# Project Analysis

## Evidence Summary
- Files inspected:
- Commands run:
- Runtime verification:
- Not verified / blocked:
- Sampling strategy:

## 1. Project Overview
- Purpose:
- Target users:
- Current maturity:
- Core value:

## 2. Technology Stack
- Languages:
- Frameworks:
- Runtime:
- Package/dependency management:
- External services:

## 3. Directory and Key File Map
| Path | Role | Notes |
|---|---|---|

## 4. Startup and Runtime Path
- Install/setup:
- Main startup command:
- Runtime ports/processes:
- Health check:
- Common startup failure points:

## 5. Architecture
Include a Mermaid diagram when useful.

## 6. Main Data/Control Flow
Step-by-step request/task path.

## 7. Core Modules
| Module | Responsibility | Called by | Depends on | Failure modes |
|---|---|---|---|---|

## 8. State and Data Contracts
- Config:
- Persistent state:
- Runtime state:
- Main schemas/contracts:
- Important ids/handles:

## 9. External Dependencies
| Dependency | Purpose | Config | Failure mode | Verification |
|---|---|---|---|---|

## 10. Testing and Verification
- Existing tests:
- Manual smoke tests:
- Missing tests:
- Suggested verification path:

## 11. Risks and Open Questions
| Risk/Question | Evidence | Impact | Suggested next step |
|---|---|---|---|

## 12. Recommended Next Steps
- Short term:
- Medium term:
- Long term:

## 13. Newcomer Reading Path
1. ...
2. ...
3. ...
```

## Evidence-Backed Architecture Analysis

```markdown
# Evidence-Backed Architecture Analysis

## Executive Summary
- What the system does:
- How confident this analysis is:
- Most important validated fact:
- Most important unverified assumption:
- Highest-risk area:

## Evidence Ledger
| Claim | Evidence | Label |
|---|---|---|
|  | file:path or command output summary | Observed / Documented / Runtime-verified / Inferred / Open |

## Repository Shape
- Project type:
- Package/service boundaries:
- Generated/vendor/build areas skipped:
- In-scope areas:
- Out-of-scope areas:

## Runtime and Entry Points
| Unit | Start/build/test command | Entrypoint | Evidence |
|---|---|---|---|

## Architecture Map
Include a Mermaid diagram when useful.

## Core Flows Traced
| Flow | Start | Major modules | State/external systems | Verification |
|---|---|---|---|---|

## State, Contracts, and Side Effects
- Configuration:
- Persistent state:
- Runtime state:
- Public contracts:
- Side effects:

## Test and Verification Coverage
- Existing tests:
- Commands run:
- What passing tests prove:
- Missing verification:

## Risk Register
| Risk | Evidence | Impact | Likelihood | Next action |
|---|---|---|---|---|

## Open Questions
| Question | Why it matters | How to answer |
|---|---|---|

## Recommended Next Actions
1. ...
2. ...
3. ...
```

## Quick Triage

```markdown
# Quick Project Triage

## What This Project Appears To Be

## Main Tech Stack

## Most Important Files

## How It Likely Runs

## Main Flow

## Immediate Risks / Unknowns

## Best Next Commands
```

## Deep Architecture Report

```markdown
# Deep Architecture Report

## Executive Summary

## Repository Evidence
- Files inspected:
- Commands run:
- Facts vs inferences:
- Sampling strategy:
- Areas not covered:

## System Context
- Users:
- Inputs:
- Outputs:
- External systems:

## Architecture Diagram

## Layer-by-Layer Breakdown

## Main Flow Trace

## Data Models and Contracts

## State, Persistence, and Consistency

## Error Handling and Recovery

## Security and Secret Handling

## Testing Strategy

## Performance and Scalability Considerations

## Maintainability Assessment

## Risk Register

## Refactor or Extension Plan

## Open Questions
```

## Debug-Oriented Analysis

```markdown
# Debug Analysis

## Symptom

## Expected Behavior

## Reproduction Path

## System Layers Involved

## Evidence Collected

## Likely Failure Boundaries

## Hypotheses
| Hypothesis | Evidence For | Evidence Against | How to Test |
|---|---|---|---|

## Isolation Plan

## Safe Fix Strategy

## Verification Plan

## Residual Risk
```

## Weekly/Progress Report

```markdown
# Weekly Progress Report

## 1. Background

## 2. Work Goals

## 3. Work Completed

## 4. Technical Understanding Gained

## 5. Validation and Results

## 6. Problems Encountered

## 7. Current Status

## 8. Next Plan
```

## Technical Handoff

```markdown
# Technical Handoff

## Project Context

## Current Environment

## What Works

## What Does Not Work

## Important Commands

## Key Files and Modules

## Main Runtime Flow

## Known Issues

## Decisions Already Made

## Do Not Change Yet

## Suggested Next Steps
```
