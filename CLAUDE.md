# CLAUDE.md

Permanent project instructions for Claude Code working in this repository. Read
this before making changes. Keep changes consistent with the principles below.

## Project vision

PMOS (AI Product Manager Operating System) is an AI-powered operating system for
product management. It orchestrates prompts, workflows, and a knowledge base to
automate and augment a product manager's work — discovery, specification,
planning, communication, and release coordination — so that product context is
captured once and reused everywhere.

## Product goals

- Turn raw inputs (feedback, research, tickets) into structured product artifacts.
- Draft PRDs, user stories, and acceptance criteria from stated intent.
- Convert priorities into roadmaps, sprint plans, and estimates.
- Generate stakeholder updates, release notes, and FAQs.
- Maintain a living, queryable knowledge base as the single source of product truth.
- Keep a human in the loop: PMOS proposes, the PM decides.

## Tech stack

- **LLM provider:** Anthropic (Claude). Default model `claude-opus-4-8`.
- **Orchestration:** n8n for multi-step agent workflows.
- **Data:** PostgreSQL (entities, artifacts, audit history).
- **Knowledge / RAG:** vector store (Qdrant) over the `knowledge/` corpus.
- **Cache / queue:** Redis.
- **Containers:** Docker / Docker Compose.
- **CI/CD:** GitHub Actions (`.github/workflows/`).

> When the stack is extended, update this section and `docs/architecture.md` together.

## Architecture principles

- **Four layers:** Interface → Orchestration → Reasoning → Knowledge. Keep
  responsibilities within their layer.
- **Prompts and workflows are data**, versioned and reviewed — never hard-coded.
- **Knowledge is decoupled from reasoning** so the corpus can evolve independently.
- **Deterministic where possible:** isolate model calls to named, observable steps.
- **Idempotent operations:** scripts and workflows should be safe to re-run.
- **Secrets via environment** (`.env`), never in code, prompts, or the repo.
- **Human-in-the-loop** for any irreversible or outward-facing action.

## Coding standards

- Match the style of surrounding code: naming, structure, and comment density.
- Prefer small, focused modules and pure functions; isolate side effects.
- Read configuration from environment variables, not hard-coded constants.
- Validate inputs at boundaries; fail loudly with clear errors.
- No secrets, customer PII, or confidential data in code or fixtures.
- Every behavioral change ships with tests (see `tests/`).
- Keep functions and files cohesive; refactor when a unit grows multiple concerns.

## Folder purpose

| Directory     | Purpose                                                              |
| ------------- | -------------------------------------------------------------------- |
| `docker/`     | Container definitions and compose files (local and prod).            |
| `docs/`       | Architecture, decisions (ADRs), setup, and API docs.                 |
| `prompts/`    | Versioned prompt templates by domain (meeting, prd, analytics, ...). |
| `workflows/`  | n8n workflow definitions (meeting/prd copilots, research, reports).  |
| `scripts/`    | Operational and developer tooling (setup, seed, index, lint, test).  |
| `knowledge/`  | Knowledge base sources and indexing inputs (RAG corpus).             |
| `tests/`      | Automated tests (unit, integration, evals).                          |
| `.github/`    | CI/CD workflows and repository automation.                           |

## How we use AI

- AI **proposes**; the PM **approves**. Default to generating drafts, not final
  decisions or irreversible actions.
- All reasoning runs through versioned prompts in `prompts/` — no inline prompt
  text scattered in code or workflows.
- Ground responses in retrieved knowledge (RAG) rather than model memory whenever
  product-specific facts are involved; cite sources where possible.
- Pin the model via `PMOS_MODEL`; keep generation parameters explicit.
- Never send secrets or confidential customer data to the model.
- Treat model output as untrusted input: validate before persisting or acting.

## Rules for prompts

- One concern per prompt file; name by task (e.g., `prd/draft.md`).
- Document expected inputs and outputs at the top of each prompt.
- Use `{{variable}}` placeholders for runtime-injected values.
- Organize by category: `meeting/`, `prd/`, `analytics/`, `roadmap/`, `executive/`.
- Review prompt changes like code; never embed secrets or customer data.
- Prefer explicit instructions and output schemas over open-ended phrasing.

## Rules for n8n workflows

- Each workflow is self-contained and documents its trigger, inputs, and outputs.
- Reference prompts from `prompts/` by name — do not inline prompt text in nodes.
- Store credentials in n8n's credential store / environment, never in node JSON.
- Keep workflows deterministic; isolate model and external calls to named nodes.
- Make workflows idempotent and safe to re-run; handle partial failures explicitly.
- Export workflow JSON into its subdirectory for version control; review diffs on change.
- Group workflows by domain: `meeting-copilot/`, `prd-copilot/`, `customer-research/`, `executive-report/`.

## Documentation standards

- Update docs in the same change as the code or config they describe.
- Capture design decisions as short, dated ADR entries in `docs/`.
- Keep `README.md`, `CLAUDE.md`, and `docs/architecture.md` mutually consistent.
- Each directory carries a `README.md` describing its purpose and conventions.
- Write concise, present-tense prose; prefer tables and lists over long paragraphs.

## Git commit conventions

- Use imperative, present-tense summaries (e.g., "Add discovery workflow").
- Keep the subject line ≤ 72 characters; add a body explaining *why* when useful.
- One logical change per commit; avoid mixing refactors with behavior changes.
- Reference issues/PRs where applicable (e.g., `Closes #123`).
- Never commit secrets, `.env`, or generated artifacts (`knowledge/index/`, caches).
- Branch from `main`; all changes merge via PR with passing CI.
