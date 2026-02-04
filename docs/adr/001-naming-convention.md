# ADR 001: Naming Convention & Standards

## Status

Accepted

## Context

Managing a Mechanical Digital Twin (Jet Engine) requires precise identification of thousands of mechanical parts and telemetry streams. We need a standardised grammar to ensure integration between Houdini simulation caches and Omniverse composition remains robust.

## Decision

We will enforce the following naming and operational rules:

### 1. Repository Naming

Format: `dt-omniverse-showreel-case##-[key]`

* **Example:** `dt-openusd-showcase-case02-jet` (this repo)
* **dt**: Digital Twin
* **omniverse**: Platform
* **showreel**: Project type
* **case02**: Sequence ID
* **jet**: Project Key (Jet Engine)

### 2. File Layers (Snake Case)

* `mesh_*` (Geometry, e.g., `mesh_turbine_blade`)
* `mat_*` (Materials / MDL)
* `light_*` (Lighting setups)
* `sim_*` (Simulation caches / Telemetry, e.g., `sim_thermal_flow`)

### 3. USD Suffixes

* `.usda`: ASCII (Human-readable, git-friendly). Use for composition arcs and root layers.
* `.usdc`: Binary (Performance). Use for heavy geometry and high-frequency caches. **GITIGNORE this extension.**

### 4. Language Standards

* **Documentation**: All technical documentation and comments MUST be in **British English** (en-GB). Use `s` instead of `z` (e.g., *optimise*, *standardise*).
* **Commit Messages**: British English, imperative mood (e.g., "Add feature", not "Added feature").

### 5. Git Workflow

* **Branches**: `feature/description-of-change` or `fix/issue-id`.
* **Tags**: Use semantic versioning for milestones (e.g., `v1.0.0-gold`).

## Consequences

* **Positive:** Predictable file system, clear separation of binary vs text data, and consistent international documentation code.
* **Negative:** Requires initial setup discipline and cognitive load for suffix management.
