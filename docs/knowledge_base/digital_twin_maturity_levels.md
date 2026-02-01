# Digital Twin Maturity Levels — Classification Framework

2:
3: **Source:** Academic research (Tao et al.) and industry frameworks
4: **Date:** 2026-02-01
5: **Context:** Reference documentation for Case 02 (Jet Engine) Digital Twin classification
6:
7: ---
8:
9: ## Overview
10:
11: Digital Twin maturity levels classify the sophistication and capabilities of a digital twin, progressing from basic descriptive models to highly autonomous and predictive systems. The classification extends from **L0 (static replica)** to **L5 (autonomous co-existence)**, with the core operational levels being L1-L3.
12:
13: ---
14:
15: ## Level Definitions
16:
17: ### L0: No Twin / Static Model
18:
19: **Descriptor:** Descriptive / Static Replica
20:
21: **Characteristics:**
22:
23: - No active digital twin or only a static 3D model
24: - Describes and depicts the physical entity without real-time data connection
25: - Measurements are disparate or non-existent
26: - Sensors are not interconnected
27:
28: **Use Cases:**
29:
30: - Visualisation
31: - Planning and communication
32: - CAD/BIM models for documentation
33: - Geometry and material representation
34:
35: **Key Limitation:** No dynamic behaviour or connection to the physical world.
36:
37: ---
38:
39: ### L1: Status / Reflecting the Real with the Virtual
40:
41: **Descriptor:** Informative (Real-Time Data) / Connected - Manual
42:
43: **Characteristics:**
44:
45: - Real-time data capture from sensors
46: - Replicates the real-time state and changes in the physical entity
47: - Continuous monitoring of asset condition and performance
48: - Primary function: **"What is happening right now?"**
49:
50: **Use Cases:**
51:
52: - Real-time status dashboards
53: - Condition monitoring
54: - Performance tracking
55: - Asset visibility
56: - **FUI/HUD overlays for real-time telemetry**
57:
58: **Data Flow:** Physical Asset → Sensors → Digital Twin (Visualisation)
59:
60: **Key Capability:** Reflects current conditions dynamically.
61:
62: ---
63:
64: ### L2: Controlling the Real with the Virtual
65:
66: **Descriptor:** Informative (Real-Time + Historical Data) / Connected - Supervisory / Decision Support
67:
68: **Characteristics:**
69:
70: - Real-time data + historical data or benchmarks
71: - Can indirectly control the physical entity's operations
72: - Enables informed decision-making and analysis
73: - Captures and estimates effects of real-world events using historical data
74: - Primary function: **"What should I do about it?"**
75:
76: **Use Cases:**
77:
78: - Predictive maintenance (early stage)
79: - Asset optimisation
80: - Decision support systems
81: - Supervisory control (operator-in-the-loop)
82:
83: **Data Flow:** Physical Asset ↔ Digital Twin ↔ Operator (Decision Support)
84:
85: **Key Capability:** Supports operational decisions through analysis and recommendations.
86:
87: ---
88:
89: ### L3: Anticipating the Real with the Virtual
90:
91: **Descriptor:** Predictive / Forecasting
92:
93: **Characteristics:**
94:
95: - Forecasts future state and operational processes
96: - Couples real-time + historical data with ML or physical process-based models
97: - Predicts future behaviour and performance
98: - Primary function: **"What will happen next?"**
99:
100: **Data Flow:** Physical Asset → Digital Twin → ML/Simulation Models → Predictions → Operator
101:
102: **Key Capability:** Predictive analytics and future state forecasting.
103:
104: ---
105:
106: ## Case 02 (Jet Engine) — Classification Justification
107:
108: **Classified Level:** **L1 (Informative / Connected)** (with elements of L2/L3 simulation visualization)
109:
110: ### Scenario
111:
112: A cutaway view of a **Rolls-Royce Trent 1000** jet engine on Testbed 80. The digital twin visualises internal physical processes that are otherwise invisible: thermodynamics (temperature gradients), fluid dynamics (airflow), and mechanical stress.
113:
114: ### L1 Characteristics Present
115:
116: - ✅ **Data Visualization:** Displays complex internal states (pressure, temperature, RPM) via FUI.
117: - ✅ **Reflecting the Real:** The visual model updates to match the engine's operating regime (Idle, Take-off, Cruise, Max).
118: - ✅ **Monitoring:** "X-Ray" vision allows engineers to see inside the running engine.
119: - ✅ **Primary function:** Answers "What is the thermodynamic state of the core right now?"
120:
121: ### Why Not L0?
122:
123: It connects "live" (simulated) data streams to visual properties. It is not just a static model; the airflow and heat maps react to the Throttle Lever Angle.
124:
125: ### Why Not Full L2?
126:
127: While it supports decision-making (Engine Health Monitoring), the primary goal of this Showreel case is the **high-fidelity visualization of complex scientific data (CFD/Houdini caches)** rather than the control loop itself.
128:
129: ---
130:
131: ## Project Focus Areas
132:
133: 1. **Scientific Visualization:** Translating heavy Houdini Pyro/FEM simulations into real-time Omniverse assets (Volume/Flow).
134: 2. **X-Ray Aesthetics:** Developing shaders that reveal internal structure without losing form definition.
135: 3. **FUI Integration:** Displaying engineering telemetry (EGT, N1/N2/N3) in 3D space.
136:
137: ---
138:
139: ## References
140:
141: 1. Tao et al. — Digital Twin Maturity Framework
142: 2. [Digital Twin Atlas](https://digital-twin-atlas.com/)
143: 3. Rolls-Royce "IntelligentEngine" vision
144:
145: ---
146:
147: **Document Status:** Knowledge Base Entry
148: **Last Updated:** 2026-02-01
149: **Maintained by:** Miles (Case 02 Assistant)
