# Commands (Makefile)

This project uses a `Makefile` to provide a few common development commands.

**Source of truth:** [`Makefile`](../Makefile)

## Quick reference

Run:

```bash
make help
```

In this repository, `make` defaults to the `help` target, so `make` and `make help` are equivalent.

### `make help` output (verified)

The following list is the exact output from running `make` in the repository at the commit referenced in [`VERIFICATION.md`](VERIFICATION.md):

```text
auto-style                Style the code
clean                     Cleanup
code-count                Count the lines of code
code-lint                 Lint the code
code-style                Test the code style
css-lint                  Lint the CSS code
deps-create               Create the dependencies
deps-install              Install the dependencies
deps-update               Update the dependencies
doc                       Document the code
feedback                  Provide feedback
help                      Print help for each target
html-lint                 Lint the HTML code
js-lint                   Lint the JavaScript code
lint                      Run all linters
run                       Run the code
test                      Test the code
```

## Target details

### Run

```bash
make run
```

Runs:

- `python3 src/hello.py -f -n Foo test`

See [`src/hello.py`](../src/hello.py) for CLI flags and behavior.

### Tests + coverage

```bash
make test
```

Runs `coverage` against the `tests.test_hello` module:

- `coverage run --source . -m tests.test_hello`
- `coverage report`

Relevant files:

- Test module: [`tests/test_hello.py`](../tests/test_hello.py)
- Coverage configuration: [`.coveragerc`](../.coveragerc)

### Documentation

```bash
make doc
```

Runs `pydoc3 src`.

### Cleanup

```bash
make clean
```

Removes `*.pyc` and `__pycache__/` directories under `src/` and `tests/`.

### Linting / style / typing

```bash
make code-style
make code-lint
make lint
```

Notes (based on the Makefile implementation):

- Each sub-tool is optional. If a tool is missing, the Makefile prints `SKIPPED` and continues.
- `make lint` runs **all** linters: Python + CSS + JavaScript + HTML.

Tools invoked by targets:

- `code-style`: `pycodestyle`
- `code-lint`: `pyflakes`, `pylint`, `flake8`, `pyright`, `mypy`
- `css-lint`: `csslint` (npm)
- `js-lint`: `jslint` (npm)
- `html-lint`: `tidy` (commonly installed via system package managers)

Pinned Python tool versions live in [`requirements.txt`](../requirements.txt).

Compatibility note:

- The repository currently pins `pylint==2.7.2`. This version does **not** run on Python 3.12 (it fails importing `inspect.formatargspec`, which was removed in Python 3.12).
  - CI currently configures Python **3.7** (see [`.github/workflows/pythonapp.yml`](../.github/workflows/pythonapp.yml)).
  - If you are using Python 3.12 locally and want `make code-lint` to work, you will need either an older Python version or updated lint tool versions.

### Dependencies

```bash
make deps-install
make deps-update
make deps-create
```

- `deps-install` installs from `requirements.txt` via `pip3`.
- `deps-update` uses `pur` (if installed) to update pinned versions in `requirements.txt`.
- `deps-create` uses `pipreqs` (if installed) to regenerate `requirements.txt` based on imports.

### Feedback

```bash
make feedback
```

Opens the GitHub issues page using the `open` command:

- `open https://github.com/AlexanderWillner/python-boilerplate/issues`

`open` is macOS-specific. On Linux, you may want to use `xdg-open <url>`; on Windows, `start <url>`.

