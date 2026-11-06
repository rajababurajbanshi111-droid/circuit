# Boolean Expression to Circuit Designer & Tinker Circuit

A high-performance web-based digital logic circuit simulator, automatic Boolean circuit designer, and Tinkercad hardware synthesis tool built with native HTML5 Canvas, a discrete event-driven propagation simulation engine, and an automated logic synthesis compiler.

---

## 🚀 Live Demo

Host this repository directly on **GitHub Pages** for a live, interactive web application:
1. Go to **Settings** > **Pages** in this repository.
2. Under **Build and deployment**, select `Deploy from a branch`.
3. Choose branch `main` and folder `/ (root)`, then click **Save**.
4. Your application will be live at: `https://<your-username>.github.io/<repo-name>/`

---

## ✨ Key Features

1. **Gate Reuse & Inverter Sharing (Common Subexpression Elimination)**:
   - When an inverted variable (such as $I_1'$, $A'$, $B'$) is used multiple times, the synthesizer instantiates **only one NOT gate** and branches the output wire to all destination gates.
   - Commutative intermediate terms (like $A \oplus B$ in the Full Adder) are reused across outputs, achieving minimal gate schematics ($2 \times \text{XOR}$, $2 \times \text{AND}$, $1 \times \text{OR}$).

2. **Non-Overlapping Input Bus Rails**:
   - Each input variable ($A, B, C \dots$) is assigned its own dedicated vertical highway rail ($X$-coordinate).
   - Taps to gate inputs branch off with standard solder junction dots (`•`), completely eliminating overlapping input lines.
   - Distinct color coding per input net.
   - Pin signal badges (e.g. `A`, `B`, `A'`) appear directly on gate input terminals.

3. **Dedicated Tinker Circuit (Hardware & Breadboard) Tab**:
   - **74xx TTL IC Bill of Materials (BOM)**: Automatically maps logic gates to real physical IC chips:
     - `74LS04` (Hex Inverter)
     - `74LS08` (Quad 2-Input AND)
     - `74LS32` (Quad 2-Input OR)
     - `74LS86` (Quad 2-Input XOR)
     - `74LS00` (Quad 2-Input NAND)
     - `74LS02` (Quad 2-Input NOR)
   - **DIP-14 Package Pinout Visualizer**: Shows IC notches, pin numbering (Pins 1–14), VCC (+5V, Pin 14), and GND (Pin 7).
   - **Virtual Breadboard & LED Test Station**: Interactive switches and glowing output LED.
   - **Physical IC Netlist Table**: Exact pin-to-pin jumper wire connections for assembling on a physical breadboard.
   - **One-Click Tinkercad Circuits / Arduino Exporter**: Ready-to-paste C++ code for Autodesk Tinkercad Circuits with an Arduino Uno.
   - **Verilog HDL & SPICE Netlist**: Ready for FPGA or analog simulation.

4. **Interactive Karnaugh Map (K-Map) Solver, Minimizer & Custom Drawer**:
   - Interactive Gray-code torus grid supporting **2, 3, 4, and 5 variables** with minterm numbers ($m_0 \dots m_{31}$).
   - **✏️ Custom Value & Minterm Drawing**: Directly type minterms (e.g. `1, 3, 5, 7, 9`) and don't cares (e.g. `11, 15`) and click **"Apply Values"** to immediately draw the map!
   - **Tactile Cell Editing**: Left-click to toggle: $0 \to 1 \to X \text{ (Don't Care)} \to 0$; right-click to cycle in reverse: $0 \to X \to 1 \to 0$.
   - **Visual Prime Implicant Grouping**: Automated loop detection (sizes 16, 8, 4, 2, 1) with vibrant color-coded outline rings and torus wrap-around/4-corner detection.
   - **SOP & POS Minimization**: Computes minimal Sum-of-Products (SOP) and Product-of-Sums (POS) equations with step-by-step variable elimination breakdown.
   - **⛶ Fullscreen K-Map Drawing Workspace**: Click `⛶ Full Screen` to expand the K-Map into a full-window layout with large 68px cells for effortless drawing and analysis.
   - **⚡ One-Click Circuit Generation & Fullscreen View**: Direct button to synthesize and simulate the minimized K-Map expression immediately on the schematic canvas, with option to open directly into Fullscreen Canvas!

5. **Multi-Input Wire Traceability & Net Path Highlighting**:
   - Solves the multi-input wire traveling problem: when many inputs travel across the schematic, simply **hover or click** any input switch, wire, or gate pin to illuminate the entire net!
   - **Laser Pulse Glow & Dimming**: All wires on the active net glow with thick neon halos and animated white energy pulses, while all unrelated wires softly dim to 12% opacity.
   - **On-Canvas HUD Trace Badge**: A floating HUD pill displays: `⚡ TRACE ACTIVE: Input [A] ➔ Feeds 3 Gate Inputs`. Click to lock the trace; click empty space to unlock.
   - **Color-Coded Pin Origin Badges**: Every gate input terminal features a color-coded pill badge with left border and dot matching its origin input's distinct color (`#10b981` Green for A, `#f59e0b` Amber for B, `#06b6d4` Cyan for C, `#a855f7` Purple for D, etc.).
   - **Preserved Color on HIGH Signals**: High-state wires maintain their assigned input net color rather than turning generic cyan.
   - **🔍 Trace Toggle**: Toolbar button `🔍 Trace: ON/OFF` to easily enable or disable interactive path tracing.

6. **⛶ Fullscreen Circuit Canvas Mode**:
   - A dedicated **`⛶ Fullscreen`** button on both the top header and canvas toolbar expands the circuit schematic to fill 100% of the screen.
   - Inspect multi-input circuits with zero distraction, full interactive switch toggling, high-DPI scaling, and smooth pan/zoom. Press `Escape` to smoothly return to split view.

5. **Digital Timing Waveform Analyzer**:
   - Oscilloscope-style digital square wave diagram tracking input transitions and output response.

6. **Interactive Canvas & Annotations**:
   - ANSI/IEEE standard gate symbols with smooth Bezier curves or orthogonal draggable waypoints.
   - **Sticky Notes**: Full multi-line notes with folded corners (`📝 + Note`).
   - **Compact Notation Indicator Tags**: Ultra-slim 24px badge indicators (`🏷️ + Tag`) with pin pointer dots that fit anywhere between gates or on wires.
   - **Schematic Footer**: Displays live active Boolean expressions, inputs summary, live output state readouts, gate counts, and architecture mode badge with `↕️ Expand` and `📋 Copy` buttons.

7. **Preservation of Architecturally Required Inputs**:
   - Standard circuits keep all architecturally required inputs (e.g. $I_0$ in 4-to-2 and 8-to-3 Encoders, $I_3$ in 3-to-1 MUX) on the canvas and in truth tables, even if unconnected to gates.
   - Custom expressions support `INPUTS: I0, I1, I2, I3` directives or `// Inputs: ...` comments.

8. **Standard Library of 31 Verified Combinational Circuits**:
   - **Standard Expressions**: XOR Pattern, Grouped expressions, SOP equations, Majority Function, De Morgan's Laws.
   - **Encoders**: 4-to-2 Binary (I0..I3), 8-to-3 Octal (I0..I7), 4-to-2 Priority, 8-to-3 Priority (74LS148).
   - **Decoders**: 2-to-4 Line, 2-to-4 Line with Enable, 3-to-8 Line (74LS138), 3-to-8 with Enable, BCD-to-7-Segment.
   - **Multiplexers (MUX)**: 2-to-1, 3-to-1 (with I3 preserved), 4-to-1, 8-to-1.
   - **Demultiplexers (DEMUX)**: 1-to-2, 1-to-3, 1-to-4, 1-to-8.
   - **Arithmetic & Converters**: Half/Full Adders, Half/Full Subtractors, 1-bit & 2-bit Magnitude Comparators, Parity Generators, 4-bit Binary to Gray, 4-bit Gray to Binary.

9. **Customizable Settings & Lab Themes**:
   - Audio feedback on switch toggles, wire display styles (flexible Bezier vs orthogonal), gate pin labels, animated high-state current pulses, and 3 high-contrast themes (Dark Cyber, Light Engineering Lab, Midnight OLED).

10. **2-Input & 3-Input Logic Gate Creation & TTL ICs**:
    - Palette pin count toggle (`2-In` vs `3-In`) for custom circuit design.
    - Contextual in-canvas gate input switcher (convert 2-input gates to 3-input on the fly).
    - Realistic hardware mapping to 74xx DIP-14 ICs: 74LS08 (Quad 2-In AND), 74LS11 (Triple 3-In AND), 74LS32 (Quad 2-In OR), 74HC4075 (Triple 3-In OR), 74LS00 (Quad 2-In NAND), 74LS10 (Triple 3-In NAND), 74LS02 (Quad 2-In NOR), 74LS27 (Triple 3-In NOR), 74LS86 (Quad 2-In XOR).

11. **Teacher / Exam Question Mode**:
    - Preset question bank with classic classroom & exam questions (BCD Invalid Codes with Don't Cares, Prime Number Detector, Majority Voters, 4-Corner Adjacency).
    - Intelligent exam question prompt parser: paste equations like `F(A,B,C,D) = Σm(1,3,5,7,9) + d(11,15)` to auto-populate and minimize.
    - Screen auto-fit: compact viewport layout and zero-zoom circuit synthesis (`zoomToFit`).

---

## 🧪 Testing

Run all automated verification test suites:
```bash
node test_trace_and_custom_kmap.js # Verify multi-input wire tracing, custom K-Map values & fullscreen
node test_kmap.js                  # Verify Karnaugh Map prime implicants, POS/SOP & torus wrapping
node test_expression_labels.js     # Verify gate signal formatting & expression toggle
node test_gate_sharing.js           # Verify inverter & gate sharing
node test_all_standard.js           # Verify all 31 library circuits
node test_engine.js                 # Verify parser, recommendations & truth tables
node test_tinker.js                 # Verify Tinkercad BOM & Arduino generator
```
