# python-boilerplate

Minimal Python project boilerplate with a small example program, tests, and a Makefile-driven developer workflow.

## What’s included (based on the current source code)

- Example CLI app using `argparse` and `logzero` logging
  - Source: [`src/hello.py`](src/hello.py)
- Basic unit test and coverage runner
  - Source: [`tests/test_hello.py`](tests/test_hello.py) and `make test` in the [`Makefile`](Makefile)
- Optional linting/style/type-check targets (they auto-skip if the tool is not installed)
  - Source: [`Makefile`](Makefile) + pinned tools in [`requirements.txt`](requirements.txt)
- Placeholder web resources (HTML/CSS/JS)
  - Source: [`resources/`](resources)

CI configuration exists for GitHub Actions and Travis (see [`.github/workflows/pythonapp.yml`](.github/workflows/pythonapp.yml) and [`.travis.yml`](.travis.yml)). Whether all badges/services are currently active depends on external configuration.

## Quick start

### Prerequisites

- Python 3
  - CI currently configures Python **3.7** (see [`.github/workflows/pythonapp.yml`](.github/workflows/pythonapp.yml))
- `pip` / `pip3` (to install from `requirements.txt`)
- Optional: `make` (to use the Makefile convenience targets)

### 1) Install dependencies

This repository uses `requirements.txt`:

```bash
python3 -m pip install -r requirements.txt
```

### 2) Run the example program

The program lives in `src/hello.py` and defines one required positional argument (`arg`) plus a few optional flags:

```bash
python3 src/hello.py test
python3 src/hello.py -f -n Foo -vv test
python3 src/hello.py --version

# equivalent module-style invocation
python3 -m src.hello test
```

What it does (today): it prints `"Hello world!"` (via `Greeter().print_message()`) and logs the parsed arguments (see `main()` in [`src/hello.py`](src/hello.py)).

## Common developer commands

The Makefile is the “source of truth” for the available `make` targets.

```bash
make            # same as: make help
make run
make test
make lint
```

For a full command reference and prerequisites, see:

- [`docs/COMMANDS.md`](docs/COMMANDS.md)

## Project structure

- `src/` — example application code (a Python package)
- `tests/` — unit tests
- `resources/` — placeholder HTML/CSS/JS assets

Details: [`docs/PROJECT_STRUCTURE.md`](docs/PROJECT_STRUCTURE.md)

## Verification

Documentation in this repository was reviewed against the exact Git commit recorded in [`docs/VERIFICATION.md`](docs/VERIFICATION.md), with notes on what could/couldn’t be executed in the review environment.

If you want to see what was identified as outdated/incorrect (and what was added), see [`docs/DOCUMENTATION_AUDIT.md`](docs/DOCUMENTATION_AUDIT.md).

## Documentation refresh / progress (what was fixed and added)

This repository’s documentation was refreshed by inspecting the implementation and validating commands where possible.

### Fixes to existing docs

- Updated `README.md` so it matches the current code and Makefile targets.
- Corrected stale/incorrect wording about the lint toolchain (the Makefile uses `pylint`, not “pyline”, and defines additional targets).

### New docs added

- [`docs/COMMANDS.md`](docs/COMMANDS.md): accurate Makefile target reference (including prerequisites and platform notes)
- [`docs/PROJECT_STRUCTURE.md`](docs/PROJECT_STRUCTURE.md): repository layout explained with links to real source files
- [`docs/VERIFICATION.md`](docs/VERIFICATION.md): exact code commit reviewed + what was executed successfully + limitations
- [`docs/DOCUMENTATION_AUDIT.md`](docs/DOCUMENTATION_AUDIT.md): items found outdated/incorrect/missing, with pointers to the implementation

### Verified commands (summary)

See [`docs/VERIFICATION.md`](docs/VERIFICATION.md) for the authoritative list, but in brief:

- `make` / `make help` ✅
- After installing `python3.12-venv`: `make deps-install`, `make run`, `make test`, `make code-style` ✅
- `make code-lint` ⚠️ fails on Python 3.12 because the repo pins `pylint==2.7.2` (not compatible with Python 3.12)

### References for independent verification

The documentation refresh was prepared against the upstream repository state at:

- Code commit: `9128f4da19da25968f3c5ea2576342a7fe516ff9`

If you publish this repository as a new GitHub repo, keep the docs in sync with the commit you actually publish (or update the commit reference in `docs/VERIFICATION.md`).

## Attribution

This project is based on the upstream repository:

- https://github.com/AlexanderWillner/python-boilerplate

## License

Apache 2.0 — see [`LICENSE`](LICENSE).
