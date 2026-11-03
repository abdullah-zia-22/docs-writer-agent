# Project structure

This document describes the repository layout **as implemented in the current source code**.

For the exact commit used for this review, see [`VERIFICATION.md`](VERIFICATION.md).

## Top level

| Path | Purpose |
|------|---------|
| `README.md` | Project overview and quick start. |
| `Makefile` | Developer commands (`make help`, `make test`, linters, etc.). |
| `requirements.txt` | Pinned Python dependencies and tooling versions. |
| `src/` | Example application code (a Python package). |
| `tests/` | Unit tests. |
| `resources/` | Placeholder front-end assets (HTML/CSS/JS). |
| `.github/workflows/` | GitHub Actions CI workflows. |
| `.travis.yml` | Travis CI configuration (if enabled in the hosting service). |
| `.coveragerc` | Coverage configuration used by `make test`. |

## `src/` (application code)

| Path | Notes |
|------|------|
| `src/__init__.py` | Marks `src` as a Python package. |
| `src/hello.py` | The example CLI program. Defines `Greeter`, a `log` decorator, and a `main()` function. |

### CLI entry point

The CLI behavior is implemented under the `if __name__ == "__main__":` block in:

- [`src/hello.py`](../src/hello.py)

It defines:

- a required positional argument: `arg`
- options: `-f/--flag`, `-n/--name`, `-v/--verbose` (counter), `--version`

## `tests/`

| Path | Notes |
|------|------|
| `tests/__init__.py` | Marks `tests` as a Python package. |
| `tests/test_hello.py` | A basic `unittest` test case that exercises `Greeter.set_message()` and calls `main(...)`. |

Test execution is wired through the Makefile target:

- `make test` → `coverage run --source . -m tests.test_hello` (see [`Makefile`](../Makefile))

## `resources/`

| Path | Notes |
|------|------|
| `resources/gui.html` | Minimal HTML skeleton. |
| `resources/styles.css` | Minimal CSS stub. |
| `resources/scripts.js` | Empty (0 bytes). |

No Python code references `resources/` today; these files appear to be placeholders for future expansion.

