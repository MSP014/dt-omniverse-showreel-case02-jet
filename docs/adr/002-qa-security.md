# ADR 002: QA & Security Protocols

## Status

Accepted

## Context

A Mechanical Digital Twin (Jet Engine) requires rigorous data integrity. Broken telemetry processing or sim-cache ingestion could lead to visual artifacts or pipeline crashes. We must also protect proprietary telemetry schemas.

## Decision

We enforce a strict "Shift Left" strategy using `pre-commit` hooks and automated guardrails:

### 1. Guardrails (Pre-commit)

* **Linting:** `black` (Formatting), `flake8` (Logic), `isort` (Imports).
* **Security:**
  * `bandit`: Scans for common security issues (e.g., hardcoded passwords, unsafe exec).
  * `pip-audit`: Checks `requirements.txt` for known vulnerabilities.
* **Hygiene:** `check-added-large-files` (Max 10MB) to prevent repo bloating.

### 2. Testing

* `pytest` must pass locally before push.
* **Telemetry Validation**: Tests should verify telemetry ingestion scripts and data range clipping (e.g., RPM cannot be negative).
* **Note**: Tests are covered by Linters (Black/Flake8) but excluded from Bandit security scans to avoid false positives related to `assert` usage.

### 3. Secrets Management

* **Isolation**: All sensitive data (credentials, asset server keys) MUST be stored in a `.env` file.
* **Sanity**: The `.env` file MUST be included in `.gitignore`. Never commit secrets to version control.

## Consequences

* **Positive:** Higher code quality, reduced security risk, and blocked accidental large files.
* **Negative:** Initial setup friction; `pip-audit` requires maintenance of `requirements.txt`.
