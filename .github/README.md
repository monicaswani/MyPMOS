# .github/

Repository automation and CI/CD configuration.

## Contents

- `workflows/` — GitHub Actions pipelines (lint, test, build).

## Conventions

- Keep CI fast and deterministic; cache dependencies where possible.
- Required checks must pass before merge to `main`.
- Store secrets in GitHub repository/organization secrets — never in the repo.
