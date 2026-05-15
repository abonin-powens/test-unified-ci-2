# test-unified-ci-2 (downstream)

Minimal POC: triggered by `test-unified-ci-1`'s dispatch, echoes the
upstream version from the payload, bumps its own version, commits, tags.

## Files

- `version.py` — two constants: `VERSION` (this repo) and `repo_a_version`
  (pinned upstream, mirrors a dependency declaration)
- `.github/workflows/tag-and-deploy.yml` — runs on `repository_dispatch`
  (`upstream-release`) or `workflow_dispatch`

## Pipeline steps

1. Read upstream version from `client_payload.version` (or manual input),
   strip optional leading `v`.
2. Echo it.
3. Patch-bump `VERSION` in `version.py`.
4. Overwrite `repo_a_version` in `version.py` with the upstream version.
5. Commit + tag `vX.Y.Z` + push.

## Manual run (no upstream needed)

Actions → "Tag and Deploy" → Run workflow → supply any `vX.Y.Z`.
