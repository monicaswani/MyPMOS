# knowledge/

Source material for the PMOS knowledge base — the corpus used for retrieval
(RAG) by agents.

## Structure (suggested)

- `sources/` — raw documents (product docs, research, guidelines).
- `index/` — generated embeddings/index (git-ignored; build with `scripts/index`).
- `cache/` — derived artifacts (git-ignored).

## Conventions

- Keep curated, license-clear source material here.
- Do **not** commit customer PII or confidential data.
- Generated indexes and caches are regenerated, not committed.
