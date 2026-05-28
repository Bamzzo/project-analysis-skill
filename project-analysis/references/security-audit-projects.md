# Security-Sensitive Project Analysis

Use this reference for security-sensitive reviews, authentication/authorization analysis, secret handling, dependency/supply-chain risk, external action systems, or audit-oriented project analysis. This is a code and architecture review aid, not a substitute for a formal penetration test.

## First Questions

- What assets, users, tenants, data, credentials, or external systems need protection?
- Where are trust boundaries crossed: UI/API, service/service, model/tool, worker/job, database, filesystem, cloud, or desktop OS?
- How are users, services, agents, or tools authenticated?
- How is authorization enforced, and is it centralized or scattered?
- Where are secrets loaded, stored, logged, redacted, rotated, and passed to subprocesses?
- What input is untrusted, and where is it validated, parsed, escaped, or sandboxed?
- What third-party packages, generated artifacts, CI workflows, and deployment paths affect the trusted build?

## Components to Locate

- Auth middleware, guards, policies, sessions, token handling, and permission checks
- User, role, tenant, organization, and resource ownership models
- Input validators, serializers, parsers, upload handlers, and deserializers
- Secret/config loading, environment templates, vault/parameter store references
- Logging, telemetry, tracing, and error reporting
- External API clients, webhook handlers, callbacks, queues, and background jobs
- Tool/action registries, approval gates, sandboxing, and dry-run logic
- Dependency manifests, lockfiles, CI workflows, release scripts, and container images

## Risk Areas

- Auth bypass from missing route/middleware coverage
- Object-level authorization gaps across tenants or resource owners
- Secrets committed, echoed, logged, or passed into broad process environments
- Unsafe file paths, archive extraction, shell execution, template rendering, or deserialization
- SSRF, open redirects, webhook spoofing, weak signature checks, or replay risk
- Overbroad CORS, CSRF gaps, insecure cookies, or token storage problems
- Dependency confusion, unpinned actions/images, mutable tags, or generated artifact drift
- Agent/tool systems that allow destructive actions without preview, approval, or audit logs

## Safety Rules

- Do not print secrets, tokens, private keys, full connection strings, sensitive records, or exploit payloads.
- Prefer defensive analysis and validation over exploit execution.
- Do not run scanners, fuzzers, network probes, credential tests, or destructive payloads unless explicitly requested and scoped.
- Label security findings by evidence and confidence: confirmed, likely, possible, or open.

## Verification

Prefer:

- route/middleware coverage inspection
- permission-policy tests or missing-test identification
- secret redaction and logging review
- dependency and lockfile inspection
- CI/release workflow review
- safe local unit tests for validators, auth guards, and policy checks
- dry-run or read-only tool/action checks

## Recommended Output Additions

For security-sensitive analysis, add:

1. Asset and Trust Boundary Map
2. Authentication and Authorization Flow
3. Secret Handling and Redaction
4. Input Validation and External Action Surface
5. Supply-Chain and Release Risks
6. Confirmed Findings vs Open Risks
7. Prioritized Remediation Plan
