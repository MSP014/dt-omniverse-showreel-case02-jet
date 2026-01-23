# ADR 005: Asset Life Cycle & Hydration

## Status

Proposed

## Context

The Jet Engine Digital Twin (Case 02) generates massive Pyro/Fluid simulation caches and complex mechanical assemblies. Storing these in Git is prohibited by the Estate Standard. We need a strategy to link the logic in Git with the heavy data in external storage.

## Decision

We will implement a **Hydration Protocol** to reconstruct the operational environment:

1. **External Storage**: All non-textual assets (simulation caches, binary USDs, textures) will be hosted on high-availability external storage.
2. **Directory Mapping**: The external archive structure must mirror the local directory skeleton (`/assets`, `/geo`, `/cache`, `/HIP`).
3. **Relative Path Integrity**: Every USD reference and Python script path MUST use relative paths. Absolute paths (e.g., `C:/Users/...`) are strictly forbidden to ensure machine-agnostic portability.
4. **Automatic Provisioning (Future)**: A `bootstrap.py` utility in `/tools` will be developed to automate directory creation and asset synchronisation.

## Consequences

* **Positive**: Fast repository cloning, professional handling of heavy binary data, and guaranteed portability for the showreel presentation.
* **Negative**: Requires an additional manual or scripted "hydration" step after cloning.
