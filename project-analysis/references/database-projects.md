# Database and Persistence Project Analysis

Use this reference for database-heavy applications, schema repositories, migrations, ORMs, persistence layers, data access modules, or projects where correctness depends on stored state.

## First Questions

- What database or storage engines are used?
- What is the source of truth for schema: migrations, ORM models, SQL files, introspection, generated types, or docs?
- How are environments separated: local, test, staging, production?
- How are migrations created, ordered, applied, rolled back, and verified?
- Where are seeds, fixtures, factories, and sample data defined?
- What transactions, constraints, indexes, and consistency assumptions protect data?
- What data is sensitive, tenant-scoped, user-owned, cached, or derived?

## Components to Locate

- Migration directories and migration runner config
- ORM models, generated clients, schema files, and query builders
- Database connection/config loading
- Repository/data-access modules
- Seed scripts, fixtures, factories, and local dev containers
- Query files, stored procedures, triggers, functions, views, and materialized views
- Backup, restore, replication, or retention scripts
- Tests for migrations, repositories, and data invariants

## Contract Map

For each important table, collection, topic, or persisted artifact, capture:

- Name and storage technology
- Producer and consumer modules
- Primary keys and important identifiers
- Required fields and constraints
- Indexes or access patterns
- Ownership/tenant boundary
- Lifecycle: created, updated, archived, deleted
- Migration or compatibility risk

## Safety Rules

- Do not run migrations, seed scripts, destructive SQL, write queries, reset commands, or production-like connection commands unless explicitly requested.
- Prefer schema inspection, migration dry-runs, generated SQL review, test database checks, or read-only queries against local fixtures.
- Redact credentials, connection strings, tokens, account ids, and sensitive sample records.
- Distinguish declared schema from the actually deployed schema when only code has been inspected.

## Common Failure Modes

- ORM models and migrations disagree.
- Migrations are not reversible or not idempotent.
- Local seeds hide production nullability, volume, or tenant-shape issues.
- Indexes do not match query patterns.
- Transactions are missing around multi-step writes.
- Soft delete, archival, or retention behavior is inconsistent.
- Generated clients or schema types are stale.
- Background jobs assume data freshness or ordering not enforced by the database.

## Verification

Prefer:

- inspect migration history and ordering
- run schema validation or migration status against a local/test database when safe
- run repository tests or data-access unit tests
- review generated SQL or ORM query output
- check indexes for the main traced queries
- validate seed/sample data covers the traced path

## Recommended Output Additions

For database or persistence-heavy projects, add:

1. Storage Technology and Environment Map
2. Schema Source of Truth
3. Migration and Rollback Path
4. Data Contract Map
5. Query and Transaction Flow
6. Data Integrity and Sensitivity Risks
7. Safe Verification Commands
