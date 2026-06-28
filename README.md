# PMOS — AI Product Manager Operating System

PMOS is an AI-powered operating system for product management. It orchestrates
prompts, workflows, and a knowledge base to automate and augment the day-to-day
work of a product manager — from discovery and spec writing to roadmap planning,
stakeholder communication, and release coordination.

> **Status:** Early scaffolding. This repository currently contains project
> structure and documentation only — no application code yet.

## What PMOS does

- **Discovery** — synthesize user research, support tickets, and feedback into themes.
- **Specification** — draft PRDs, user stories, and acceptance criteria from intent.
- **Planning** — turn priorities into roadmaps, sprint plans, and estimates.
- **Communication** — generate stakeholder updates, release notes, and FAQs.
- **Knowledge** — maintain a living, queryable knowledge base of product context.

## Repository layout

| Directory     | Purpose                                                              |
| ------------- | -------------------------------------------------------------------- |
| `docker/`     | Container definitions and compose files for local and prod runtimes. |
| `docs/`       | Architecture, design decisions, and contributor documentation.       |
| `prompts/`    | Versioned prompt templates used by the AI agents.                    |
| `workflows/`  | Multi-step agent workflow definitions (discovery, spec, planning).   |
| `scripts/`    | Operational and developer tooling (setup, seed, maintenance).        |
| `knowledge/`  | Knowledge base sources and indexing inputs (RAG corpus).             |
| `tests/`      | Automated tests (unit, integration, evals).                          |
| `.github/`    | CI/CD workflows and repository automation.                           |

## Getting started

> Application code is not yet present. These steps describe the intended flow.

```bash
# 1. Clone and enter the repo
git clone <repo-url> && cd pmos

# 2. Configure environment
cp .env.example .env
# edit .env with your API keys and settings

# 3. Bring up the local stack
docker compose -f docker/docker-compose.yml up --build
```

## Documentation

See [`docs/`](./docs) for architecture and design documentation. Start with
[`docs/architecture.md`](./docs/architecture.md).

## Contributing

Read [`docs/contributing.md`](./docs/contributing.md) before opening a pull
request. All changes run through the CI defined in [`.github/`](./.github).

## License

To be determined.
