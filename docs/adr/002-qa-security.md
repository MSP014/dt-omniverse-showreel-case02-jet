# ADR 002: QA & Security Protocols

## Status

Accepted

## Context

"Works on my machine" is not an acceptable delivery standard. We deal with complex pipelines where a single broken script can stop a render farm. We also need to prevent credential leaks.

## Decision

We enforce a strict "Shift Left" strategy using `pre-commit` hooks:

### 1. Guardrails (Pre-commit)

* **Linting:** `black` (Formatting), `flake8` (Logic), `isort` (Imports).
* **Security:**
  * `bandit`: Scans for common security issues (e.g., hardcoded passwords, unsafe exec).
  * `pip-audit`: Checks `requirements.txt` for known vulnerabilities.
* **Hygiene:** `check-added-large-files` (Max 10MB) to prevent repo bloating.

### 2. Testing

* `pytest` must pass locally before push.
* Tests should mock external dependencies (Omniverse/Houdini APIs) where possible to run fast.

## Consequences

* **Positive:** Higher code quality, reduced security risk, blocked accidental large files.
* **Negative:** Initial setup friction; `pip-audit` requires maintenance of `requirements.txt`.
