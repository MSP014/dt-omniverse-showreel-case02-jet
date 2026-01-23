# Case 02 Technical Debt

## [PRE-COMMIT] Configuration Misalignment

- **Status:** Resolved (2026-01-23)
- **Severity:** Medium
- **Description:** Current `.pre-commit-config.yaml` deviated from the Estate Standard.
- **Resolution:** Standardised to local hooks (`language: system`), updated versions to v4.5.0, and aligned large-file limits.

## [PIPELINE] Asset Hydration & Bootstrap

- **Status:** Open
- **Severity:** Medium
- **Description:** Per ADR 005, a mechanism is needed to sync heavy assets into the repository structure.
- **Tasks to Resolve:**
  - Create `tools/bootstrap.py` for directory setup and asset downloading.
  - Upload initial asset packs to external storage and document links in README.
