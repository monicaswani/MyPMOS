# scripts/

Operational and developer tooling for PMOS.

## Planned scripts

- `setup` — install dependencies and prepare a local environment.
- `seed` — load sample data and knowledge for development.
- `index` — (re)build the knowledge vector index from `knowledge/`.
- `lint` / `test` — convenience wrappers used locally and in CI.

## Conventions

- Scripts should be idempotent and safe to re-run.
- Read configuration from environment variables (`.env`), not hard-coded values.
- Document required arguments at the top of each script.
