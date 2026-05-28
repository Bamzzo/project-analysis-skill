# Infrastructure, Deployment, and DevOps Project Analysis

Use this reference for Terraform, Pulumi, CloudFormation, Kubernetes, Docker, CI/CD, deployment scripts, platform tooling, or cloud infrastructure repositories.

## First Questions

- What environments exist: local, dev, staging, production, preview?
- What cloud/provider/runtime is targeted?
- Which files define infrastructure state?
- Which commands plan, apply, deploy, roll back, or destroy?
- Where are secrets, variables, and remote state configured?
- What parts are safe to inspect, plan, or run locally?

## Components to Locate

- Infrastructure root modules/stacks
- Environment-specific overlays or variable files
- Container build files and compose files
- Kubernetes manifests, Helm charts, or Kustomize overlays
- CI/CD workflow definitions
- Deployment scripts and release automation
- State backends and lock configuration
- Secrets references and parameter stores
- Monitoring, logging, alerting, and health checks

## Environment Map

For each environment, capture:

- Name
- Config path
- Provider/account/region/cluster if visible
- State backend or deployment target
- Deployment command
- Approval or promotion gate
- Rollback path
- Risks and unknowns

## Safety Rules

- Do not run apply, deploy, destroy, migration, or write commands unless explicitly requested.
- Prefer read-only commands, config inspection, validation, formatting checks, or dry-run/plan commands.
- Redact secrets and account-sensitive values.
- Distinguish declared infrastructure from actually deployed infrastructure.

## Common Failure Modes

- Environment variable defaults point to production.
- Remote state is shared across environments.
- CI deploy path differs from documented manual path.
- Resource names are generated in non-obvious ways.
- Image tags are mutable.
- Kubernetes overlays drift from base manifests.
- Secrets are required but not documented.
- Rollback is assumed but not implemented.

## Verification

Prefer:

- syntax validation
- formatter/check commands
- dry-run/plan without applying
- container build dry run when safe
- CI workflow inspection
- health check endpoint or readiness/liveness config review

## Recommended Output Additions

For infrastructure projects, add:

1. Environment and Deployment Map
2. State and Secret Handling
3. CI/CD Flow
4. Plan/Apply or Build/Deploy Boundary
5. Operational Risks
6. Safe Verification Commands
