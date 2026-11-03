# Documentation audit notes

This file records documentation gaps and potential sources of confusion found during the review, with pointers to the relevant implementation.

## Items that were outdated / incorrect in the previous README

- **Makefile command list mismatch**
  - The old README showed a shortened command list that did not match the actual `make help` output.
  - Source of truth: [`Makefile`](../Makefile)

- **Tool name typo: “pyline”**
  - The old README referenced “pyline”, but the Makefile uses `pylint` (and also calls `pyright` and `mypy`).
  - Source: `code-lint` target in [`Makefile`](../Makefile)

- **Missing Make targets**
  - The Makefile also defines `lint`, `auto-style`, CSS/JS/HTML lint targets, and dependency maintenance targets (`deps-create`).
  - Source: [`Makefile`](../Makefile)

## Potentially confusing / environment-dependent behavior

- **`make feedback` is macOS-specific by default**
  - It uses `open <url>`, which works on macOS but not on many Linux/Windows setups.
  - Source: `feedback` target in [`Makefile`](../Makefile)

- **CI test runner uses `pytest` but tests are `unittest`**
  - GitHub Actions installs and runs `pytest`, which can execute `unittest` tests.
  - Source: GitHub Actions workflow: [`.github/workflows/pythonapp.yml`](../.github/workflows/pythonapp.yml)
  - Test code: [`tests/test_hello.py`](../tests/test_hello.py)

- **`main()` type annotation vs how it’s called**
  - `main()` is annotated as `main(args: argparse.Namespace)`, but `tests/test_hello.py` calls it with `sys.argv[1:]` (a list).
  - This works today because `main()` only logs `args` and does not access `Namespace` fields.
  - Source: [`src/hello.py`](../src/hello.py), [`tests/test_hello.py`](../tests/test_hello.py)

- **Pinned lint toolchain is not compatible with newer Python versions**
  - With Python 3.12, `pylint==2.7.2` fails at import time because it depends on `inspect.formatargspec` (removed in Python 3.12).
  - Source: `requirements.txt` pin + `code-lint` target in [`Makefile`](../Makefile)
  - See also: [`docs/VERIFICATION.md`](VERIFICATION.md)

- **Coverage report may include `.venv/`**
  - `make test` runs `coverage ... --source .`, so if your virtualenv lives in the repo root, coverage can include third-party files under `.venv/`.
  - Source: `test` target in [`Makefile`](../Makefile)

## Missing documentation now covered by the new docs

- Project structure and file purpose: [`docs/PROJECT_STRUCTURE.md`](PROJECT_STRUCTURE.md)
- Make target reference and prerequisites: [`docs/COMMANDS.md`](COMMANDS.md)
- Reproducible commit reference + execution limitations: [`docs/VERIFICATION.md`](VERIFICATION.md)

