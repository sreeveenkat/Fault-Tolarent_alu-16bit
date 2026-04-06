🔐 Fault-Tolerant ALU
Multi-Level Error Detection using Parity Prediction, Carry Checking & Residue Codes (mod-3 / mod-5)

This project implements a Fault-Tolerant Arithmetic Logic Unit (ALU) in SystemVerilog with multiple parallel error detection techniques designed for reliable digital systems.

The architecture improves fault coverage by combining:
<img width="1536" height="1024" alt="image" src="https://github.com/user-attachments/assets/0f08a08c-4b6c-4635-a4a8-51df241f3ad9" />

✅ Parity Prediction
✅ Carry Chain Checking
✅ Residue Code Checking (mod-3 and mod-5)
✅ Multi-Level Error Decision Logic

This design targets:

Fault-resilient VLSI systems
AI accelerator datapaths
Safety-critical arithmetic units
FPGA/ASIC research implementations
🏗 Architecture Diagram

🧠 System Overview

The design consists of two primary sections:

1️⃣ ALU Core (Functional Unit)
Performs arithmetic and logical operations.
Generates result and internal carry chain.
Parameterizable bit-width (default: 8-bit, scalable to 16/32-bit).

Supported operations:

Opcode	Operation
000	ADD
001	SUB
010	AND
011	OR
100	XOR
101	Shift Left
110	Shift Right
2️⃣ Error Detection Units (Parallel Checking)

Three independent mechanisms validate computation simultaneously.

🔹 Parity Prediction

Input parity is computed:

P(A) ⊕ P(B)

Compared with output parity:

P(Result)

If mismatch → parity_error = 1

✔ Low area overhead
✔ Fast detection
⚠ May miss some multi-bit symmetric errors

🔹 Carry Chain Checking
Monitors internal carry propagation.
Detects carry corruption in ripple-carry structure.
Ensures carry[i+1] consistency.

If invalid carry relation → carry_error = 1

✔ Strong for arithmetic datapath faults

🔹 Residue Code Checking (mod-3 & mod-5)

For addition:

(A + B) mod m == (A mod m + B mod m) mod m

Where m = 3 or 5.

Process:

Compute residue of A
Compute residue of B
Compute residue of Result
Compare predicted vs actual residue

If mismatch → residue_error = 1

✔ Detects multi-bit arithmetic faults
✔ Higher coverage than parity alone

🔎 Multi-Level Error Decision

Final fault signal:

error_flag = parity_error 
           | carry_error 
           | residue3_error 
           | residue5_error;
🏭 RTL → GDSII Design Flow
SystemVerilog RTL
        ↓
Functional Simulation
        ↓
Synthesis
        ↓
Floorplanning
        ↓
Placement
        ↓
Clock Tree Synthesis (CTS)
        ↓
Routing
        ↓
Static Timing Analysis (STA)
        ↓
Physical Verification (DRC/LVS)
        ↓
GDSII Generation
📊 Physical Design Results
📐 Area
Total Cell Area : 6868.11 µm²
Total Instances : 979 cells
⚡ Timing
Clock Frequency : 100 MHz
Worst Setup Slack : +0.061 ns ✅
Timing Status : Met
🧪 Verification
DRC Violations : 0 ✅
Connectivity : Clean ✅
🔌 Power
Supply Voltage : 0.9V
⚠ Note: Power net connection warnings observed (requires globalNetConnect refinement)
⚖️ Fault-Tolerance Overhead
Metric	Standard ALU	Fault-Tolerant ALU
Area	Low	Increased
Delay	Low	Slightly Higher
Reliability	Low	High
🧪 Fault Coverage

The design improves reliability using multiple detection mechanisms:

Parity → detects bit-level errors
Carry checking → detects arithmetic carry faults
Residue codes → detects multi-bit computation errors

✔ Combined approach significantly improves overall fault detection coverage

🧰 Tools & Technologies
RTL Design : SystemVerilog
Simulation : ModelSim / XSIM
Synthesis : Cadence / Synopsys / Vivado
Physical Design : Cadence Innovus
Verification : Custom Testbench
📁 Repository Structure
├── rtl/
├── testbench/
├── simulation_results/
├── synthesis/
├── floorplan/
├── placement/
├── cts/
├── routing/
├── signoff/
├── gds/
└── README.md
🎯 Key Contributions
Designed multi-layer fault detection ALU
Integrated parity, carry, and residue checking
Achieved reliable computation with redundancy
Completed full RTL → GDSII ASIC flow
Achieved timing closure with clean physical verification
📦 Final Outcome

✔ Successfully implemented Fault-Tolerant ALU from RTL → GDSII
✔ Achieved timing closure and zero DRC violations
✔ Demonstrated practical ASIC design and fault-tolerant techniques
