# Verification notes

This documentation update was prepared by reviewing the repository source code and (where possible) running the repository’s own helper commands.

## Commit

All statements in the updated documentation are intended to match the repository at:

- Commit: `9128f4da19da25968f3c5ea2576342a7fe516ff9`

To reproduce:

```bash
git clone https://github.com/AlexanderWillner/python-boilerplate
cd python-boilerplate
git checkout 9128f4da19da25968f3c5ea2576342a7fe516ff9
```

## What was verified by execution

In the review environment the following was executed successfully:

- `make` / `make help` output (used to document available Make targets)

Tool versions in the review environment:

- Python: `Python 3.12.3`
- Make: `GNU Make 4.3`

## Updated verification (after installing `python3.12-venv`)

After installing the system package `python3.12-venv`, a local virtual environment could be created and dependencies could be installed.

The following commands were then verified successfully:

- `python3 -m venv .venv`
- `pip install -r requirements.txt`
- `make deps-install`
- `make run`
- `make test`
- `make code-style`

### Notes / limitations observed during execution

- `make code-lint` failed under **Python 3.12** due to the pinned `pylint==2.7.2` / `wrapt` dependency using `inspect.formatargspec`, which was removed in Python 3.12.
  - This is a **tooling compatibility** issue; it is not caused by the application code in `src/`.
  - CI currently configures Python **3.7** (see [`.github/workflows/pythonapp.yml`](../.github/workflows/pythonapp.yml)), where this pinned pylint version is expected to work.

- `make test` uses `coverage run --source . ...`. If you create a `.venv/` directory inside the repository root, coverage may include third-party packages from `.venv/` in the report.
  - Workaround when running locally: create your virtualenv outside the repo, or adjust coverage configuration (not changed as part of this documentation-only update).

## How to reproduce locally on Ubuntu/Debian

To run and verify these targets locally, you typically need:

```bash
sudo apt-get update
sudo apt-get install -y python3-pip python3-venv
python3 -m venv .venv
. .venv/bin/activate
pip install -r requirements.txt
make test
```

