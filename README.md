# fmtoolkit-public

Public CI artifacts for integrating FMToolkit into your GitHub Actions pipeline.

- **`.github/workflows/fmtoolkit-ci-reusable.yml`** — the reusable workflow
  that does the actual work: diffs changed files in a pull request, calls
  the FMToolkit REST API for each one, and posts a summary check.
- **`fmtoolkit-ci.yml`** — the file you copy into your own repository at
  `.github/workflows/fmtoolkit-ci.yml`. It's a thin wrapper that calls the
  reusable workflow above.

## Installing FMToolkit in your repo

1. Add your FMToolkit API key as a repository secret named `FMTOOLKIT_API_KEY`
   (Settings → Secrets and variables → Actions).
2. Copy `fmtoolkit-ci.yml` from this repo into your own repository at
   `.github/workflows/fmtoolkit-ci.yml`.
3. Commit and push. FMToolkit will run on your next pull request.

Edit the `file_patterns` and `on_*` policy fields in your copy of
`fmtoolkit-ci.yml` to match your codebase and desired strictness.
# test line, should never actually land on main
