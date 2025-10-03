# Repository Guidelines

## Project Structure & Module Organization
- Runtime modules stay in `src/t_robot/`: use `controllers/`, `hardware/`, and `perception/` for domain logic, and share helpers from `common/`.
- House CLI helpers in `scripts/`, reusable datasets in `assets/`, and documentation drafts in `docs/`.
- Keep tests under `tests/`, splitting fast suites into `tests/unit/`, hardware simulations into `tests/integration/`, and fixtures under `tests/resources/`.
- Export public symbols that mirror file paths (e.g., `controllers/path_tracker.py` exposes `PathTracker`) to keep imports predictable.

## Build, Test, and Development Commands
- `python -m venv .venv` then `.venv\\Scripts\\Activate.ps1` sets up the Windows virtual environment.
- `pip install -e .[dev]` installs runtime and dev dependencies in editable mode.
- `pytest -q` runs the quick suite; `pytest --cov=src/t_robot --cov-report=term-missing` highlights coverage gaps before merging.
- `python -m build` produces release artifacts when preparing a distribution.

## Coding Style & Naming Conventions
- Use 4-space indentation, `snake_case` for modules and functions, `PascalCase` for classes, and `UPPER_SNAKE_CASE` constants.
- Apply `ruff format` and enforce rules with `ruff check src tests` to keep imports, types, and style consistent.
- Name modules after their directory responsibilities so the public API stays predictable.

## Testing Guidelines
- Add unit coverage for each change in `tests/unit/` and guard hardware-facing flows with simulations in `tests/integration/`.
- Name tests `test_<feature>.py`, centralize fixtures in `tests/conftest.py`, and aim for ≥85% branch coverage.
- Mock motor and sensor interfaces and add timeouts around async assertions to keep runs deterministic.

## Commit & Pull Request Guidelines
- Follow Conventional Commits (`feat:`, `fix:`, etc.) with imperative summaries under 72 characters and add `Refs #<id>` for linked work.
- Capture calibration-data touch points in commit bodies for deployment traceability.
- PRs should outline the change, list validation commands (e.g., `pytest`, `ruff`, `mypy`), and include telemetry or screenshots when relevant.
- Verify CI is green before requesting review and add a migration checklist whenever protocols or interfaces change.

## Security & Configuration Tips
- Keep secrets out of version control; document required variables in `docs/configuration.md` and rely on the secret manager.
- Run `pip audit` after dependency updates and rotate simulator credentials before sharing external logs.
- Confirm safety interlocks stay enabled ahead of field deployments and release tagging.
