# Repository Guidelines

## Project Structure & Module Organization
Source modules live under `src/t_robot/`, grouped by domain: control loops in `src/t_robot/controllers/`, hardware drivers in `src/t_robot/hardware/`, and perception helpers in `src/t_robot/perception/`. Shared utilities go in `src/t_robot/common/`. CLI tooling and setup scripts belong in `scripts/`, reusable data files and calibration assets in `assets/`, and documentation drafts in `docs/`. Place integration fixtures in `tests/resources/` so they stay versioned alongside the automated checks.

## Build, Test, and Development Commands
Run `python -m venv .venv` followed by `.venv\Scripts\Activate.ps1` to prepare an isolated environment. Install dependencies with `pip install -e .[dev]` from the repository root. Use `python -m build` to produce distribution artifacts when validating release candidates. Day-to-day validation relies on `pytest -q` for fast test feedback and `pytest --cov=src/t_robot --cov-report=term-missing` before merging any feature branch.

## Coding Style & Naming Conventions
We follow a strict 4-space indentation style, `snake_case` for functions and modules, `PascalCase` for classes, and `UPPER_SNAKE_CASE` for constants. Keep public module names aligned with their directory (e.g., `controllers/path_tracker.py` exposes `PathTracker`). Run `ruff format` to apply formatting and `ruff check src tests` to enforce linting rules; fix import ordering and type hints before opening a review.

## Testing Guidelines
Every behavior change needs a unit test in `tests/unit/` and, when hardware interaction is involved, a simulation guard in `tests/integration/`. Test files follow `test_<feature>.py`, with fixtures centralized in `tests/conftest.py`. Target ≥85% branch coverage, and mock motor or sensor interfaces so tests stay deterministic. When adding asynchronous routines, include timeouts in assertions to avoid hanging suites.

## Commit & Pull Request Guidelines
Use Conventional Commit prefixes (`feat:`, `fix:`, `docs:`, `chore:`) with imperative summaries under 72 characters. Reference tracking issues with `Refs #<id>` in the body and note any calibration data touched. Pull requests must describe the change, list validation commands, and attach screenshots or telemetry snippets when UI dashboards or plots change. Ensure CI passes (`pytest`, `ruff`, `mypy`) before requesting review, and mark breaking protocol updates with a migration checklist.

## Security & Configuration Tips
Never commit `.env.local` or hardware keys; store them in the secrets manager and document required variables in `docs/configuration.md`. Validate new dependencies with `pip audit`, and rotate simulator credentials when sharing logs externally. For field deployments, double-check that safety interlocks remain enabled in default configs before tagging a release.
