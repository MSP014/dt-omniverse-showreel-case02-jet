# Jet Engine Digital Twin (Case 02) — Knowledge Base Index

 Welcome to the central Knowledge Base for the **Trent 1000 Jet Engine Digital Twin** project. This directory contains all foundational concepts, engineering specifications, and architectural documentation necessary to implement the real-time Omniverse application.

 ---

## 📂 Core Concepts & Architecture

 | Document | Description |
 | :--- | :--- |
 | [**Main Concept**](main_concept.md) | The definitive guide to the project. Covers the Operational States, Visual Modes (Thermal/Velocity), LOD strategies, and the strict semantic contracts that guide the application engineering. |
 | [**Digital Twin Maturity Levels**](digital_twin_maturity_levels.md) | Theoretical framework contextualizing this project within the broader spectrum of Digital Twin evolution (from static models to autonomous, AI-driven systems). |
 | [**USD Architecture: Contract**](usd_architecture/00_project_usd_contract.md) | The definitive naming conventions, units, and structural principles for the USD scene graph assembly. |
 | [**USD Architecture: Payloads & References**](usd_architecture/01_payloads_references_assembly.md) | Documentation on how to compose the heavy engine geometry without breaking viewport performance, defining the boundaries for Close-Up Payload loading. |
 | [**USD Architecture: Instancing & Radial Geometry**](usd_architecture/02_instancing_radial_geometry.md) | Strategies for efficiently instancing repeating radial components (like compressor/turbine blades) using PointInstancers to drastically reduce the prim count. |
 | [**USD Architecture: Houdini Sim Caches & States**](usd_architecture/03_houdini_sim_caches_and_states.md) | The technical layout of the 4-state simulation matrix, covering how `OperationalState` and `VisualMode` VariantSets are wired to VDB grids and BasisCurves. |
 | [**USD Architecture: Custom Attributes & Telemetry**](usd_architecture/04_custom_attributes_telemetry.md) | Technical specs on how to embed schema parameters (like target temperatures or component metadata) directly into USD prims for the Data Provider to bind to. |

## ⚙️ Engineering & Physics Reference

 | Document | Description |
 | :--- | :--- |
 | [**Engine Technical Specifications**](Trent%201000%20-%20Engine%20Technical%20Specifications.md) | Baseline physical data for the Trent 1000 turbofan (dimensions, thrust, spool RPM ranges). |
 | [**Testbed 80 Facility Details**](Testbed_80_Facility_Details.md) | Scale and technical capabilities of the Rolls-Royce indoor testing facility, providing the narrative and physical context for our simulation environment. |
 | [**FUI and HUD Data Mapping**](FUI%20and%20HUD.txt) | Raw schema definitions for the telemetry values exposed to the UI (N1/N2/N3 RPM, EGT, Fuel Flow, etc.). |

## 💬 Transcripts & Research Logs

 | Directory | Description |
 | :--- | :--- |
 | [`transcripts/`](transcripts/) | Raw transcripts and research logs from subject matter experts, used to inform the documentation in this root folder. |

 > **Note for Developers & Artists:** Always ensure that any updates to the simulation matrix or the Telemetry Data Provider schema `[in Python]` remain perfectly synchronized with the contracts laid out in the `main_concept.md` document. No dual-encoding of visual states!
