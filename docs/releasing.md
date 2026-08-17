# Releasing

A release is a tag. Everything else is automatic — after a one-time setup that
only the repository owner can do, because it binds identities.

## Cutting a release

```bash
# 1. bump the version in BOTH places (the workflow refuses if they disagree)
#    pyproject.toml   -> version = "0.1.0"
#    CITATION.cff     -> version: 0.1.0   and date-released
# 2. commit, tag, push
git commit -am "release: 0.1.0"
git tag v0.1.0
git push && git push --tags
```

`.github/workflows/release.yml` then: verifies tag == versions; runs ruff,
pytest, both conformance suites `--strict`, and `--check`; builds sdist +
wheel and asserts both vector suites are inside the wheel; publishes to PyPI
via Trusted Publishing; creates the GitHub Release with `dist/*` and
`SHA256SUMS` attached. Zenodo archives the release and mints a DOI.

## One-time setup (owner)

### PyPI — Trusted Publishing (no API token, ever)

1. Log in to https://pypi.org, go to **Your projects → Publishing** (or, for
   the first release, **Add a new pending publisher** at
   https://pypi.org/manage/account/publishing/).
2. Fill in exactly:
   - PyPI project name: `provenance-substrate`
   - Owner: `isaacsight`
   - Repository name: `provenance-substrate`
   - Workflow name: `release.yml`
   - Environment name: `pypi`
3. On GitHub: **Settings → Environments → New environment** named `pypi`.
   Optionally add yourself as a required reviewer — then every publish waits
   for one click from you, which is the human gate this whole project is
   about.

That is all. The workflow requests a short-lived OIDC token from GitHub;
PyPI checks it against the publisher you registered. Nothing to rotate,
nothing to leak.

### Zenodo — DOI per release

1. Log in to https://zenodo.org with GitHub.
2. https://zenodo.org/account/settings/github/ → flip **provenance-substrate**
   on.
3. Metadata comes from `.zenodo.json` (title, creators, license, keywords,
   related identifiers). The first published GitHub Release after the toggle
   mints a concept DOI (all versions) and a version DOI.
4. Paste the concept DOI badge into README.md and the `doi:` field into
   CITATION.cff on the next release.

### JOSS

`paper/paper.md` needs your ORCID (currently a placeholder). Submit at
https://joss.theoj.org/papers/new with the repository URL and the Zenodo
archive DOI when asked; JOSS wants the archived version to match the tagged
release.

## Re-running a release

`workflow_dispatch` with an existing tag re-runs verify/build/publish; PyPI
refuses to overwrite an existing version (as it should), so a re-run only
makes sense to re-attach artifacts to the GitHub Release. To ship a fix, bump
the version and cut a new tag.
