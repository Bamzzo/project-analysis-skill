# Data, ML, and Pipeline Project Analysis

Use this reference for data pipelines, analytics, ETL/ELT, training, evaluation, inference, notebooks, model-serving, RAG indexing, or experiment repositories.

## First Questions

- What is the pipeline goal: ingest, transform, train, evaluate, serve, index, or report?
- What are the main inputs and outputs?
- Where are datasets, features, models, artifacts, and metrics stored?
- What configuration controls runs?
- Is execution batch, streaming, interactive, scheduled, or service-based?
- What is deterministic and what depends on external data or model behavior?

## Components to Locate

- Pipeline runner or orchestration entrypoint
- Config loader and environment handling
- Data connectors and storage paths
- Transform/feature code
- Training, evaluation, inference, or indexing code
- Model/provider adapters
- Experiment tracking and metrics
- Artifact serialization and versioning
- Notebooks and scripts used as operational entrypoints
- Tests, golden datasets, sample inputs, or fixtures

## Data Contract Map

For each important dataset or artifact, capture:

- Name and path/source
- Producer
- Consumer
- Schema or expected columns/fields
- Freshness assumptions
- Size or sampling strategy
- Sensitive data risk
- Validation or quality checks

## Pipeline Flow

Trace:

```text
source data
-> extraction/loading
-> cleaning/normalization
-> feature/record construction
-> model/index/report step
-> metrics/artifacts/output
-> serving or downstream consumption
```

## Common Failure Modes

- Local sample data differs from production data.
- Schemas are implicit or only documented in notebooks.
- Random seeds, time windows, or external APIs make runs non-reproducible.
- Large data paths are hardcoded.
- Metrics are computed on stale or filtered data.
- Model artifacts lack version metadata.
- Evaluation data leaks into training.
- Notebook code is the real pipeline but is not tested.

## Verification

Prefer small, safe checks:

- run schema validation on sample data
- run a dry-run or tiny sample pipeline
- run unit tests for transforms
- inspect generated artifact metadata
- compare documented metrics with code-computed metrics
- verify environment variables and storage credentials without printing secrets

## Recommended Output Additions

For data/ML projects, add:

1. Pipeline Purpose
2. Data Sources and Artifacts
3. Schema and Freshness Contracts
4. Training/Evaluation/Inference Flow
5. Reproducibility and Data Quality Risks
6. Minimal Verification Dataset or Command
