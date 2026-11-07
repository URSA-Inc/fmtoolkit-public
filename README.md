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

## Classes defined in other files

For a changed Python file, the workflow also sends the files of your
repository that define the base classes of its classes (every base of every
ancestor) and the classes their fields are annotated with, at both commits,
so FMToolkit can analyze those classes. It follows the file's imports
(including relative imports and re-exports through a package's
`__init__.py`) and finds modules from the repository root or `src/`; a module
it can't find there is a library and isn't sent. At most 20 files and 1 MB
are sent per changed file.
