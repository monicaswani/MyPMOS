# ADR-001: Use Claude Code instead of Cursor

- **Status:** Accepted
- **Date:** 2026-06-28
- **Deciders:** PMOS core team

## Context

PMOS is a documentation- and configuration-heavy project: versioned prompts,
n8n workflow JSON, a RAG knowledge base, and per-folder conventions captured in
`CLAUDE.md`. We need an AI development environment that can reason across the
whole repository, follow durable project rules, and operate well in an automation
context — not just provide inline code completion.

We evaluated two primary options:

- **Cursor** — an AI-first IDE (VS Code fork) with strong inline completion,
  in-editor chat, and codebase indexing.
- **Claude Code** — Anthropic's agentic CLI/IDE tool that operates over the repo
  with tools (read, edit, run), persistent project instructions, and headless
  automation support.

## Decision

We will standardize on **Claude Code** as the primary AI development environment
for PMOS.

### Why Claude Code over Cursor

1. **Agentic, repo-wide workflow.** PMOS work is multi-step (scaffold, refactor,
   reconcile docs, commit). Claude Code executes these as tool-driven agent loops
   rather than completion-at-the-cursor, which fits how we build PMOS.
2. **Persistent project instructions.** `CLAUDE.md` is a first-class, durable
   contract that Claude Code reads on every session. This matches our principle
   of treating conventions as versioned data rather than per-developer settings.
3. **Editor-agnostic.** Claude Code runs in the terminal and across IDEs, so the
   team is not locked into a single editor fork.
4. **Automation & CI fit.** Headless/CLI operation lets us reuse the same agent
   in scripts and CI (`.github/`), aligning the dev tool with our orchestration
   strategy.
5. **Provider alignment.** PMOS already standardizes on Anthropic Claude for
   reasoning (`PMOS_MODEL=claude-opus-4-8`). Using Claude Code keeps tooling and
   runtime on a consistent model family and mental model.

## Consequences

### Positive

- Consistent, repo-aware automation from local development through CI.
- Project conventions live in `CLAUDE.md` and apply uniformly across contributors.
- No editor lock-in; contributors keep their preferred editor.

### Negative / trade-offs

- Less emphasis on real-time inline autocomplete than Cursor provides; developers
  who rely heavily on tab-completion may need to adjust their workflow.
- Terminal/agent-centric flow has a learning curve for IDE-first contributors.

### Neutral

- This decision concerns the development environment only; it does not constrain
  runtime architecture. Contributors may still use any editor alongside Claude Code.

## Alternatives considered

- **Cursor** — strong inline completion and indexing, but editor-bound and less
  suited to headless automation and durable, repo-level project instructions.
- **Plain editor + chat assistant** — rejected; no repository tool access or
  enforceable project conventions.
