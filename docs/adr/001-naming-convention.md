# ADR 001: Naming Convention

## Status

Accepted

## Context

Inconsistent naming across files and repositories leads to pipeline friction and "where is that file?" fatigue. We need a standardized grammar for Case 02.

## Decision

We will enforce the following naming rules:

### 1. Repository Naming

Format: `dt-omniverse-showreel-case##-[key]`

* Example: `dt-omniverse-showreel-case02-jet` (this repo)
* **dt**: Digital Twin
* **omniverse**: Platform
* **showreel**: Project type
* **case02**: Sequence ID
* **jet**: Project Key (Jet Engine)

### 2. File Layers (Snake Case)

* `mesh_*` (Geometry)
* `mat_*` (Materials)
* `light_*` (Lighting setups)
* `sim_*` (Simulation caches)

### 3. USD Suffixes

* `.usda`: ASCII (Human readable, git-friendly). Use for composition arcs and root layers.
* `.usdc`: Binary (Performance). Use for heavy geometry/caches. **GITIGNORE this extension.**

## Consequences

* **Positive:** Predictable file system, clear separation of binary vs text data.
* **Negative:** Requires discipline to rename existing assets during import.
