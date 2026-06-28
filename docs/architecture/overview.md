# PMOS Architecture

> Living document. Updated as the system takes shape.

## Overview

PMOS is composed of four conceptual layers:

1. **Interface** — entry points for users (API, CLI, future UI).
2. **Orchestration** — agent workflows that sequence prompts and tools to
   complete product-management tasks (see `workflows/`).
3. **Reasoning** — LLM-backed agents driven by versioned prompts (see `prompts/`).
4. **Knowledge** — a retrieval layer over the product knowledge base
   (see `knowledge/`), backed by a vector store.

## Data flow

```
User request
   │
   ▼
Interface ──► Orchestration (workflow) ──► Reasoning (agent + prompt)
                     │                            │
                     ▼                            ▼
              Knowledge retrieval  ◄──────  Tool / integration calls
                     │
                     ▼
              Response + persisted artifacts
```

## Stores

- **Relational DB** (Postgres) — entities, artifacts, audit history.
- **Vector store** — embeddings for knowledge retrieval (RAG).
- **Cache/queue** (Redis) — short-term state and background jobs.

## Key decisions (to expand)

- Prompts and workflows are versioned as data, not hard-coded.
- Knowledge is decoupled from reasoning so the corpus can evolve independently.
