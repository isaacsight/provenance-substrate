# Changelog

All notable changes. The academic v1 suite hash is the real changelog: if it
moved, reference behaviour moved, and the entry below says why.

## 0.1.1 — 2026-08-17

No behaviour change; suite hashes unchanged (finance v1 `be4cdbe3e0a53bbd…`, academic v1 `880744c3325c9227…`). Cut so that the first GitHub Release after enabling the Zenodo integration mints the concept DOI. Version string exposed in `provsubstrate.__version__` and the MCP `serverInfo` now match the package.

## 0.1.0 — 2026-08-17

First release. Extracted from the kernel.chat monorepo (PR #74) and moved to
this repository.

- Core: canonical JSON byte-compatible with the TypeScript reference
  (ECMA-262 number formatting, fuzzed against Node on 1,000 doubles),
  content-addressed envelopes, HMAC approval tokens, hash chain.
- `finance`: full port of the kbot-finance ledger substrate; **finance v1
  conformance 143/143** (suite `be4cdbe3e0a53bbd…`, vendored).
- `lean`, `claims`, `repro`, `bench`, `review` wedges; **academic v1
  conformance 167 vectors / 24 kinds** (suite `880744c3325c9227…`).
- `provsub` CLI (`approve` is the human's step), dependency-free stdio MCP
  server (verdict-only tools).
- Docs, CITATION.cff, `.zenodo.json`, JOSS paper draft, MIT.
