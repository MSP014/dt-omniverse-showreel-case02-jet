# Case 02: Jet Engine Digital Twin (L1) — Implementation Plan

**Jira Project**: JET
**Status**: In Progress
**Last Updated**: 2026-01-31

---

## 🧩 EPIC: Research & Pre-production (JET-1)

### ✅ [JET-10] Explore CAD models

**Status**: ✅ Done
**Objective**: Research available CAD models of Rolls-Royce Trent 1000 and evaluate feasibility for retopology.

### ✅ [JET-12] Create Master Reference Board

**Status**: ✅ Done
**Objective**: Compile visual references from factory tours, technical documentation, and operational footage.

### ⏸️ [JET-16] Define Parameters & Create Data CSV

**Status**: Partially Complete (Deferred)
**Objective**: Define engine telemetry parameters and generate CSV data for Digital Twin simulation.

**Decomposition:**

#### ✅ [JET-22] Define Trent 1000 Testbed FUI Parameters

**Status**: ✅ Done
**Objective**: Research and document key parameters for FUI (Heads-Up Display) and Testbed 80 specifications.
**Deliverables**:

- `docs/knowledge_base/FUI and HUD.txt` (display parameters, warning thresholds)
- `docs/knowledge_base/Testbed 80 - Technical Specifications and Facility Details.txt` (facility specs)

#### ⏸️ [JET-23] Create Data CSV with Trent 1000 Testbed Parameters

**Status**: To Do (Deferred)
**Objective**: Generate synthetic CSV file with realistic telemetry data based on parameters defined in JET-22.
**Depends on**: JET-21 (USD Export), JET-28 (Test Stand Rig) — CSV generation deferred until rigged assets are available in USD.

**Definition of Done:**

- Python script `tools/generate_telemetry.py` creates CSV with columns: timestamp, RPM (LP/IP/HP), EGT, Fuel_Flow_kg_s, Thrust_kN, engine_mode (idle/takeoff/cruise/max).
- Data includes realistic sensor noise and physical correlations (e.g., high RPM correlates with high EGT).
- Parameters sourced from Flightradar24 transcript (13,617 RPM HP, 1,500°C EGT, 10:1 bypass ratio).
- CSV can be imported into Omniverse Python script to drive animations.

### ✅ [JET-31] Setup Repository & Migration to Gold Standard

**Status**: ✅ Done
**Objective**: Initialise GitHub repository, configure pre-commit hooks, establish NVIDIA Showreel Standard compliance.

### ✅ [JET-32] Collect & Document Trent 1000 Factory Tour References

**Status**: ✅ Done
**Objective**: Collect 61 high-resolution reference screenshots from 'How Rolls-Royce Jet Engines Are Built' video (Flightradar24, 2026-01-30). Video transcript with technical specifications saved to `docs/knowledge_base/`.

**Logged**: 45m

---

## 🧩 EPIC: Hero Asset: Jet Engine (JET-3)

**Status**: 🔄 In Progress

### 🔄 [JET-17] Retopologize Trent 1000 Core

**Status**: 🔄 In Progress
**Estimate**: 6h
**Objective**: Create a clean, optimised (mid-poly) polygon mesh based on the "dirty" high-poly .STL model. This is critical for UV unwrapping and real-time performance in Omniverse.

**Definition of Done:**

- Clean quad topology with edge flow following mechanical forms.
- Polygon count appropriate for real-time rendering (~100k-200k tris).
- Comparison renders (high-poly vs retopo) show no visual degradation.

### 🔄 [JET-18] Create Procedural Cables & Pipes

**Status**: 🔄 In Progress
**Estimate**: 6h
**Objective**: Develop a procedurally generated system for the external 'dress kit' (cables, pipes, harnesses). Based on Flightradar24 refs: hydraulic lines, electrical harnesses, protective conduits, bleed air ducting. This demonstrates core procedural modelling skills and faithfully represents the 'heavy metal' aesthetic.

**Definition of Done:**

- Houdini HDA or script generates dress kit based on engine surface sampling.
- Cables follow realistic routing (avoiding collision, respecting mounting points).
- Variety in cable diameter, colour coding, protective sleeving.

### 🔄 [JET-19] UV Unwrapping & Map Baking

**Status**: 🔄 In Progress
**Estimate**: 6h
**Objective**: Create clean UVs for all retopologised components. Bake utility maps (Normal, AO, Curvature) from the high-poly .STL source mesh to the new, clean mesh.

**Definition of Done:**

- UV islands optimised for texture resolution (critical parts get more space).
- Baked maps (2K-4K) show no artefacts (seams, projection errors).
- Test render in Substance Painter shows clean normal map application.

### 🔄 [JET-20] Texturing & Material Creation

**Status**: 🔄 In Progress
**Estimate**: 6h
**Objective**: Author photorealistic PBR materials for all engine components: titanium alloys (fan blades), nickel-based superalloys (turbine stages), painted steel (casings), carbon composites (nacelle parts). Use Substance Designer/Painter or Houdini's procedural workflows. Reference Flightradar24 factory tour imagery for colour accuracy and wear patterns.

**Definition of Done:**

- PBR textures (Albedo, Roughness, Metallic, Normal) at 2K-4K resolution.
- Materials react realistically to lighting (metallic sheen, anisotropic reflections).
- Wear patterns (scratches, oxidation) grounded in real-world references.

### 🔄 [JET-21] Final Asset Assembly & USD Export

**Status**: 🔄 In Progress
**Estimate**: 6h
**Objective**: Collect all geometry, materials, and variants into a single, clean .USD file. This is the final deliverable for this Epic, ready for the main scene assembly.

**Definition of Done:**

- Single USD file (`Trent_1000_Hero.usd`) with correct hierarchy (Fan, Compressor, Combustion, Turbine, Nozzle).
- Materials assigned and functional in USD Preview Surface.
- File opens in Omniverse without errors, renders correctly.

---

## 🧩 EPIC: Environment: Testbed 80 (JET-4)

**Status**: 🔄 In Progress

### 🔄 [JET-24] Model Architectural Shell (Testbed 80)

**Status**: 🔄 In Progress
**Estimate**: 6h
**Objective**: Create the main "bunker" structure based on refs: walls (including their massive 1.7m+ thickness), floor (including the embedded rails), and ceiling.

**Definition of Done:**

- Accurate proportions based on reference images.
- Embedded rail system modelled into floor.
- Wall thickness and structural reinforcements visible.

### 🔄 [JET-25] Model Environmental Details

**Status**: 🔄 In Progress
**Estimate**: 6h
**Objective**: Add key high-fidelity details: wall acoustic panels, ceiling crane, the main air intake/exhaust structures, doors, and all visible light fixtures.

**Definition of Done:**

- Acoustic panels modelled with correct pattern and mounting.
- Ceiling crane rail and hook system functional (rigged or static).
- Air intake/exhaust ducts visible and connected to wall penetrations.

### 🔄 [JET-26] UV Unwrapping & Texturing (Environment)

**Status**: 🔄 In Progress
**Estimate**: 6h
**Objective**: Create clean UVs for all environmental assets. Author PBR materials (raw concrete, painted metal, acoustic panelling) to achieve a realistic, heavy industrial look.

**Definition of Done:**

- UV layouts optimised for tileable textures where appropriate.
- Concrete materials show realistic roughness variation and discolouration.
- Painted metal shows wear at contact points (doors, railings).

### 🔄 [JET-27] Export Environment as USD

**Status**: 🔄 In Progress
**Estimate**: 6h
**Objective**: Assemble all environmental components into a single, optimised USD file (e.g., "Testbed_80.usd"), ready for scene assembly.

**Definition of Done:**

- USD file loads in Omniverse without errors.
- Lighting-ready (neutral grey materials if no textures applied yet).
- Polycount optimised (LODs if necessary).

---

## 🧩 EPIC: Asset Creation (Test Stand) (JET-5)

**Status**: 🔄 In Progress

### 🔄 [JET-28] Model Test Stand Rig

**Status**: 🔄 In Progress
**Estimate**: 6h
**Objective**: Model the main mechanical rig/gantry that holds the engine, based on visual references. Focus on the connection points to the engine and the ceiling mount.

**Definition of Done:**

- Rig accurately represents mounting points visible in references.
- Hydraulic/mechanical actuators modelled with correct proportions.
- Engine mounting interface matches Trent 1000 flange geometry.

### 🔄 [JET-29] UV Unwrapping & Texturing (Test Stand)

**Status**: 🔄 In Progress
**Estimate**: 6h
**Objective**: Create UVs and PBR materials (heavy painted industrial metal, hydraulic elements) for the test stand.

**Definition of Done:**

- Industrial painted metal shader with chipping and wear.
- Hydraulic lines show rubber/steel material transition.
- Warning labels and markings applied (decals or baked textures).

### 🔄 [JET-30] Export Test Stand as USD

**Status**: 🔄 In Progress
**Estimate**: 6h
**Objective**: Export the stand as a separate, optimised USD asset (e.g., "Test_Stand.usd").

**Definition of Done:**

- USD file integrates cleanly with `Testbed_80.usd` and `Trent_1000_Hero.usd`.
- Transform pivots set correctly for animation (if rigged).
- Materials render correctly in Omniverse.

---

## 🧩 EPIC: Simulation & VFX (JET-6)

**Status**: Backlog
**Unblocks after**: JET-3, JET-4, JET-5 complete
**Objective**: Implement visual effects for engine operation: exhaust plume particle systems, heat haze shaders, combustion chamber glow.

**Planned Scope:**

- Houdini Pyro simulation for exhaust plume (cached to USD Volume)
- Heat distortion shader (refractive index modulation based on EGT data)
- MDL shaders for incandescence (turbine glow at high EGT)
- PhysX debris simulation (optional: simulated blade shedding for failure scenarios)

**Key Decisions:**

- Pre-cache simulations in Houdini → export as USD Volumes (not real-time physics)
- Multiple cached states per engine mode (Idle/Takeoff/Cruise/Max)
- Shader-driven effects (glow, heat haze) respond to CSV telemetry data

---

## 🧩 EPIC: Pipeline & Data Integration (JET-7)

**Status**: Backlog
**Unblocks after**: JET-23 (CSV generation), JET-21 (Hero Asset USD Export)
**Objective**: Connect telemetry CSV data to USD scene via Python scripting. Drive visual states (fan rotation, turbine glow, FUI displays) based on engine mode.

**Planned Scope:**

- Python script in Omniverse reads CSV data (timestamp, RPM, EGT, etc.)
- Map data to USD attributes:
  - `RPM_LP/IP/HP` → Fan/Compressor/Turbine rotation speed (Xform animation)
  - `EGT` → Turbine incandescence intensity (MDL shader parameter)
  - `Thrust_kN` → Exhaust plume volume density (USD Volume attribute)
  - `engine_mode` → State switcher (loads appropriate Houdini cache variant)
- FUI screens render telemetry graphs in real-time (texture-based or geometry-based UI)

**Key Decisions:**

- Use USD Variants to store multiple simulation states (one variant per engine mode)
- Python script: Omniverse Kit Extension or standalone USD API script?
- Telemetry data synchronisation: frame-based (24fps) or time-based (real seconds)?

---

## 🧩 EPIC: Scene Assembly & LookDev (JET-8)

**Status**: Backlog
**Unblocks after**: JET-6 (VFX), JET-7 (Data Integration)
**Objective**: Assemble final Omniverse scene with all assets, establish cinematic lighting, create camera animations for turntable and hero shots.

**Planned Scope:**

- Import all USD assets (`Trent_1000_Hero.usd`, `Testbed_80.usd`, `Test_Stand.usd`)
- Lighting rig:
  - Studio HDRI (soft key light, rim light from ceiling)
  - Practical lights (testbed fixtures, warning beacons)
  - Spot/area lights for engine detail shots (highlight fan blades, turbine stages)
- Camera sequences:
  - Turntable orbit (360°, slow rotation)
  - Close-up: Fan blade detail
  - Cross-section reveal: Internal combustion/turbine glow
  - FUI overlay: Telemetry dashboard over engine view
- Final polish: Depth of Field, Motion Blur, colour grading via Omniverse post-process

**Key Decisions:**

- Use Omniverse RTX Path Tracing or Real-Time rendering?
- Camera animation: keyframed in Omniverse or exported from Houdini/Blender?

---

## 🧩 EPIC: Final Shot Production & Delivery (JET-9)

**Status**: Backlog
**Unblocks after**: JET-8 (Scene Assembly)
**Objective**: Render final shots, apply post-production (compositing, grading), encode deliverables for NVIDIA Showreel submission.

**Planned Scope:**

- Render passes: Beauty, Diffuse, Specular, Emission, Z-Depth, Cryptomatte
- Compositing (After Effects / Nuke):
  - Add film grain, vignette, lens distortion for cinematic look
  - Composite FUI elements over 3D render
  - Colour grading: industrial blue-grey palette with warm engine glow highlights
- Export deliverables:
  - **Hero Shot**: 4K (3840×2160), H.264, 24fps, ~15-30 seconds
  - **Turntable Animation**: 1080p, looping GIF + MP4
  - **Detail Shots**: 4K stills (JPG/PNG) for portfolio
- Documentation: Breakdown images (wireframe, lighting passes, shader previews)

**Key Decisions:**

- Final delivery format: MP4 (ProRes 422 for archival, H.264 for web)?
- Include "Making Of" breakdown images in GitHub README?

---

## 🔗 Task Dependencies

**Critical Path** (tasks that block downstream work):

```text
JET-1 (Research) → JET-3 (Hero Asset) → JET-7 (Data Integration) → JET-8 (Scene Assembly) → JET-9 (Delivery)
                → JET-4 (Environment) ↗
                → JET-5 (Test Stand) ↗
```

**Detailed Dependencies:**

| Task | Depends On | Reasoning |
| ---- | ---------- | --------- |
| JET-17 (Retopo) | — | Starting point for hero asset |
| JET-18 (Cables/Pipes) | JET-17 | Dress kit needs clean engine surface to sample points |
| JET-19 (UV Unwrap) | JET-17 | Cannot UV unwrap until retopo is complete |
| JET-20 (Texturing) | JET-19 | Texturing requires clean UVs |
| JET-21 (USD Export) | JET-18, JET-20 | All geometry and materials must be finalised |
| JET-23 (CSV data) | JET-21, JET-28 | CSV needs rigged USD assets to test animations |
| JET-24 (Testbed Shell) | — | Can proceed in parallel with JET-17 |
| JET-27 (Environment USD) | JET-24, JET-25, JET-26 | All environment components required |
| JET-28 (Test Stand) | — | Can proceed in parallel |
| JET-30 (Stand USD) | JET-28, JET-29 | Stand geometry and textures required |
| JET-6 (Simulation/VFX) | JET-21 | VFX simulations need hero asset geometry |
| JET-7 (Data Integration) | JET-23, JET-21 | CSV data and USD scene required |
| JET-8 (Scene Assembly) | JET-6, JET-7, JET-27, JET-30 | All assets, VFX, and data integration complete |
| JET-9 (Final Delivery) | JET-8 | Scene must be final before rendering |

---

## 📊 Progress Summary

| Epic | Status | Completion |
| ------ | -------- | ------------ |
| JET-1 (Research) | ✅ 80% Done | 4/5 tasks complete |
| JET-3 (Hero Asset) | 🔄 In Progress | 0/5 tasks complete |
| JET-4 (Environment) | 🔄 In Progress | 0/4 tasks complete |
| JET-5 (Test Stand) | 🔄 In Progress | 0/3 tasks complete |
| JET-6 (Simulation) | ⏸️ Backlog | Not started |
| JET-7 (Pipeline) | ⏸️ Backlog | Not started |
| JET-8 (Scene Assembly) | ⏸️ Backlog | Not started |
| JET-9 (Final Delivery) | ⏸️ Backlog | Not started |

**Total Estimated Hours (Active Tasks)**: 72h (12 tasks × 6h each)

---

## 🎯 Next Priorities

1. **JET-28** (Model Test Stand Rig) — Start here for immediate visual progress
2. **JET-24** (Model Testbed 80 Shell) — Parallel track for environment
3. **JET-17** (Retopologize Engine Core) — Critical path for hero asset
