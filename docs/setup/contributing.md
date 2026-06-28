# Contributing to PMOS

## Workflow

1. Branch from `main`.
2. Make focused changes with clear commit messages.
3. Ensure tests and linters pass locally (see `tests/` and `scripts/`).
4. Open a pull request; CI in `.github/` must pass before merge.

## Standards

- Keep prompts and workflows versioned and documented.
- Add or update tests for any behavioral change.
- Update relevant docs in `docs/` when architecture or interfaces change.
- Never commit secrets — use `.env` (ignored) based on `.env.example`.

## Commit messages

Use imperative, present-tense summaries (e.g., "Add discovery workflow").
