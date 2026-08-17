# JOSS submission — checklist and paste-ready text

Submit at <https://joss.theoj.org/papers/new>. JOSS signs you in with
**ORCID**, so an ORCID iD is required; put the same iD in `paper/paper.md`
(`orcid:` under authors) before submitting.

## Pre-flight (all automated; check they are green)

- `CI` workflow green on `main` (tests, both conformance suites, no drift, build).
- `JOSS paper` workflow green (paper compiles with JOSS's own toolchain; PDF is the run artifact — read it once).
- Tagged release exists and is archived: v0.1.1 → Zenodo version DOI `10.5281/zenodo.21984096`, concept DOI `10.5281/zenodo.21984095`.
- `paper/paper.md`: 250–1000 words (currently ~620), Summary + Statement of need present, every `[@key]` resolves in `paper.bib`.
- ORCID filled in (`0000-0000-0000-0000` placeholder replaced).

## Form fields

| Field | Value |
|---|---|
| Repository URL | `https://github.com/isaacsight/provenance-substrate` |
| Git branch | `main` |
| Version | `v0.1.1` |
| Software archive DOI (asked at acceptance) | `10.5281/zenodo.21984096` (version) — concept `10.5281/zenodo.21984095` |
| Kind of submission | New submission |
| Suggested subject / editor area | Computer science; reproducibility & research software; formal methods; AI-assisted science |
| Keywords | provenance, reproducibility, formal verification, Lean 4, peer review, hash chain, conformance testing, canonical JSON, AI safety |

## Cover-letter text (the "Comments to the editor" box)

> `provenance-substrate` is a dependency-free Python library plus a language-neutral conformance suite for making AI-assisted work checkable: a model's output is treated as a claim, a deterministic engine (the Lean kernel, a re-executed computation, an arithmetic reconciler) must confirm it, a human signs the exact bytes, and every step is hash-chained. It generalizes the ledger substrate of `@kernel.chat/kbot-finance` (TypeScript) to Lean proofs, manuscript claims, paper reproductions, a quantitative-hallucination benchmark, and peer-review provenance. Conformance is proved by vectors, not prose: the finance v1 suite (143 vectors) is vendored from the TypeScript reference and passes byte-for-byte; the academic v1 suite (167 vectors, 24 kinds) is generated from this implementation and checked for drift in CI. Closest prior art (deterministic integrity gates for LLM-assisted clinical manuscripts, arXiv 2606.09500; CODECHECK; in-toto/SLSA; PROV/RO-Crate/nanopublications) is discussed and differentiated in the paper. Archived at Zenodo, concept DOI 10.5281/zenodo.21984095; on PyPI as `provenance-substrate`.

## Honest notes for the reviewer conversation

- The Python repository is young (extracted 2026-08-17). The substrate it ports has a longer history in the `kernel` monorepo and `kbot-finance` package; link that history if an editor asks about JOSS's "substantial scholarly effort" heuristic.
- The real Lean kernel path (`LakeDisposer`) is not exercised in CI (no Lean on the runner); the stub-kernel path is fully covered and the LakeDisposer errors clearly when Lean is absent. Say so if asked; do not overclaim.
- Negative reproductions currently stop at the verifier stage and are not signable as dataset rows; a policy flag is planned. Say so if asked.
