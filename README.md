# Case 02: Jet Engine (Aerospace Propulsion Digital Twin)

> [!WARNING]
> **Work in Progress:** This project is currently under active development. Some links and assets may be placeholders.

---

> **Role:** L1 Digital Twin (Mechanical Engineering)
> **Stack:** Houdini (Sim/PDG), Omniverse (USD/Python), Jira Integration

---

## 🎯 Key Technical Workflows

* **Optimized USD Pipelines:** Processing heavy Houdini Pyro/Fluid simulations into lightweight USD payloads for real-time Omniverse playback.
* **Data-Driven Digital Twin:** Python-based generation of realistic sensor streams (RPM, EGT, Vibration) linked to flight regimes (Idle, Takeoff, Cruise).
* **Complex Assembly Management:** Leveraging USD Variants and Payloads to structure massive mechanical assemblies (10k+ parts).

## 👁️ Visual Proof

> *Placeholders for future GIFs - Replace with actual optimised media*

1. **Engine Idle State:** `![Idle Demo](docs/img/idle_demo.gif)`
2. **Telemetry Dashboard:** `![FUI Demo](docs/img/fui_demo.gif)`
3. **Pipeline Flow:** `![Data Flow](docs/img/pipeline_diagram.png)`

## 🏗️ Engineering Trace

Systematic documentation of architectural choices, naming conventions, and security protocols used to build this Digital Twin showcase.

* [**Read our Engineering Decisions (ADRs)**](docs/adr/) for deep dives into Naming, Security, and Architecture.

## 📂 Repository Structure

```text
.
├── docs/        # ADRs and knowledge base
├── plans/       # Implementation plans & tech debt
├── src/         # Core logic and scripts
├── tests/       # Validation and testing suite
└── tools/       # Internal pipeline utilities
```

---

## 💾 Project Data / Assets

To keep this repository lightweight (GitHub < 1GB), heavy binary assets are stored externally.

* [**Download Heavy Assets (One Drive / S3 Link TBD)**](https://example.com/placeholder)
  * Includes: `*.usd` crates, `*.hip` source files, and high-res textures.

## 🛠️ Setup & Installation

1. **Clone:** `git clone https://github.com/MSP014/dt-omniverse-showreel-case02-jet.git`
2. **Env:** Create conda env: `conda create -n case02-env python=3.10`
3. **Deps:** `pip install -r requirements.txt`
4. **Hooks:** `pre-commit install`

---

## 📜 Changelog

* **2026-01-22:** Initial repository bootstrap. Established "Gold Standard" structure (ADRs, Pre-commit, Hybrid Access).
