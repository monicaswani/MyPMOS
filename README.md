# PMOS — AI Product Manager Operating System

PMOS is an AI-powered operating system for product management. It orchestrates
prompts, n8n workflows, and a living knowledge base to automate and augment a
product manager's work — from discovery and spec writing to roadmap planning,
stakeholder communication, and release coordination.

> **Status:** Early scaffolding. This repository currently contains project
> structure and documentation only — no application code yet.

---

## Vision

Product managers spend most of their time moving context between tools — turning
meetings into notes, notes into specs, specs into roadmaps, and roadmaps into
stakeholder updates. PMOS captures product context **once** and makes it reusable
**everywhere**, with AI drafting the artifacts and the PM staying firmly in the
loop. PMOS proposes; the PM decides.

---

## Features

- **Meeting copilot** — capture meetings, summarize, and extract action items.
- **PRD copilot** — turn intent into PRDs, user stories, and acceptance criteria.
- **Customer research** — synthesize feedback and tickets into themes and opportunities.
- **Roadmap planning** — convert priorities into roadmaps, estimates, and sprint plans.
- **Executive reporting** — generate stakeholder updates, release notes, and status reports.
- **Knowledge base** — a queryable, retrieval-grounded source of product truth (RAG).
- **Versioned prompts & workflows** — prompts and automations are reviewed data, not hard-coded.

---

## Architecture

PMOS is organized into four conceptual layers. Reasoning is grounded in retrieved
knowledge, and orchestration sequences everything into repeatable workflows.

```
                ┌─────────────────────────────────────────────┐
                │                 Interface                     │
                │            API · CLI · (future UI)            │
                └───────────────────────┬───────────────────────┘
                                        │
                ┌───────────────────────▼───────────────────────┐
                │              Orchestration (n8n)               │
                │  meeting-copilot · prd-copilot · research ···  │
                └───────┬───────────────────────────────┬───────┘
                        │                               │
        ┌───────────────▼───────────────┐   ┌───────────▼───────────────┐
        │        Reasoning (Claude)      │   │     Knowledge (RAG)        │
        │   versioned prompts + tools    │◄──┤   vector store (Qdrant)    │
        └───────────────┬───────────────┘   └────────────────────────────┘
                        │
        ┌───────────────▼───────────────────────────────────────────────┐
        │      Stores:  PostgreSQL (artifacts) · Redis (cache/queue)      │
        └─────────────────────────────────────────────────────────────────┘
```

**Flow:** a request enters through the interface, an n8n workflow orchestrates the
steps, Claude reasons over versioned prompts while retrieving grounding context
from the knowledge base, and results are persisted as product artifacts.

See [`docs/architecture/overview.md`](./docs/architecture/overview.md) for detail.

---

## Folder structure

```
PMOS/
├── .github/                # CI/CD workflows and repo automation
├── docker/                 # Container definitions and compose files
│
├── docs/
│   ├── architecture/       # System architecture and component overviews
│   ├── decisions/          # Architecture Decision Records (ADRs)
│   ├── setup/              # Setup, environment, and contributor guides
│   └── api/                # API and interface documentation
│
├── prompts/                # Versioned prompt templates, by domain
│   ├── meeting/
│   ├── prd/
│   ├── analytics/
│   ├── roadmap/
│   └── executive/
│
├── workflows/              # n8n workflow definitions, by use case
│   ├── meeting-copilot/
│   ├── prd-copilot/
│   ├── customer-research/
│   └── executive-report/
│
├── scripts/                # Operational and developer tooling
├── knowledge/              # Knowledge base sources (RAG corpus)
├── tests/                  # Unit, integration, and eval tests
│
├── README.md
├── CLAUDE.md               # Permanent project instructions for Claude Code
├── .env.example
└── .gitignore
```

---

## Quick Start

> Application code is not yet present. These steps describe the intended flow.

```bash
# 1. Clone and enter the repo
git clone <repo-url> && cd pmos

# 2. Configure environment
cp .env.example .env
# edit .env with your Anthropic API key and service settings

# 3. Bring up the local stack (app, Postgres, Redis, vector DB, n8n)
docker compose -f docker/docker-compose.yml up --build
```

Prerequisites: Docker + Docker Compose, and an Anthropic API key. See
[`docs/setup/`](./docs/setup) for full setup and contribution guides.

---

## Roadmap

| Phase | Focus                          | Status         |
| ----- | ------------------------------ | -------------- |
| 0     | Project scaffolding & docs     | ✅ Done         |
| 1     | Core platform (API, DB, RAG)   | 🔜 Next        |
| 2     | Meeting copilot                | ⏳ Planned      |
| 3     | PRD copilot                    | ⏳ Planned      |
| 4     | Customer research synthesis    | ⏳ Planned      |
| 5     | Roadmap planning               | ⏳ Planned      |
| 6     | Executive reporting            | ⏳ Planned      |

---

## Future Modules

- **Integrations** — Slack, Jira, GitHub, and calendar sync.
- **Analytics module** — usage and outcome metrics for product decisions.
- **Experiment tracking** — hypotheses, A/B tests, and result synthesis.
- **OKR alignment** — link roadmap items to objectives and key results.
- **Web UI** — a dashboard surface over the API and workflows.
- **Multi-workspace** — team and organization separation with shared knowledge.

---

## Documentation

- [`CLAUDE.md`](./CLAUDE.md) — permanent project instructions and conventions.
- [`docs/`](./docs) — architecture, decisions, setup, and API documentation.

## License

To be determined.
