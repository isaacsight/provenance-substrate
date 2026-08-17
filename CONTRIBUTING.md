# Contributing

The vectors are the standard, not the prose. Two rules follow from that.

1. **A change that alters any `expected` in `src/provsubstrate/conformance/vectors_academic_v1/` is a semantic change.** Regenerate with `python -m provsubstrate.conformance.generate`, explain in the commit why the reference behaviour changed, and bump the suite (a new `format_version` directory if the change is not backward-compatible). `provsub conformance --check` must pass in CI. Never edit a vector by hand.
2. **`vectors_finance_v1/` is vendored from `@kernel.chat/kbot-finance` and is never edited here.** If the Python port disagrees with a finance vector, the port is wrong.

Everything else: no runtime dependencies, nothing reads a clock or a random source on its own (timestamps and seeds are parameters), no emojis, `ruff check src tests` clean, `pytest -q` green, Python ≥ 3.10.

Ports to other languages are the most valuable contribution there is. Implement the kinds you claim, run the vectors, quote the suite hash, open an issue titled "conformance: <language> <kinds>" and we will link it from the README.
