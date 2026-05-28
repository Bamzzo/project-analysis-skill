---
name: project-analysis
description: Use when asked to analyze, onboard, reverse-engineer, document, evaluate, audit, or plan non-trivial changes for a software project or repository, especially unfamiliar, large, legacy, messy, multi-package, or complex codebases. Helps identify project purpose, architecture, entry points, modules, data/control flow, dependencies, state, contracts, external systems, risks, tests, verification paths, and next actions.
---

# Project Analysis

Use this skill to turn an unfamiliar or messy project into a clear, actionable map. The goal is not only to summarize files, but to explain how the project works, where its core paths are, what can break, how to verify it, and what to do next.

## Operating Principles

- Inspect before concluding. Distinguish code facts, documentation facts, runtime facts, inferences, and open questions.
- Prefer the project's real structure over generic architecture claims.
- Find the main path first: input -> dispatch -> core logic -> external dependency -> state/output.
- Keep uncertainty visible. Say "inferred from" when not verified by execution.
- Tie important conclusions to evidence: file paths, commands, test output, configs, or docs.
- Produce action-oriented output: what to read, run, test, fix, or avoid next.
- Do not expose secrets. If scanning configs, mention secret presence generically and avoid printing values.
- Avoid exhaustive file-by-file summaries. Explain the system by role, flow, boundary, and risk.

## Choose Depth

If the user does not specify depth, use **standard**.

For very large repositories, start with the surface map even when the requested depth is deep or audit.

| Depth | Inspect | Execute | Output emphasis | Required evidence |
|---|---|---|---|---|
| **quick** | top-level docs, manifests, scripts, major directories | read-only discovery only | what it is, likely stack, key files, obvious risks, next commands | files/commands inspected and major unknowns |
| **standard** | docs, manifests, configs, entrypoints, core modules, tests/CI | safe read-only commands; run lightweight verification only when clearly appropriate | architecture map, startup path, main flow, verification path, next actions | file paths for main claims and commands actually run |
| **deep** | standard scope plus 1-3 traced high-value flows and relevant tests/contracts | targeted tests/build/typecheck or dry runs when safe | flow traces, state/contracts, failure modes, missing coverage | file/line evidence for traced paths and verification limits |
| **audit** | broad risk surface: config, auth, state, side effects, CI/CD, dependencies, tests | validation, dry-run, read-only, or explicitly safe commands only | evidence ledger, risk register, readiness judgment, prioritized remediation | evidence for every major risk or explicit "Open" label |

## Core Workflow

1. Clarify the analysis goal when needed:
   - onboarding, architecture report, debugging, refactor planning, weekly report, technical review, or learning roadmap.
   - If obvious from the user request, proceed without asking.

2. Inventory the repository:
   - List top-level files and directories.
   - Identify language/framework/package files.
   - Find docs, configs, scripts, tests, examples, CI, and environment templates.
   - Prefer fast search tools such as `rg --files`.
   - Ignore or de-prioritize generated/vendor/cache/build directories unless they are the subject of the task.

3. Classify the project shape:
   - single app, full-stack app, library, CLI, monorepo, agent system, data/ML pipeline, infrastructure project, plugin/extension, mobile/desktop app, or mixed system.
   - Select only the relevant reference files for that shape.

4. Find entry points:
   - Backend: `main`, app factory, routers, CLI entrypoints, package scripts.
   - Frontend: package scripts, app root, routing, API client.
   - Agent/automation: planner, tool registry, executor, state/observation, model adapter.
   - Data/ML: pipeline runner, config loader, train/eval/inference entrypoints.
   - Library/SDK: public exports, package metadata, examples, tests, docs.
   - Infrastructure: root modules, stacks, manifests, deployment scripts, CI workflows.

5. Identify modules and responsibilities:
   - Group files by role, not just by directory.
   - For each core module, capture purpose, callers, dependencies, inputs, outputs, and failure modes.

6. Trace the main flow:
   - Document control flow and data flow.
   - Include external systems, state stores, callbacks, queues, model calls, or filesystem effects.
   - Use Mermaid diagrams for non-trivial flows.

7. Analyze state and contracts:
   - Locate config, runtime state, persistent state, caches, generated files, and important ids.
   - Identify request/response schemas, tool schemas, data models, file formats, and error shapes.

8. Evaluate verification:
   - Find existing tests and test commands.
   - Identify health checks, smoke tests, example inputs, manual validation steps, and missing tests.
   - Record what was actually run, what was only inferred, and what could not be run.

9. Assess risks and next actions:
   - Separate known issues from potential risks.
   - Rank by impact and likelihood.
   - Recommend short-term, medium-term, and long-term next steps.

## Baseline Read-Only Discovery

Before deep reading, collect a small, safe baseline when the environment allows:

- Working tree state: `git status --short` when this is a git repository.
- File inventory: `rg --files` or the fastest available equivalent.
- Top-level structure: `ls`, `dir`, or platform equivalent.
- Project manifests: package, workspace, build, dependency, lock, CI, container, environment-template, and README files.
- Script surfaces: package scripts, Makefile targets, task runners, CLI help, test/build/lint commands.
- Ignore patterns: generated, vendored, cache, build, dist, virtualenv, notebook checkpoint, and dependency directories.

Inspect scripts before running them. Do not run install, update, format, codegen, migration, seed, deploy, apply, destroy, write, or production-contacting commands unless the user explicitly requests it or the command is clearly safe in context. If secret-like files or variables appear, describe their role without printing values.

## Large Project Protocol

For large or unfamiliar repositories, work in phases and avoid premature deep dives:

1. **Surface map**: collect top-level structure, package/workspace files, docs, scripts, CI, config, tests, and generated/vendor directories.
2. **System classification**: identify project type(s), runtime boundaries, package boundaries, ownership boundaries, and deployable units.
3. **Entry-point map**: find how each major unit starts, builds, tests, and talks to other units.
4. **Core path selection**: choose 1-3 highest-value flows to trace based on the user's goal.
5. **Evidence pass**: attach file paths, commands, or runtime outputs to important claims.
6. **Verification pass**: run safe commands when appropriate, or list exact commands that should be run and why they were not run.
7. **Synthesis**: produce a role-based architecture map, risks, open questions, and prioritized next actions.

When the repository is too large to inspect fully, state the sampling strategy and the areas not yet covered.

## Reference Loading

Load only the relevant reference files:

- For report structures and deliverable formats, read `references/output-templates.md`.
- For general project inspection prompts, read `references/analysis-checklists.md`.
- For Agent, LLM, tool-calling, workflow, or automation projects, read `references/agent-projects.md`.
- For frontend/backend/web apps, read `references/web-projects.md`.
- For debugging-oriented analysis, read `references/debugging-projects.md`.
- For monorepos, workspaces, multi-package repositories, or polyglot systems, read `references/monorepos.md`.
- For data, ML, analytics, ETL, training, evaluation, or inference projects, read `references/data-ml-projects.md`.
- For infrastructure, deployment, cloud, CI/CD, containers, Kubernetes, or Terraform projects, read `references/infra-projects.md`.
- For libraries, SDKs, CLIs, packages, plugins, or extension projects, read `references/library-cli-projects.md`.
- For mobile, desktop, Electron, Tauri, Flutter, React Native, Android, or iOS projects, read `references/mobile-desktop-projects.md`.
- For database-heavy projects, schema repositories, migrations, ORMs, or data persistence reviews, read `references/database-projects.md`.
- For security-sensitive reviews, authentication/authorization analysis, secret handling, or supply-chain risk, read `references/security-audit-projects.md`.

## Default Output Structure

For standard analysis, produce:

1. Project Overview
2. Technology Stack
3. Directory and Key File Map
4. Startup and Runtime Path
5. Architecture
6. Main Data/Control Flow
7. Core Modules
8. State and Data Contracts
9. External Dependencies
10. Testing and Verification
11. Risks and Open Questions
12. Recommended Next Steps
13. Newcomer Reading/Learning Path

Adjust this structure to the user's purpose. For reviews, lead with risks. For weekly reports, lead with work done and progress. For debugging, lead with symptoms, hypotheses, and isolation plan.

## Evidence Labels

When useful, label claims:

- **Observed**: confirmed by reading files or running commands.
- **Documented**: stated in docs, not independently verified.
- **Runtime-verified**: confirmed by command/test/API output.
- **Inferred**: reasonable conclusion from structure or names.
- **Open**: needs user confirmation or execution.

For architecture, startup, dependency, and risk claims, include evidence whenever practical:

- `file:path:line` for code/config/docs evidence.
- command names and summarized output for runtime evidence.
- "not verified" plus the blocker when execution was not possible or unsafe.

## Completion Criteria

Before finalizing, make sure the analysis answers these questions or labels them as open:

- What is this project, who/what uses it, and what value does it provide?
- How is it installed, started, built, tested, and deployed or packaged?
- Where are the main entrypoints and runtime boundaries?
- What are the most important data/control flows?
- Where do configuration, persistent state, runtime state, schemas, and external dependencies live?
- What has been verified by commands or runtime behavior, and what remains inferred?
- What are the highest-risk areas, safest next actions, and best newcomer reading path?

## Final Guidance

End with the highest-value next actions. A project analysis is successful only if the user knows what the project is, how it works, where to look next, and how to proceed safely.
