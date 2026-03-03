# AGENTS.md

## Cursor Cloud specific instructions

### Overview
Splunk Attack Range is a Python CLI tool (`attack_range.py`) that uses Terraform and Ansible to provision instrumented cloud lab environments on AWS, Azure, or GCP for detection engineering. It simulates cyberattacks and forwards telemetry into Splunk.

### Running the CLI
- Entry point: `python3 attack_range.py <action>` (see `--help` for all actions).
- A valid `attack_range.yml` config is required for most commands. The `configure` action is **interactive** (uses `questionary` prompts) and requires a TTY — do not run it non-interactively.
- The default config template is at `configs/attack_range_default.yml`.

### Key dependencies
- **Python 3.10+** (Python 3.12 available in this environment)
- **Terraform 1.9.8** (installed at `/usr/local/bin/terraform`)
- **Ansible** (installed via pip)
- Python packages from `requirements.txt` (installed via `pip3 install -r requirements.txt`)

### Linting / Testing
- This project has **no automated test suite** and **no linter configuration** (no flake8, pylint, mypy, ruff, etc.).
- Basic syntax checking: `python3 -m py_compile attack_range.py` and `python3 -m py_compile modules/<file>.py`.
- The CONTRIBUTING.md mentions pre-commit hooks, but no `.pre-commit-config.yaml` is present.

### Cloud credentials
- All `build`, `destroy`, `show`, `stop`, `resume`, `simulate`, `dump`, and `replay` commands require cloud provider credentials (AWS/Azure/GCP).
- Without credentials, the CLI will load but fail at the cloud API call stage with a region mismatch or authentication error.

### PATH note
- Pip-installed scripts (ansible, ansible-runner, etc.) are in `~/.local/bin`. This is added to PATH in `~/.bashrc`.
