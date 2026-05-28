# Library, SDK, CLI, Plugin, and Extension Analysis

Use this reference for reusable packages, SDKs, command-line tools, plugins, extensions, framework integrations, or developer tooling.

## First Questions

- Who is the consumer: end user, developer, another package, runtime host, or plugin manager?
- What is the public API or command surface?
- What is internal implementation detail?
- How is the package built, versioned, released, and documented?
- What compatibility promises exist?
- What examples or tests define expected behavior?

## Components to Locate

- Package metadata and entrypoints
- Public exports
- CLI command parser and subcommands
- Plugin manifest or extension activation points
- Configuration schema
- Examples and docs
- Tests for public behavior
- Build and release scripts
- Changelog or version policy

## Public Surface Map

For each public API, command, or extension point, capture:

- Name
- Purpose
- Inputs/options
- Output/result
- Errors
- Side effects
- Stability or compatibility concerns
- Example usage
- Test coverage

## Flow Patterns

CLI:

```text
argv
-> command parser
-> config/env loading
-> command handler
-> core library
-> filesystem/network/process side effect
-> stdout/stderr/exit code
```

Library/SDK:

```text
consumer import
-> public API
-> validation/config
-> core implementation
-> adapter/external dependency
-> returned value/error
```

Plugin/extension:

```text
host runtime
-> manifest/activation
-> extension entrypoint
-> registered commands/hooks/tools
-> host API call
-> user-visible or system-visible effect
```

## Common Failure Modes

- Docs describe APIs that are not exported.
- Tests cover internals instead of public behavior.
- CLI exits with success after partial failure.
- Configuration precedence is unclear.
- Plugin activation depends on hidden host state.
- Release artifacts differ from source behavior.
- Breaking changes are not reflected in versioning.
- Error messages lack actionable context.

## Verification

Prefer:

- inspect package exports or generated types
- run documented examples
- run CLI help and one harmless command
- run public API tests
- build/package locally if safe
- check release workflow and published artifact configuration

## Recommended Output Additions

For libraries, SDKs, CLIs, plugins, or extensions, add:

1. Public Surface
2. Consumer Usage Path
3. Configuration and Error Contract
4. Build and Release Path
5. Compatibility Risks
6. Example-Based Verification
