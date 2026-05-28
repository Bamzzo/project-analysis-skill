# Monorepo and Multi-Package Analysis

Use this reference for monorepos, workspaces, polyglot repositories, multi-service systems, or repositories with many deployable/package units.

## First Questions

- Which workspace/package manager is used?
- What are the package/service boundaries?
- Which packages are apps, libraries, tools, configs, or generated artifacts?
- Which packages are deployable units?
- Which packages are shared dependencies?
- Are there multiple languages, runtimes, or build systems?
- Is ownership documented by CODEOWNERS, docs, team names, or directory conventions?

## Files to Inspect

- `package.json`, `pnpm-workspace.yaml`, `yarn.lock`, `turbo.json`, `nx.json`, `lerna.json`
- `Cargo.toml`, `go.work`, `go.mod`, `pyproject.toml`, `poetry.lock`, `uv.lock`
- `settings.gradle`, `build.gradle`, `pom.xml`, `.sln`, `.csproj`
- CI workflows, Dockerfiles, deployment manifests, Makefiles
- root README and package-level README files

## Boundary Map

For each important package or service, capture:

- Path
- Type: app, service, library, CLI, config, test fixture, generated, infra
- Runtime and build command
- Public exports or API surface
- Internal dependencies
- External dependencies
- Tests and verification command
- Deployment or release path

## Dependency Graph

Identify:

- Root-level dependencies shared by all packages
- Package-to-package dependencies
- Cycles or implicit coupling
- Generated clients or schemas
- Version pinning and release strategy
- Cross-language boundaries

## Common Failure Modes

- Root scripts hide package-specific behavior.
- Shared package changes break multiple apps.
- Build cache masks stale generated artifacts.
- Multiple package managers are accidentally mixed.
- Local dev and CI use different workspace filters.
- Generated clients or schemas are out of date.
- Package boundaries are organizational rather than technical.
- Tests only cover leaf packages, not integration paths.

## Verification

Prefer targeted commands:

- list workspaces/packages
- run root lint/typecheck/build if reasonably safe
- run one package-level test for the traced path
- verify generated code freshness if generators exist
- inspect CI matrix for the real source of truth

## Recommended Output Additions

For monorepos, add:

1. Workspace Map
2. Package/Service Boundary Table
3. Internal Dependency Graph
4. Shared Infrastructure and Tooling
5. Cross-Package Change Risk
6. Targeted Verification Commands
