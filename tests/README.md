# tests/

Automated tests for PMOS.

## Layout (planned)

- `unit/` — fast, isolated tests for individual modules.
- `integration/` — tests across components (DB, vector store, queue).
- `evals/` — prompt and workflow quality evaluations against fixtures.

## Conventions

- Tests must be deterministic; mock external services and model calls in unit
  tests, and gate live-model evals behind explicit configuration.
- Every behavioral change ships with corresponding tests.
- Run via `scripts/test` (wrapper) or the language-native test runner.
