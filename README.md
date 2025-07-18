# DIGITAL-VLSI-SOC-DESIGN-AND-PLANNING

## Table of contents
- [Day 1 - Inception of open-source EDA, OpenLANE and sky130 PDK](#day-1---inception-of-open-source-eda-openlane-and-sky130-pdk)
  - [How to talk to computers](#How-to-talk-to-computers)
    - [Introduction to QFN-48 Package, chip, pads, core, die and IPs](#Introduction-to-QFN-48-Package,-chip,-pads,-core,-die-and-IPs)
    - [Introduction to RISCV](#Introduction-to-RISCV)
    - [How Applications Run Inside Hardware (Laptop/Chip Level)](#How-Applications-Run-Inside-Hardware-(Laptop/Chip-Level))
  - [Soc design and OpenLANE](#Soc-design-and-OpenLANE)
    - [Introduction to all components of open-source digital asic design](#Introduction-to-all-components-of-open-source-digital-asic-design)
    - [Simplified RTL2GDS flow](#Simplified-RTL2GDS-flow)
    - [Introduction to OpenLANE and Strive chipsets](#Introduction-to-OpenLANE-and-Strive-chipsets)
    - [Introduction to OpenLANE detailed ASIC design flow](#Introduction-to-OpenLANE-detailed-ASIC-design-flow)
  - [Get familiar to open-source EDA tools](#Get-familiar-to-open-source-EDA-tools)
    - [OpenLANE Directory structure in detail](#OpenLANE-Directory-structure-in-detail)
    - [Design Preparation Step](#Design-Preparation-Step)
    - [Review files after design prep and run synthesis](#Review-files-after-design-prep-and-run-synthesis)
    - [OpenLANE Project Git Link Description](#OpenLANE-Project-Git-Link-Description)
    - [Steps to characterize synthesis results](#Steps-to-characterize-synthesis-results)
- [Day 2 - Good floor planning considerations](#Day-2---Good-floor-planning-considerations)
  - [Chip Floor planning consideration](#Chip-Floor-planning-consideration)
    - [Utilization factor and aspect ratio](#Utilization-factor-and-aspect-ratio)
    - [Concept of pre-placed cells](#Concept-of-pre-placed-cells)
    - [De-coupling capacitors](#De-coupling-capacitors)
    - [Power planning](#Power-planning)
    - [Pin placement and logical cell placement blockage](#Pin-placement-and-logical-cell-placement-blockage)
    - [Steps to run floorplan using OpenLANE](#Steps-to-run-floorplan-using-OpenLANE)
    - [Review floorplan files and steps to view floorplan](#Review-floorplan-files-and-steps-to-view-floorplan)
    - [Review floorplan layout in Magic](#Review-floorplan-layout-in-Magic)
  - [Library building and Placement](#Library-building-and-Placement)
    - [Netlist binding and initial place design](#Netlist-binding-and-initial-place-design)
    - [Optimize placement using estimated wire-length and capacitance](#Optimize-placement-using-estimated-wire-length-and-capacitance)
    - [Final placement optimization](#Final-placement-optimization)
    - [Need for libraries and characterization](#Need-for-libraries-and-characterization)
    - [Congestion aware placement using RePlAce](#Congestion-aware-placement-using-RePlAce)
  - [Cell design and characterization flows](#Cell-design-and-characterization-flows)
    - [Inputs for cell design flow](#Inputs-for-cell-design-flow)
    - [Circuit design steps](#Circuit-design-steps)
    - [Layout design step](#Layout-design-step)
    - [Typical characterization flow](#Typical-characterization-flow)
  - [General timing characterization parameters](#General-timing-characterization-parameters)
    - [Timing threshold definitions](#Timing-threshold-definitions)
    - [Propagation delay and transition time](#Propagation-delay-and-transition-time)
- [Day 3 - Design library cell using Magic Layout and ngspice characterization](#Day-3---Design-library-cell-using-Magic-Layout-and-ngspice-characterization)
  - [Labs for CMOS inverter ngspice simulations](#Labs-for-CMOS-inverter-ngspice-simulations)
    - [IO placer revision](#IO-placer-revision)
    - [SPICE deck creation for CMOS inverter](#SPICE-deck-creation-for-CMOS-inverter)
    - [SPICE simulation lab for CMOS inverter](#SPICE-simulation-lab-for-CMOS-inverter)
    - [Switching Threshold Vm](#Switching-Threshold-Vm)
    - [Static and dynamic simulation of CMOS inverter](#Static-and-dynamic-simulation-of-CMOS-inverter)
    - [Lab steps to git clone vsdstdcelldesign](#Lab-steps-to-git-clone-vsdstdcelldesign)
  - [Inception of layout ̂CMOS fabrication process](#Inception-of-layout-CMOS-fabrication-process)
    - [Create Active regions](#Create-Active-regions)
    - [Formation of N-well and P-well](#Formation-of-N-well-and-P-well)
    - [Formation of gate terminal](#Formation-of-gate-terminal)
    - [Lightly doped drain (LDD) formation](#Lightly-doped-drain-(LDD)-formation)
    - [Source - drain formation](#Source---drain-formation)
    - [Local interconnect formation](#Local-interconnect-formation)
    - [Higher level metal formation](#Higher-level-metal-formation)
    - [Lab introduction to Sky130 basic layers layout and LEF using inverter](#Lab-introduction-to-Sky130-basic-layers-layout-and-LEF-using-inverter)
    - [Lab steps to create std cell layout and extract spice netlist](#Lab-steps-to-create-std-cell-layout-and-extract-spice-netlist)
  - [Sky130 Tech File Labs](#Sky130-Tech-File-Labs)
    - [Lab steps to create final SPICE deck using Sky130 tech](#lab-steps-to-create-final-spice-deck-using-sky130-tech)
    - [Lab steps to characterize inverter using sky130 model files](#lab-steps-to-characterize-inverter-using-sky130-model-files)
    - [Lab introduction to Magic tool options and DRC rules](#lab-introduction-to-magic-tool-options-and-drc-rules)
    - [Lab introduction to Sky130 pdk's and steps to download labs](#lab-introduction-to-sky130-pdks-and-steps-to-download-labs)
    - [Lab introduction to Magic and steps to load Sky130 tech-rules](#lab-introduction-to-magic-and-steps-to-load-sky130-tech-rules)
    - [Lab exercise to fix poly.9 error in Sky130 tech-file](#lab-exercise-to-fix-poly9-error-in-sky130-tech-file)
    - [Lab exercise to implement poly resistor spacing to diff and tap](#lab-exercise-to-implement-poly-resistor-spacing-to-diff-and-tap)
    - [Lab challenge exercise to describe DRC error as geometrical construct](#lab-challenge-exercise-to-describe-drc-error-as-geometrical-construct)
    - [Lab challenge to find missing or incorrect rules and fix them](#lab-challenge-to-find-missing-or-incorrect-rules-and-fix-them)
- [Day 4 - Pre-layout timing analysis and importance of good clock tree](#day-4---pre-layout-timing-analysis-and-importance-of-good-clock-tree)
  - [Timing modeling using delay tables](#timing-modeling-using-delay-tables)
    - [Lab steps to convert grid info to track info](#lab-steps-to-convert-grid-info-to-track-info)
    - [Lab steps to convert magic layout to std cell LEF](#lab-steps-to-convert-magic-layout-to-std-cell-lef)
    - [Introduction to timing libs and steps to include new cell in synthesis](#introduction-to-timing-libs-and-steps-to-include-new-cell-in-synthesis)
    - [Introduction to delay tables](#introduction-to-delay-tables)
    - [Delay table usage Part 1](#delay-table-usage-part-1)
    - [Delay table usage Part 2](#delay-table-usage-part-2)
    - [Lab steps to configure synthesis settings to fix slack and include vsdinv](#lab-steps-to-configure-synthesis-settings-to-fix-slack-and-include-vsdinv)
  - [Timing analysis with ideal clocks using openSTA](#timing-analysis-with-ideal-clocks-using-opensta)
     - [Setup timing analysis and introduction to flip-flop setup time](#setup-timing-analysis-and-introduction-to-flip-flop-setup-time)
     - [Introduction to clock jitter and uncertainty](#introduction-to-clock-jitter-and-uncertainty)
     - [Lab steps to configure OpenSTA for post-synth timing analysis](#lab-steps-to-configure-opensta-for-post-synth-timing-analysis)
     - [Lab steps to optimize synthesis to reduce setup violations](#lab-steps-to-optimize-synthesis-to-reduce-setup-violations)
     - [Lab steps to do basic timing ECO](#lab-steps-to-do-basic-timing-eco)
  - [Clock tree synthesis TritonCTS and signal integrity](#clock-tree-synthesis-tritoncts-and-signal-integrity)
     - [Clock tree routing and buffering using H-Tree algorithm](#clock-tree-routing-and-buffering-using-h-tree-algorithm)
     - [Crosstalk and clock net shielding](#crosstalk-and-clock-net-shielding)
     - [Lab steps to run CTS using TritonCTS](#lab-steps-to-run-cts-using-tritoncts)
     - [Lab steps to verify CTS runs](#lab-steps-to-verify-cts-runs)
  - [Timing analysis with real clock using openSTA](#timing-analysis-with-real-clock-using-opensta)
     - [Setup timing analysis using real clocks](#setup-timing-analysis-using-real-clocks)
     - [Hold timing analysis using real clocks](#hold-timing-analysis-using-real-clocks)
     - [Lab steps to analyze timing with real clocks using OpenSTA](#lab-steps-to-analyze-timing-with-real-clocks-using-opensta)
     - [Lab steps to execute OpenSTA with right timing libraries and CTS assignment](#lab-steps-to-execute-opensta-with-right-timing-libraries-and-cts-assignment)
     - [Lab steps to observe impact of bigger CTS buffers on setup and hold timing](#lab-steps-to-observe-impact-of-bigger-cts-buffers-on-setup-and-hold-timing)
- [Day 5 - Final step for RTL2GDS using tritinRoute and openSTA](#day-5---final-step-for-rtl2gds-using-tritinroute-and-opensta)
  - [Routing and design rule check (DRC)](#routing-and-design-rule-check-drc)
     - [Introduction to Maze Routing Lees algorithm](#introduction-to-maze-routing--lee-algorithm)
     - [Lees Algorithm conclusion](#lees-algorithm-conclusion)
     - [Design Rule Check](#design-rule-check)
  - [Power Distribution Network and routing](#power-distribution-network-and-routing)
     - [Lab steps to build power distribution network](#lab-steps-to-build-power-distribution-network)
     - [Lab steps from power straps to std cell power](#lab-steps-from-power-straps-to-std-cell-power)
     - [Basics of global and detail routing and configure TritonRoute](#basics-of-global-and-detail-routing-and-configure-tritonroute)
  - [TritonRoute Features](#tritonroute-features)
     - [TritonRoute feature 1 - Honors pre-processed route guides](#tritonroute-feature-1---honors-pre-processed-route-guides)
     - [TritonRoute Feature2 & 3 - Inter-guide connectivity and intra- & inter-layer routing](#tritonroute-feature2--3---inter-guide-connectivity-and-intra--inter-layer-routing)
     - [TritonRoute method to handle connectivity](#tritonroute-method-to-handle-connectivity)
     - [Routing topology algorithm and final files list post-route](#routing-topology-algorithm-and-final-files-list-post-route)
- [References](#references)
- [Acknowledgement](#acknowledgement)


---      
# Day 1 - Inception of open-source EDA, OpenLANE and sky130 PDK
---
## How to talk to computers
---
### Introduction to QFN-48 Package, chip, pads, core, die and IPs
---

##  Example: Dissecting the ARDUINO Chip — From Board to Silicon

###  1. System-Level View: Arduino Board

We start by examining the **Arduino board** using a **block diagram**, where different functional components are shown, and the **main processor** (microcontroller) is highlighted. This processor is the heart of the system and handles the core logic and control tasks.

![Screenshot 2025-05-11 131627](https://github.com/user-attachments/assets/c1bc1d66-616d-4a6e-a3b4-feaec29c949c)

The Block diagram of the board will look like below

![Screenshot 2025-05-11 131748](https://github.com/user-attachments/assets/04f21c36-2726-4b3a-910c-ed946a82e255)

---

###  2. Processor Package (QFN-48)

Zooming into the processor block:

![Screenshot 2025-05-11 132116](https://github.com/user-attachments/assets/6e009475-3598-422c-8f1d-178f4b0aa3ed)


* The processor is enclosed in a **QFN-48** package — **Quad Flat No-lead** with **48 pins**.
* This **package** acts as the physical container for the chip, providing both protection and electrical connectivity.
* Inside the package, the **silicon chip** (or **die**) is placed in the center.
* The chip is connected to the **IO pins of the package** via **wire bonds**, which are tiny gold or aluminum wires.

![Screenshot 2025-05-11 132558](https://github.com/user-attachments/assets/a2c4a79f-8169-4835-82a9-712846ca4f4e)

---

###  3. Die-Level View: Inside the Chip

Within the package, the actual **chip** contains multiple layers of metal and silicon. Key physical elements include:

![Screenshot 2025-05-11 132731](https://github.com/user-attachments/assets/f63b82e2-cd76-4dc4-a7a8-af0095f9ab9d)


* **Pads**: Metal contact areas on the periphery of the die. These connect to the package pins via wire bonds.
* **Core**: The central region of the die that holds the digital and analog circuits.
* **Die**: The entire silicon piece, including the core, pads, and any other peripheral regions.

---

###  4. Core Components Breakdown

The **core** of the chip includes several important blocks:

![Screenshot 2025-05-11 133639](https://github.com/user-attachments/assets/0fb5ae39-8c58-4b48-8c23-e7b02da5bbdf)


####  Foundry IPs – Standard, Silicon-Proven Blocks

These are **pre-designed, validated modules provided by the foundry** (e.g., SkyWater):

* **SRAM** – Used as internal memory for storing data and instructions.
* **DAC (Digital-to-Analog Converter)** – Converts digital signals into analog voltages.
* **ADC (Analog-to-Digital Converter)** – Converts analog signals from sensors into digital values.
* **PLL (Phase-Locked Loop)** – Generates and stabilizes clock signals for synchronization.

These blocks are known as **Foundry IPs** because they are created and maintained by the foundry for general use in chip designs.

####  Macros – Custom, Higher-Level Functional Blocks

These are **larger, more complex blocks**, typically developed by the chip design team or third-party IP providers:

* **RISC-V SoC** – A full **System on Chip** based on the open-source **RISC-V** architecture. This includes the CPU core, buses, memory interface, etc.
* **SPI (Serial Peripheral Interface)** – A standard communication protocol used for talking to peripherals like sensors and memory chips.

These are called **Macros** because they are **pre-built, reusable modules**, often integrated as black-box components in the design.

---

###  5. Foundry IPs vs. Macros: What's the Difference?

| Aspect           | Foundry IPs                             | Macros                                      |
| ---------------- | --------------------------------------- | ------------------------------------------- |
| Provider         | Semiconductor foundry (e.g., SkyWater)  | Chip designer or third-party IP vendors     |
| Size/Complexity  | Small to medium, focused functions      | Large, complex subsystems or full cores     |
| Examples         | SRAM, PLL, ADC, DAC                     | RISC-V SoC, SPI interface                   |
| Customization    | Minimal (standard blocks)               | High (often tailored to the application)    |
| Integration Type | Built into the flow at transistor level | Integrated as black boxes (hardened blocks) |


---
# Introduction to RISCV
##  Running a C Program on Custom Silicon (Using Qflow + PicoRV32)

To execute a **C program on custom hardware** (fabricated or simulated as a layout), we follow a structured flow from **high-level software** to **low-level hardware implementation**:

---

###  1. C Program Compilation Flow

* The process begins with writing a **C program**.
* This program is compiled into **RISC-V assembly code** using a **RISC-V GCC compiler**.
* The assembly is then **assembled into binary (machine code)** — a set of instructions the processor understands.

  >  This binary will eventually be **loaded into instruction memory** during hardware simulation or execution.

---

###  2. Executing the Binary on a Layout

* The goal is to **run this binary on a custom hardware layout**, which includes a **RISC-V CPU implemented on silicon**.
* Since the layout is built using digital logic, we need a **hardware description (RTL)** of a CPU that understands RISC-V instructions.

---

###  3. Interface Between Software and Hardware (CPU RTL)

* To bridge the software (binary) and hardware (layout), we need a **RISC-V compliant CPU core in RTL** form.
* We use **PicoRV32**, a lightweight and open-source RISC-V CPU core written in **Verilog**.
* PicoRV32 **implements the RISC-V ISA specifications**, acting as the interpreter of the compiled binary.

---

###  4. RTL to GDSII Flow (RTL2GDS2)

* The Verilog RTL (PicoRV32) is taken through the **RTL-to-GDSII flow** using a toolchain like **Qflow** or **OpenLANE**.
* This flow includes:

  1. **Synthesis** – Convert RTL to gate-level netlist.
  2. **Floorplanning** – Define chip layout regions.
  3. **Placement and Routing** – Place cells and wire them.
  4. **Layout (GDSII)** – Generate the physical design file.
* The final **GDSII file** represents the chip layout that can be fabricated or simulated.

---

###  Summary of Flow

```plaintext
[C Program]
    ↓
[RISC-V Assembly]
    ↓
[Machine Code (Binary)]
    ↓
[Loaded into Instruction Memory]
    ↓
[PicoRV32 RTL (Implements RISC-V ISA)]
    ↓
[RTL to GDSII Flow (Qflow/OpenLANE)]
    ↓
[Final Chip Layout (GDSII)]
```
![Screenshot 2025-05-11 140918](https://github.com/user-attachments/assets/0f1d675b-e9d9-4e9b-b292-10da2483ab57)

---



---

### How Applications Run Inside Hardware (Laptop/Chip Level)

Applications that run on a computer or embedded system go through several transformation layers—from high-level code to machine-executable binaries—all the way to physical hardware built from logic gates.

---

###  1. Three Core Components

1. **Application Software**

   * High-level programs written by users (e.g., in C, C++, Java, Python).
   * Examples: web browsers, calculators, games.

2. **System Software**

   * Acts as a bridge between applications and hardware.
   * Includes the **Operating System**, **Compiler**, and **Assembler**.

3. **Hardware (Chip)**

   * The silicon device (e.g., RISC-V processor) that executes the binary instructions.

---

###  2. Role of System Software

System software performs multiple stages of translation to bridge human logic and silicon behavior.

####  Layers of System Software

* **Operating System (OS)**

  * Manages memory, scheduling, input/output, and system-level resources.
  * Coordinates execution but does **not directly convert code** to binary.

* **Compiler**

  * Converts high-level language (C/C++/Java) into **assembly code** specific to a hardware's **Instruction Set Architecture (ISA)**.
  * Output: `.exe`, `.s`, or `.asm` file.

* **Assembler**

  * Translates ISA-level assembly code into **binary machine code**.
  * Output: `.bin`, `.hex`, or `.elf` (Executable and Linkable Format).

![Screenshot 2025-05-11 145243](https://github.com/user-attachments/assets/37cee062-b35f-4599-840c-3f20eb64f7da)

---

###  3. Instruction Set Architecture (ISA): The Abstract Interface

* The **ISA** defines how the processor should behave — a contract between **software and hardware**.
* It includes the instruction formats, data types, addressing modes, registers, etc.
* Example: RISC-V, x86, ARM.

> ISA is **not hardware**, but it defines the rules that **hardware must follow** to execute software correctly.

---

###  4. RTL Implementation of the ISA

* To execute instructions defined by the ISA, we need a **hardware implementation** of it.
* This is done by designing a **Register Transfer Level (RTL)** model (e.g., **PicoRV32**, **Rocket Chip**).

  * RTL is written in **HDL** languages like Verilog or VHDL.
  * It **implements the ISA’s behavior using digital logic (flip-flops, ALUs, control units)**.

---

###  5. From RTL to Physical Chip

Once we have RTL:

1. **Synthesis**

   * RTL is converted into a **gate-level netlist** (logic gates + connections) using tools like Yosys or Synopsys Design Compiler.

2. **Physical Design (PD)**

   * The netlist is used in **floorplanning, placement, and routing** stages to design the chip layout.
   * Tools like OpenLANE or Cadence Innovus are used.
   * Output: **GDSII file** – the final chip design ready for fabrication.

![Screenshot 2025-05-11 145445](https://github.com/user-attachments/assets/c14f0e62-e5ca-4774-923c-ceee85f04111)

---

###  Final Summary Flow

```plaintext
[Application Software]
    ↓ (written in C/C++/Java)
[Compiler]
    ↓ (ISA-specific code, e.g., for RISC-V)
[Assembler]
    ↓ (Binary Machine Code)
[Instruction Set Architecture (ISA)]
    ↓ (Abstract interface for hardware)
[RTL Implementation of ISA (e.g., PicoRV32)]
    ↓
[Synthesis → Gate-Level Netlist]
    ↓
[Physical Design (PD)]
    ↓
[Chip Layout (GDSII)]
```

---
## Soc design and OpenLANE
### Introduction to all components of open-source digital asic design

---

##  Essential Elements to Implement an ASIC

To build an **ASIC (Application-Specific Integrated Circuit)**, the following three components are required:

---

### 1.  **RTL IPs (Register Transfer Level Intellectual Property)**

RTL IPs define the **functional blocks** of your chip, written in HDL languages like Verilog or VHDL. These include processors, memory interfaces, controllers, and more.

####  Open-Source Sources:

* [**librecores.org**](https://librecores.org)
* [**opencores.org**](https://opencores.org)
* [**github.com**](https://github.com) (search for “Verilog” or “RTL IP” repositories)

---

### 2.  **EDA Tools (Electronic Design Automation)**

These tools automate the process of converting your RTL into a physical layout. They handle synthesis, placement, routing, and verification.

####  Open-Source Tools:

* **Qflow** – A complete RTL-to-GDSII flow using open tools
* **OpenROAD** – A fully automated digital layout backend
* **OpenLANE** – A digital ASIC design flow built on top of OpenROAD, Magic, and others

---

### 3.  **PDK Data (Process Design Kit)**

A PDK contains all technology-specific files needed for fabrication: design rules, SPICE models, standard cell libraries, etc.

####  Open-Source PDK:

* **Google + SkyWater SKY130 PDK**

  * The first open-source 130nm PDK
  * Developed by SkyWater in collaboration with Google
  * Hosted and maintained by [Google/SkyWater project on GitHub](https://github.com/google/skywater-pdk)

---
![Screenshot 2025-05-11 181703](https://github.com/user-attachments/assets/36acebb7-658c-4eb3-b73f-38c721ba1320)

---
## Simplified RTL2GDS flow

##  Simplified RTL to GDSII (GDS2) Flow

The **RTL to GDSII flow** converts a high-level hardware description (RTL) into a **physical layout** (GDSII format) ready for chip fabrication. Here's a step-by-step summary of this process:

![Screenshot 2025-05-11 181841](https://github.com/user-attachments/assets/b2503984-052f-47a3-9c6a-2e00de1d3a49)

---

###  Synthesis

* **Goal**: Convert RTL (Verilog/VHDL) into a gate-level **netlist** using Standard Cell Libraries (SCL).
* **Standard Cells**:

  * Have **fixed height**, and width is an **integer multiple of site width**.

    ![Screenshot 2025-05-11 183704](https://github.com/user-attachments/assets/764e2e1b-b221-4d99-86cc-ef83cff0e866)

  * Each cell has multiple "views":

    * **HDL (behavioral)**
    * **SPICE (electrical)**
    * **Layout**: abstract + detailed
* Output: Netlist with basic logic gates and interconnections.

![Screenshot 2025-05-11 183123](https://github.com/user-attachments/assets/9d33ce20-81c1-48c3-b0f3-a49a664ee41a)

---

###  Floorplanning

![Screenshot 2025-05-11 183844](https://github.com/user-attachments/assets/44d44035-e97d-4d27-a8ae-45a940093765)


* **Chip Floorplanning**:

  * Divide the chip die into blocks.
  * Place **I/O pads** around the die.
* **Macro Floorplanning**:

  * Define **macro dimensions** and **pin locations**.
  * Specify **placement rows** for standard cells.
    
![Screenshot 2025-05-11 183925](https://github.com/user-attachments/assets/7c478108-b643-4e75-999b-9ad180d14484)

![Screenshot 2025-05-11 183942](https://github.com/user-attachments/assets/7fa3be31-5ab7-46f4-a206-bcc81298e6ae)

---

###  Placement

![Screenshot 2025-05-11 184056](https://github.com/user-attachments/assets/cadd9ba5-858e-4cbf-843a-001fb2702c74)

* Place standard cells within the defined rows.
* Align cells to the **site grid** for manufacturability.
* Two steps:

  * **Global Placement**: Coarse placement to minimize wirelength.
  * **Detailed Placement**: Refines positions for legal and optimal cell placement.

![Screenshot 2025-05-11 184129](https://github.com/user-attachments/assets/109ee283-1439-4861-a823-37d7a1e8b199)

---

###  Clock Tree Synthesis (CTS)

* Create a **clock distribution network** to deliver the clock signal:

  * To **all sequential elements** (like flip-flops).
  * With **minimum skew** (zero skew is ideal but hard).
* Common clock tree shapes: **H-tree**, **X-tree**, or custom structures.

![Screenshot 2025-05-11 184203](https://github.com/user-attachments/assets/a1ee3ebb-409a-464e-9096-c61e5fd8378a)

---

###  Routing

* Connect all placed cells using **metal interconnects**:

  * **Routing grid** is based on available metal layers and track pitches.
* Two phases:

  * **Global Routing**: Plan the path, generate routing guides.
  * **Detailed Routing**: Final wiring based on routing guides.

![Screenshot 2025-05-11 184259](https://github.com/user-attachments/assets/dccae6d3-ae51-4d70-8fb2-f56abbe48307)

---

###  Physical Verification

Ensure the layout meets manufacturing and functional specifications.

* **Design Rule Checking (DRC)**: Checks layout against foundry rules.
* **Layout vs. Schematic (LVS)**: Verifies layout matches original netlist.
* **Static Timing Analysis (STA)**: Ensures timing constraints are met.

---

### Final Output

* A **GDSII file** — the complete physical layout ready for chip fabrication.

---

#  Introduction to OpenLANE and Strive chipsets

##  What is OpenLane?

**OpenLane** is an open-source digital ASIC design flow developed as part of a true open-source tape-out experiment. Its mission is to enable **fully automated RTL-to-GDSII synthesis** — requiring **no human intervention**.

##  What is Strive?

**Strive** is a family of "**Open Everything**" System-on-Chips (SoCs) built entirely using:
-  **Open RTL** – open-source logic designs
-  **Open EDA Tools** – like OpenLane, Qflow, OpenROAD
-  **Open PDKs** – such as SkyWater 130nm

![Screenshot 2025-05-12 123007](https://github.com/user-attachments/assets/ea236fab-f1a2-402c-a59f-62cc370f3851)

![Screenshot 2025-05-12 123151](https://github.com/user-attachments/assets/02e267b5-ce46-4957-b270-ede0c49bf3cc)

##  OpenLane's Main Goal

Produce a **clean GDSII** layout with:
-  No **LVS violations** (Layout vs. Schematic)
-  No **DRC violations** (Design Rule Check)
-  **Timing violations**: still **Work In Progress (WIP)**

###  Fabrication Support
- Tuned for **SkyWater 130nm Open PDK**
- Also supports:
  - **XFAB180**
  - **GlobalFoundries GF130G**

##  Key Features

-  **Containerized**: Easy to run with Docker
-  **Functional Out-of-the-Box**
-  Native build/run instructions (in development)
-  Use for both **Macro hardening** and **full chip design**

##  Modes of Operation

-  **Autonomous Mode** – Fully automated RTL-to-GDSII
-  **Interactive Mode** – Manual control for debugging & tweaking

##  Design Space Exploration

- Designed to help **find the best flow configuration** for different designs
- Includes **43 open-source designs** with optimized configurations
-  More designs will be added regularly

---


## Introduction to OpenLANE detailed ASIC design flow

**OpenLANE** is a fully open-source flow for digital ASIC design. It automates the transformation of a hardware design (described in Verilog RTL) into a **GDSII layout**, which can be sent for chip fabrication. The flow includes synthesis, floorplanning, placement, routing, DFT, and final verification—all integrated from multiple open tools.

![Screenshot 2025-05-12 125303](https://github.com/user-attachments/assets/06a71c18-c52d-46d9-b8a4-67859a62aad2)

---

### 1.  RTL Synthesis

* The design starts in **Verilog RTL**.
* OpenLANE uses **Yosys** for synthesis. It takes in the RTL and constraints and translates it into a **gate-level netlist**.
* Then, the **ABC** tool maps this netlist to actual **standard cells** using guidance from **ABC scripts**, which define **synthesis strategies**.

#### Synthesis Strategies:

* Aim to optimize for:

  * **Least area**
  * **Best timing**
* OpenLANE provides a **Synthesis Exploration Utility** that tests multiple strategies on a design and reports how area and delay are affected.
* Based on this data, the **best-performing strategy** is selected.

![Screenshot 2025-05-12 130901](https://github.com/user-attachments/assets/2784665a-68b0-481a-8d60-d73d5b657e6d)

---

### 2.  Design Exploration & Regression Testing

* The **Design Exploration Utility** sweeps design configurations to help optimize results.
* It also supports **Continuous Integration (CI)** by running regression tests on \~70+ open designs, comparing results with the best known configurations.

![Screenshot 2025-05-12 131018](https://github.com/user-attachments/assets/f628cc0f-beef-45a3-9be7-bb104122ad1f)

---

### 3.  Design for Testability (DFT)

After synthesis, OpenLANE optionally performs **Design for Testability** using the open-source project **Fault**:

![Screenshot 2025-05-12 131442](https://github.com/user-attachments/assets/6595dac7-d38e-4d00-9424-3897bc6db3b2)

* **Scan Chain Insertion**: Adds logic that makes internal flip-flops observable/testable.
* **ATPG (Automatic Test Pattern Generation)**: Creates test vectors for manufacturing tests.
* **Fault Simulation and Coverage Analysis**
* Adds support logic like a **JTAG Controller** for boundary scan.

---

### 4.  Physical Implementation (PnR) with OpenROAD

OpenROAD automates **Place and Route**, performing the following steps:

####  Floorplanning & Power Planning

* Assign die area, place I/O pads, and macros.
* Insert **endcaps**, **tap cells**, and **decoupling capacitors**.
* Establish **power and ground grid**.

####  Placement

* Global and detailed placement of standard cells in rows.

####  Post-Placement Optimization

* Improve performance and reduce congestion.

####  Clock Tree Synthesis (CTS)

* Builds a distribution tree (H-tree, X-tree) to deliver clock signal to all flip-flops with **minimal skew**.
* Modifies the netlist, so **logic verification** is required afterward.

####  Routing

* Global routing determines approximate paths.
* Detailed routing finalizes wire connections on metal layers.

---

### 5.  Netlist Verification: Logic Equivalence Checking (LEC)

As physical implementation **modifies the netlist** (via CTS, optimization, etc.), it must be re-verified for correctness.

* **Yosys** is used to compare:

  * Synthesized gate-level netlist
  * Post-layout netlist
* Ensures functional equivalence: the logic **has not changed**.

---

### 6.  Antenna Rule Fixes

During fabrication, long metal wires can accumulate charge (like an antenna) and **damage transistor gates**. To address this:

![Screenshot 2025-05-12 132500](https://github.com/user-attachments/assets/042a234e-0a8c-4fc2-9562-974196a2bff0)

* OpenLANE takes a **preventive approach**:

![Screenshot 2025-05-12 132641](https://github.com/user-attachments/assets/4e681067-d681-4fef-a5ea-6b6433e2489f)

  * Inserts a **Fake Antenna Diode** next to every cell input after placement.
  * Runs **Magic’s Antenna Checker** on the routed layout.
  * If any violations are found, **replaces the fake diode** with a **real diode** from the standard cell library.

![Screenshot 2025-05-12 132748](https://github.com/user-attachments/assets/433117c8-e820-4219-9a4a-cac785acdac2)

---

### 7.  Sign-off Checks

Before final GDSII output, the design must pass several critical checks:

####  Static Timing Analysis (STA)

* RC data is extracted via **DEF2SPEF**.
* Timing is verified using **OpenSTA**.

####  Design Rule Checking (DRC)

* Verifies that the layout complies with manufacturing rules using **Magic**.

####  Layout vs. Schematic (LVS)

* Compares the final routed layout to the logical netlist.
* Tools used:

  * **Magic**: Extracts SPICE netlist from layout.
  * **Netgen**: Compares SPICE with synthesized Verilog netlist.

![Screenshot 2025-05-12 133126](https://github.com/user-attachments/assets/46b80c17-7ea3-4134-85c8-7762a16386e6)

---

### 8.  Final Output

The result of the full OpenLANE flow is a **GDSII file**:

* Fully verified for logic, timing, design rules, and manufacturability.
* Can be sent to a foundry for **chip fabrication**.

---

## Get familiar to open-source EDA tools
---
###  OpenLANE Directory structure in detail
---

##  PDKs and Open Source Compatibility

###  What is a PDK?

A **Process Design Kit (PDK)** is a collection of files provided by a semiconductor foundry. It includes everything needed to design integrated circuits for a specific fabrication process node—like **SkyWater 130nm (sky130)**.

These files define:

* Transistor models
* Design rules
* Standard cell libraries
* Layout layers
* Parasitics
* DRC/LVS rules

---

###  Challenge with Foundry PDKs

Most **foundry PDKs** are designed to work with **commercial EDA tools** (like Cadence, Synopsys, Mentor). They are often closed-source and tailored for proprietary formats.

But open-source tools such as:

* **Magic** (Layout & DRC)
* **Netgen** (LVS)
* **OpenROAD** (PnR)
* **Yosys** (Synthesis)

…require **different formats and configurations**.

---

###  Solution: `open_pdks`

To bridge this gap, the **`open_pdks`** project was created. It contains **scripts and build systems** that:

* Convert **foundry-compatible PDKs** into formats usable by open-source EDA tools.
* Structure and install libraries in a standard layout recognized by tools like **Magic**, **Netgen**, and **KLayout**.
* Handle **naming conventions**, **file generation**, and **tool-specific settings**.

---

###  SkyWater’s Open Source PDK: `sky130A`

SkyWater, in partnership with Google, released the **sky130** process node as an open-source PDK.

Within it, the **`sky130A`** variant has been fully adapted using `open_pdks` to work with open-source tools.

The directory is structured into two major parts:

#### 1. `libs.ref/`

* Contains **technology/process-specific files**.
* These are neutral and not tool-specific.
* Includes:

  * Spice models
  * Liberty timing files
  * Cell definitions
  * GDS layouts

#### 2. `libs.tech/`

* Contains **tool-specific configurations** and files.
* Tailored for tools like Magic, Netgen, and KLayout.
* Includes:

  * DRC rules for Magic
  * Extraction rules
  * Tool setup files

---

###  The Library We Use: `sky130_fd_sc_hd`

For most digital designs, we use the **sky130\_fd\_sc\_hd** library, where:

* `fd` stands for **Foundry**
* `sc` stands for **Standard Cells**
* `hd` means **High Density**

This library includes:

* Logic gates like NAND, NOR, Flip-Flops, etc.
* Timing and power models
* Layout views and abstract LEF views
* DRC and LVS-compatible layout data

This library is essential for:

* **Synthesis**: Mapping RTL to standard cells
* **Place & Route**: Using LEF and GDS
* **Verification**: Using extraction rules and simulation models

---

###  Summary

| Component         | Description                                                              |
| ----------------- | ------------------------------------------------------------------------ |
| `open_pdks`       | Converts foundry PDKs for use with open-source tools                     |
| `sky130A`         | SkyWater's open-source 130nm process node adapted for open tools         |
| `libs.ref/`       | Tool-agnostic, process-specific data                                     |
| `libs.tech/`      | Tool-specific data for Magic, Netgen, etc.                               |
| `sky130_fd_sc_hd` | High-density standard cell library used in OpenLANE and other open flows |

![Screenshot 2025-05-14 134235](https://github.com/user-attachments/assets/02d99f54-a9f4-4298-89ec-81cdd3ffd42a)

---
## Design Preparation Step

Invoking OpenLANE 

![Screenshot 2025-05-14 141223](https://github.com/user-attachments/assets/3409996a-2763-4dc7-8ab8-a2acfa297240)

With OpenLANE invoked and the environment initialized, the next step is to load the necessary packages required for running the flow. This begins with the Tcl command: %package require openlane 0.9. At this point, the design flow is ready for execution.
![Screenshot 2025-05-14 142500](https://github.com/user-attachments/assets/153bfa36-69da-4f29-be91-cb1dc12beaa7)


---

###  `picorv32a` Design Directory Structure

When using OpenLANE, each design (like `picorv32a`) follows a specific directory structure. The most important components are:

---

### 1. **`src/` Directory**

* **Purpose:** Contains the **RTL source files** for the design.
* **Typical contents:** `.v` (Verilog) files.

For `picorv32a`, this includes:

* The top-level module (e.g., `picorv32.v`)
* Any submodules used in the design

 These files are used during the **synthesis phase**, where the RTL is converted into a gate-level netlist.

---

### 2. **`config.tcl` File**

* **Purpose:** Defines the **design-specific configuration** for OpenLANE to run the flow.
* **Location:** Typically in the root of the design directory.

 It contains key settings such as:

* Design name and top module
* Clock port and clock period
* Synthesis and placement constraints
* Macro placement, if any
* I/O configurations
* Flow-specific overrides or tool tuning parameters

Example content from `config.tcl`:

```tcl
set ::env(DESIGN_NAME) picorv32a
set ::env(CLOCK_PORT) clk
set ::env(CLOCK_PERIOD) 10.0
```

These settings guide the entire flow—from synthesis to routing.
![Screenshot 2025-05-14 143715](https://github.com/user-attachments/assets/fa76111a-8cc2-4446-b5ff-457fd7fc3151)

---

---

In OpenLANE, multiple configuration files contribute to setting environment variables like the clock period. One of those variables is `CLOCK_PERIOD`, which is used during synthesis, placement, and timing analysis to define how fast the design should run.

In OpenLANE, environment variables like `CLOCK_PERIOD` are set from different configuration files, and the **last loaded value takes precedence**. This variable is essential, as it defines the target clock frequency for synthesis and timing closure.

In your **design-specific `config.tcl`** (for example, in `picorv32a`), the clock period is set as:

```tcl
set ::env(CLOCK_PERIOD) 5.0
```
![Screenshot 2025-05-14 150936](https://github.com/user-attachments/assets/976e1687-047d-447d-8207-271cd2635c88)

This value will override OpenLANE’s internal default settings. However, the platform-specific configuration file:

```
sky130A_sky130_fd_sc_hd_config.tcl
```

also sets a clock period, for example:

```tcl
set ::env(CLOCK_PERIOD) 24.73
```
![Screenshot 2025-05-14 151019](https://github.com/user-attachments/assets/782acb60-95ab-4beb-b697-edcb07429432)

Since this file is sourced **after** your design’s config file during the flow setup, its value (24.73 ns) takes **higher priority**, and **overrides your 5.0 ns setting**.

---

### Result:

Even though the design sets `CLOCK_PERIOD` to 5 ns, OpenLANE ends up using **24.73 ns** from the platform config file, because it’s assigned later in the flow.

---

## Review files after design prep and run synthesis

###  Starting the OpenLANE Flow: Design Preparation

Before beginning synthesis in the OpenLANE ASIC flow, the **design environment must be initialized**. This is known as the **design setup stage**, where OpenLANE prepares all necessary files and directory structures specific to your design.

To do this, we use the following command inside the OpenLANE interactive shell:

```tcl
% prep -design picorv32a
```

###  What This Command Does:

* **Creates a run directory** for the design (e.g., `runs/picorv32a/`).
* **Copies the RTL files** from `designs/picorv32a/src/` into the run workspace.
* **Loads `config.tcl`**, which contains your design constraints, such as clock period, I/O specs, and tool-specific overrides.
* **Applies technology and platform-specific settings**, such as standard cell libraries and PDK configurations.
* **Initializes OpenLANE environment variables** for your design.

Once this setup is complete, the flow is ready to begin the actual RTL-to-GDSII process, starting with **synthesis**.

![Screenshot 2025-05-14 152733](https://github.com/user-attachments/assets/c03a2e9b-c52f-4e99-8904-fe70042fac3a)

NOTE: mergeLef.py is merging the two LEFs ie .lib and tech.lib 
The runs directory has been created in picorv32a along with the date as shown below. All the folder structures inside the runs directory which is required by the openlane is also shown.
inside the tmp we find the merged.lef folder which was created earlier. This file includes all the layer levels, vias and cells information.

![Screenshot 2025-05-14 154231](https://github.com/user-attachments/assets/a180963f-e6f0-4dab-8ade-ab1c30db7283)

Below is the snap showing the contains of runs
![Screenshot 2025-05-14 161709](https://github.com/user-attachments/assets/d11330ba-a189-4a5c-94aa-c61889623f29)

The config.tcl present inside the **'runs'** directory basically shows the default parameters is being taken by the run.
![Screenshot 2025-05-14 162240](https://github.com/user-attachments/assets/8dec90f6-19d5-4892-aa3c-90d1a80c8dc6)

Coming back to openLANE prompt, the next step is **"Synthesis"**
**run_synthesis**

![Screenshot 2025-05-14 164547](https://github.com/user-attachments/assets/4d74a75b-4435-43f6-a1ff-2f32d976d514)

As seen, the WNS = -24ns so the slack is not met (we will fix it post route)
---
## OpenLANE Project Git Link Description
In this lecture Kunal Sir has explained us how to access the information related to OpenLANE and study full potential of this specific tool.
---
## Steps to characterize synthesis results
---
The chip area for module picorv32a was found to be **236829.638400**
The following **results** have been generated after successful Synthesis
![Screenshot 2025-05-15 132328](https://github.com/user-attachments/assets/9d1f4c00-2be7-47ab-bc18-f82c92f26960)

The following **reports** have been generated after successful synthesis .
![Screenshot 2025-05-15 132606](https://github.com/user-attachments/assets/31378b0f-d563-411a-86ae-9692549f0631)
Note: The reports are always generated in a chronological order so the last report generated by the vosys gives us the actual synthesis statistical report.
![Screenshot 2025-05-15 132917](https://github.com/user-attachments/assets/48af9129-22d5-4f87-9ae6-f00bb071ef47)
The **flip-flop ratio** is typically calculated as the ratio of the number of flip-flops to the total number of standard cells in a digital design. It's a useful metric for estimating how much of a digital design is sequential (flip-flops) versus combinational logic.

## Flip-Flop Ratio Calculation

### Given:
- **Number of D Flip-Flops (D FFs)**: `1613`
- **Total Number of Cells**: `18036`

### Formula:
{Flip-Flop Ratio} = {Number of Flip-Flops}/{Total Number of Cells}


### Calculation:
{Flip-Flop Ratio} = {1613}/{18036} =0.0894


### Result:
**Flip-Flop Ratio** ≈ `0.089` or **8.94%**

>  **Interpretation**: Approximately **8.94%** of the standard cells in the design are D flip-flops, indicating the proportion of sequential logic.

---
# Day 2 - Good floor planning considerations
---
## Chip Floor planning consideration
---
### Utilization factor and aspect ratio
---
##  **Step 1: Define Width and Height of Core and Die**

Physical Design begins with **floorplanning**, where we define the **dimensions of the chip**, i.e., the **core** and the **die**.

---

###  What is a Netlist?

A **netlist** is a textual representation of a digital circuit. It lists all the components (like **standard cells** and **flip-flops**) and the **connections (nets)** between them.

In simple terms:

* Think of the netlist as the blueprint or connectivity list of the design.
* It tells which gates are used and how they’re connected.

![Screenshot 2025-05-15 140941](https://github.com/user-attachments/assets/0c590691-fddc-47c2-bdfc-e9530e21c05c)

---

###  Understanding Logic Elements:

* **Standard Cells**: These are predefined logic gates like AND, OR, NOT, NAND, etc. They are used to build combinational logic.
* **Flip-Flops (FFs)**: These are **registers** used for storing state. They are sequential elements.

So:

*  AND, OR, NAND → **Standard Cells**
*  D Flip-Flop → **Register (Sequential Element)**

---

###  Starting the Area Estimation:

Assume:

* Each **standard cell** and **flip-flop** occupies **1 square unit** of area.

![Screenshot 2025-05-15 141201](https://github.com/user-attachments/assets/12ae41f2-fb28-4d76-a8d6-59fe94cc1be6)

We have:

* **2 standard cells**
* **2 flip-flops**

So, total area occupied by the netlist =
 **2 (std cells) + 2 (FFs) = 4 square units**

This is the **minimum area** that the logic can occupy **without considering spacing, power straps, buffers, etc.**

![Screenshot 2025-05-15 141525](https://github.com/user-attachments/assets/7feefae6-18fb-429e-86d8-b07d7ff0ac43)

---

###  What is Die?

The **die** is the physical piece of silicon on which the entire chip is implemented. It is cut from a **silicon wafer** during manufacturing.

###  What is Core?

The **core** is the inner portion of the die where **logic cells (gates and FFs)** are placed.

* Logic is **placed inside the core**.
* The core is surrounded by other regions (e.g., IO pads, power rings).

![Screenshot 2025-05-15 141821](https://github.com/user-attachments/assets/f3f76aac-ec77-43b0-ba09-b8a4a6eec569)

---

###  What is Utilization Factor?

**Utilization Factor** is defined as:

$$
\text{Utilization Factor} = \frac{\text{Area occupied by standard cells and FFs}}{\text{Total core area}}
$$

It tells us how much of the **core area** is filled with actual logic.

![Screenshot 2025-05-15 141941](https://github.com/user-attachments/assets/755b2a46-6c70-4aa5-901b-625b0c97956f)

---

###  Example Calculation:

Assume the **core area = 4 square units**
Area of all std cells and FFs = 4 square units

So,

$$
\text{Utilization Factor} = \frac{4}{4} = 1 \quad \text{(or 100%)}
$$

This is **utilization factor = 1**.

![Screenshot 2025-05-15 142023](https://github.com/user-attachments/assets/5695b756-6b89-4ed5-b161-4621ea3a34df)

![Screenshot 2025-05-15 142037](https://github.com/user-attachments/assets/7381f19c-d39c-457f-832f-90ce57fa8dd3)

---

###  But Practically?

We **never use 100% utilization** because:

* We need space for **routing**, **buffers**, **clock tree**, **spare cells**, etc.

So **practical utilization** is:

* **60% to 80%** in most designs.
* Sometimes up to 85%, depending on design complexity and routing congestion.

---

###  What is Aspect Ratio?

**Aspect Ratio** is:

$$
\text{Aspect Ratio} = \frac{\text{Height of Core}}{\text{Width of Core}}
$$

It defines the **shape** of the core.

---

###  Aspect Ratio for Our Case:

Assume:

* Height = 2 units
* Width = 2 units

So,

$$
\text{Aspect Ratio} = \frac{2}{2} = 1
$$

This is a **square-shaped** core.
An **aspect ratio of 1** is preferred because:

* It makes **routing easier**
* Reduces wirelength and congestion

---

## Concept of pre-placed cells
---

### **Next Step in Floorplanning: Defining the Location of Pre-placed Cells**

The next major step in floorplanning is to **define the location of pre-placed cells**, which must be positioned **prior to automated placement and routing**.

---

### **What Are Pre-placed Cells?**

**Pre-placed cells** refer to blocks or macros whose placement is **manually specified** before the automated place-and-route (PnR) flow begins. These typically include large functional units or IPs that are either reused or require specific physical constraints for performance, area, or integration reasons.

---

### **Example: Reused Combinational Logic**

Consider a large **combinational logic block**, such as a **multiplier** or a **MUX-based selector**, that implements a specific function and occupies around **50K–100K gates**. If this logic is instantiated **multiple times** within the top-level design, instead of re-synthesizing and re-placing it repeatedly, a more efficient approach is adopted:

![Screenshot 2025-05-15 150448](https://github.com/user-attachments/assets/1730545f-63a5-448d-a5cb-cfe8eac86bcf)

1. **Modularization**: The combinational logic is isolated from the main RTL and synthesized independently.
2. **Partitioning**: If needed, the logic is partitioned into smaller sub-blocks (e.g., two independent modules).

    ![Screenshot 2025-05-15 150614](https://github.com/user-attachments/assets/81bb177a-09a5-4849-9aeb-0176919096cc)

3. **I/O Extension**: Each sub-block is equipped with defined I/O pins to interface with the top-level.
4. **Hardening**: These sub-blocks are implemented and verified separately.
5. **Black-boxing**: At the top level, these modules are instantiated as **black boxes** with known dimensions and pin locations.

6. ![Screenshot 2025-05-15 150727](https://github.com/user-attachments/assets/430ece16-5c14-4073-bf9e-e447639608d7)

9. **Reuse**: These blocks can now be **replicated** multiple times in the design without redoing implementation, allowing **resource and area reuse**.

7. ![Screenshot 2025-05-15 150743](https://github.com/user-attachments/assets/618f4e79-59a5-497f-a5b0-babaee6d8bb2)

---

### **Advantages of Pre-placed Cells (Hard Macros)**

* **IP Reusability**: Once implemented, a block can be reused across the same design or different designs.
* **Design Scalability**: Reduces implementation effort for large, repeated structures.
* **Predictable Physical Characteristics**: Timing, power, and area of these cells are known beforehand.
* **Controlled Placement**: Helps in managing congestion and timing near critical paths.

---

### **Common Examples of Pre-placed Cells**

* **Memory macros** (SRAM, ROM)
* **Clock-gating cells**
* **Analog/RF blocks**
* **Multipliers, comparators, or MUX logic (as reused IP)**
* **Third-party hard IPs (e.g., PLL, SerDes)**

![Screenshot 2025-05-15 151125](https://github.com/user-attachments/assets/909c176c-f356-4f6a-b3c2-4e07196c5f60)

---

### **Why Are They Called Pre-placed Cells?**

They are called **pre-placed** because:

* Their **locations are fixed during the floorplanning phase**, before standard cell placement.
* Their **physical properties are rigid** (pre-characterized height/width and pin locations).
* They must be strategically placed to ensure **power delivery**, **clock connectivity**, and **timing closure** without causing **routing blockages** or **congestion hotspots**.

---

### **What is Floorplanning?**

**Floorplanning** is the process of defining the physical organization of the chip before placement and routing. This includes:

* Defining **core and die area**
* Specifying **placement regions** for major blocks
* Placing **pre-placed cells/macros**
* Planning **power grids**, **clock distribution**, and **I/O pad locations**

Pre-placed cells are a critical component of floorplanning. They serve as **anchor points** around which the rest of the placement and routing is organized.

---
## De-coupling capacitors
---

### **Defining the Location of Pre-placed Cells**

In floorplanning, after determining the dimensions of the die and the core, the **next critical step** is to define the **location of pre-placed cells**.

---

### **What are Pre-placed Cells?**

**Pre-placed cells** (also known as **hard macros**) are blocks whose:

* **Functionality** is pre-designed,
* **Physical layout** is fixed (including size and I/O pin locations),
* **Placement** is manually defined **before automated placement** of standard cells.

These are typically **IP blocks**, **memories**, **large combinational or sequential logic blocks**, or **reused modules**.

---

### **Example: Blocks A, B, and C**

Assume **Block A**, **Block B**, and **Block C** are pre-placed cells in a given SoC or ASIC design.

* Each of these blocks is **implemented once**, meaning their layout and implementation are finalized.
* They are **instantiated multiple times** in the main design wherever needed — a concept known as **module reuse** or **macro replication**.

---

### **Placement Strategy: Proximity to I/O Pins**

Assume the design contains a background **core area** surrounded by **I/O pads**.

If:

* Blocks A, B, and C **communicate frequently with input pins**, then it is optimal to **place them closer to the input side of the chip**.
* This reduces **wirelength**, **signal propagation delay**, and **loading**, and improves **timing closure**.

![Screenshot 2025-05-16 123943](https://github.com/user-attachments/assets/e07a815d-208d-4dc5-aed9-9d90b8f51700)

---

### **Immutability of Pre-placed Cells**

Once pre-placed cells are positioned in the floorplan:

* Their locations become **fixed and unmovable** for the rest of the design cycle.
* Any change in their position may require **re-floorplanning** or **re-implementation**, affecting the entire layout and timing.

This is because these blocks:

* Have fixed **physical characteristics**
* Influence **power, clock, and signal distribution**

---

### **Decoupling Capacitors Around Pre-placed Cells**

After placing pre-placed cells, it's essential to **surround them with decoupling capacitors (decaps).**

![Screenshot 2025-05-16 133546](https://github.com/user-attachments/assets/4084c7c3-0945-4b53-b477-6fc28636713f)

---

### **Why Do We Need Decoupling Capacitors?**

**Decoupling capacitors** act as **local charge reservoirs** that:

* **Stabilize the power supply** to nearby logic.
* Provide **instantaneous current** during fast switching.
* Reduce **IR drop** and **ground bounce**.

---

### **Relation to Noise Margin**

In digital circuits, the **noise margin** defines how much noise a logic signal can tolerate before it is misinterpreted.

If the power supply experiences:

* **Voltage fluctuations** (due to sudden switching of pre-placed cells),
* It causes **variation in threshold voltages** and may push logic levels outside valid high/low ranges.

This results in:

* **Reduced noise margin**
* **Increased susceptibility to errors**
* **Timing violations or glitches**

**Decoupling capacitors** help to:

* Minimize these power supply fluctuations
* Maintain stable voltage levels
* **Preserve noise margins** and ensure signal integrity

![Screenshot 2025-05-16 132839](https://github.com/user-attachments/assets/39187cc6-0996-4f7e-ade5-15d43378a29a)
![Screenshot 2025-05-16 133105](https://github.com/user-attachments/assets/e6806a29-cf04-4cca-b41b-b740dd9abe7e)
![Screenshot 2025-05-16 133144](https://github.com/user-attachments/assets/b49187fd-f9cc-43d0-9345-9733954685e4)
![Screenshot 2025-05-16 133333](https://github.com/user-attachments/assets/80a8bafd-410c-4c63-80f4-c8c395ce087b)

---
# Power planning
---

### **Role of Decoupling Capacitors and the Need for Power Planning**

Once a **decoupling capacitor** is placed near a specific block (or macro), it acts as a **local charge reservoir** for that circuit. Let’s explore how this plays out when the macro is reused multiple times and how it relates to **power integrity** and **power planning**.

---

### **Scenario: Repeated Macro Instances**

Assume a macro is instantiated **four times** across the chip. Each instance:

![Screenshot 2025-05-16 140059](https://github.com/user-attachments/assets/7b69d49d-0030-47b8-ba27-ecb3e8023a0b)

* Performs the same logic
* Has its own dedicated **decoupling capacitors**
* Is powered by a common VDD and VSS supply network

Now, consider a **driver** in one macro instance sending a signal to a **load** in another macro instance. This signal traverses across a **16-bit bus**.

To ensure **signal integrity**, the load must receive the **correct signal shape** — matching the driver's output levels — which requires a **stable local power supply**.

---

### **Problem: Inadequate Local Power Near the Interconnect**

Even though each macro has local decaps, the **interconnect region (bus area)** might be far from any VDD/VSS taps or decoupling capacitors.

![Screenshot 2025-05-16 140201](https://github.com/user-attachments/assets/ed6711d6-6b82-4273-bfea-f444f892bf0c)

In this case:

* The **signal integrity** degrades due to **voltage fluctuations**.
* The bus may **not receive full VDD**, especially when many lines switch simultaneously.
* The power supply has to source current over a long distance, introducing **IR drop** and **timing issues**.

---

### **Detailed Analysis: Ground Bounce and IR Drop**

Let’s assume the initial state of the 16-bit bus is:
`1110010111000110`

![Screenshot 2025-05-16 140713](https://github.com/user-attachments/assets/a97da371-3682-431b-9412-40bf73ee0748)

This signal is passed through an **inverter** in the load macro.

**What happens next?**

1. **Discharging High Bits:**

   * Bits at logic '1' must discharge to '0' through **ground (VSS)**.
   * All these transitions discharge through a **single ground tap**.
   * This causes a **current spike**, creating a **temporary rise in ground voltage**, known as **ground bounce**.
   * If this bounce exceeds the **noise margin**, the logic level at the receiver becomes **undefined**.

![Screenshot 2025-05-16 140811](https://github.com/user-attachments/assets/c60e802f-2828-478c-a95d-9f19bed22f17)

2. **Charging Low Bits:**

   * Bits at logic '0' must charge to '1' through **VDD**.
   * All of them charge through a **single VDD tap**.
   * This causes a **voltage drop** at the VDD tap due to sudden current draw, known as **IR drop** or **voltage droop**.
   * This too affects signal integrity, potentially leading to logic errors.

![Screenshot 2025-05-16 141355](https://github.com/user-attachments/assets/088483e5-0dbc-43be-8958-540a008b0c3a)

---

### **Root Cause**

These issues arise because the **power supply is accessed only from a single point**, and the switching current must traverse long resistive/inductive paths in the metal layers.

---

### **Solution: Power Planning**

To mitigate these problems, **robust power planning** is essential. This involves:

* **Distributing power supply taps (VDD/VSS)** throughout the chip
* Ensuring all regions, including interconnect-heavy areas, have **nearby access to power**
* Using **power grids and straps** on higher metal layers to lower resistance
* Strategically placing **decoupling capacitors** near both **macros and routing channels**

![Screenshot 2025-05-16 141606](https://github.com/user-attachments/assets/b57a954b-7fb7-433b-b65e-732bdf9f6ab0)

With proper power planning:

* The 16-bit bus can **draw power locally**, reducing IR drop
* Switching noise is **minimized**, and
* **Noise margins are preserved**, maintaining reliable operation

![Screenshot 2025-05-16 141743](https://github.com/user-attachments/assets/3ec0b739-9561-4d3a-b945-3f4ad9c6de8e)

---

# Pin placement and logical cell placement blockage
---

### **Understanding the Concept of Pin Placement in Floorplanning**

To understand pin placement, let’s consider an example design involving flip-flops, combinational logic, and pre-placed cells.

---

### **Example Circuit Description**

#### **1. Basic Flip-Flop Driven Logic:**

* **FF1** has input **Din1** and clock **Clk1**.
* **FF2** has output **Dout1** and is also clocked by **Clk1**.
* Between FF1 and FF2, some **combinational logic** exists.

#### **2. Replicated Logic Circuit:**

* A similar circuit with:

  * Input **Din2**
  * Output **Dout2**
  * Clock **Clk2**

#### **3. Pre-placed Cells:**

* **Block A** receives **Din1** and **Din2** as inputs.
* **Block B** takes **Clk1** and **Clk2** as inputs and generates a **clock output ClkOut**.

![Screenshot 2025-05-16 144621](https://github.com/user-attachments/assets/f2284d5c-b166-4d9f-b646-426805f68b89)

---

### **3. Additional Timing Scenario — Inter-clock Domain**

Now consider a design section that demonstrates **cross-clock domain interaction:**

#### **Circuit 1:**

* **FF1** takes **Din3** and is clocked by **Clk1**.
* **FF2** produces **Dout3** and is clocked by **Clk2**.

#### **Circuit 2:**

* **FF1** receives **Din4** and **Clk2**.
* **FF2** generates **Dout4** and is clocked by **Clk1**.

This setup is useful for studying **inter-clock timing interactions**, often critical in real SoCs with multiple clock domains.

---

### **Pre-placed Cell (Block C):**

* **Block C** takes **Din3** and **Din4** as inputs.
* The output of Block C is connected to downstream **combinational logic**.

![Screenshot 2025-05-16 145644](https://github.com/user-attachments/assets/f5d3cf93-860f-470a-bafd-4f046167615e)

---

### **Summary of All I/O Ports in the Design:**

| **Port Type**    | **Ports**                  |
| ---------------- | -------------------------- |
| **Input Data**   | Din1, Din2, Din3, Din4     |
| **Clock Inputs** | Clk1, Clk2                 |
| **Output Data**  | Dout1, Dout2, Dout3, Dout4 |
| **Clock Output** | ClkOut                     |

![Screenshot 2025-05-16 145803](https://github.com/user-attachments/assets/895e71f0-cc54-40b2-8521-c08dd11ee16d)

---

### **Pin Placement in Floorplanning**

In the **physical design (PD)** flow, these ports are mapped to physical **pins** located in the area **between the core and the die boundary** (known as the *I/O ring*).

#### **General Placement Trend:**

* **Input pins** are usually placed on the **left side** of the chip.
* **Output pins** are placed on the **right side**.
* This convention helps with **signal flow** and **timing optimization** but is **not mandatory** — pin placement is influenced by the **location of the connected blocks** within the core.

#### **Clock Ports:**

* Clock ports like **Clk1** and **Clk2** are generally **larger than data pins**.
* This is because:

  * Clock nets have **higher fan-out** (they drive many sequential elements).
  * They need **stronger drivers** and **lower skew**, requiring **more robust routing** and **more metal layers**.
  * Wider pins help **minimize resistance**, **IR drop**, and **electromagnetic noise**.

![Screenshot 2025-05-16 150354](https://github.com/user-attachments/assets/105c2abe-3539-4bf0-b4ef-105a58925262)

---

### **Netlist Representation**

* The entire **connectivity between gates and blocks** (including FFs, combinational logic, and macros) is described using **HDL languages** like **Verilog or VHDL**.
* The compiled result is called a **netlist**, which serves as the basis for physical design.

---

### **Placement Blockages and Design Rule Considerations**

* The region between the **core and die** must **not contain any standard cells**.
* This region is reserved for **pads, pins, power straps, ESD structures**, and routing tracks.
* To enforce this, **placement blockages** are defined — these are **logical constraints** that prevent the automated placement and routing tool from placing cells in that area.

![Screenshot 2025-05-16 150835](https://github.com/user-attachments/assets/1d102194-7883-4fcc-8245-2bd1b9c6c2e7)

---

### **Outcome**

Once all:

* Pre-placed cells are located,
* Pins are placed based on connectivity and clock/data separation,
* Blockages are applied,

The **floorplan is complete**, and the design is now ready for the **placement and routing** stage.

---
# Steps to run floorplan using OpenLANE
---
### Variables used in OpenLANE during physical design
---
![Screenshot 2025-05-16 200627](https://github.com/user-attachments/assets/b4441017-b176-48eb-906e-2ed6b0f4cebc)
![Screenshot 2025-05-16 200659](https://github.com/user-attachments/assets/8a54a19d-3dfa-4236-8af5-481f30100195)
![Screenshot 2025-05-16 200738](https://github.com/user-attachments/assets/34650727-df7d-4366-9fa0-3433e7312703)
![Screenshot 2025-05-16 200759](https://github.com/user-attachments/assets/8e45473a-7538-4a2c-b26a-d539342fd168)
![Screenshot 2025-05-16 200825](https://github.com/user-attachments/assets/d9fb0532-bf6d-438b-a57c-9f8ae266a00e)
![Screenshot 2025-05-16 200856](https://github.com/user-attachments/assets/71d95f72-3483-4bd2-8c3e-25190251a99d)
![Screenshot 2025-05-16 200937](https://github.com/user-attachments/assets/ad6d5e5f-ee9f-4540-85e4-c4d207a9abed)
![Screenshot 2025-05-16 201005](https://github.com/user-attachments/assets/88036aa8-13eb-47dc-a93a-65114cb39e8c)
![Screenshot 2025-05-16 201032](https://github.com/user-attachments/assets/db70cdaa-2c85-4396-8503-e8173edbcff0)
![Screenshot 2025-05-16 201051](https://github.com/user-attachments/assets/dfe16e1c-a648-4c69-b22e-2ab6ab4be391)

### **What Happens in Floorplanning?**

The **floorplanning stage** is a key step in the digital physical design (PD) flow. It defines the spatial organization of a chip before standard cell placement and routing begins.

---

### **Key Tasks in Floorplanning:**

1. **Define Die Area**

   * The complete area of the chip, including core, I/O ring, and pad frame.

2. **Define Core Area**

   * The internal area of the chip where standard cells are placed.
   * This area is inset from the die boundary by a defined core margin.

3. **Set Aspect Ratio**

   * The ratio of **width to height** of the core (`aspect ratio = width / height`).

4. **Set Core Utilization Factor**

   * The percentage of the core area to be filled with standard cells.
   * For example, a utilization factor of 0.65 means 65% cell area, 35% left for routing, buffers, and congestion management.

5. **Pin (Input/Output) Placement**

   * I/O ports are placed on the periphery of the core.
   * While the default trend is to place inputs on the left and outputs on the right, pin placement is ideally based on the logical connectivity and location of blocks in the core.

6. **Power Distribution Network (PDN) Planning**

   * Specification of metal layers, tracks, and straps for distributing VDD and VSS across the core.

7. **Macro Placement**

   * Placement of large, pre-designed blocks like SRAMs, PLLs, or other IP blocks.
   * These are usually manually placed early in the flow and are referred to as *preplaced cells*.

---

### **OpenLane Floorplanning Configuration**

In OpenLane, floorplanning behavior is controlled by environment variables defined in TCL configuration files. These variables can be set or overridden at multiple levels.

#### **Floorplanning Variables File:**

* Path: `openlane/configuration/floorplan.tcl`
* This file contains the default floorplan configuration switches.

![Screenshot 2025-05-16 201540](https://github.com/user-attachments/assets/484287e3-d0e8-471e-9ee8-8ac1200b5ba4)

##### Example:

```tcl
set ::env(FP_IO_MODE) 1 ; # 0 = matching mode, 1 = random equidistant
```

---

### **Example Floorplanning Configuration: `FP_IO_MODE`**

In the `floorplan.tcl` file located at `openlane/configuration/floorplan.tcl`, various switches control how the floorplan is generated. One such switch is:

```tcl
set ::env(FP_IO_MODE) 1 ; # 0 = matching mode, 1 = random equidistant
```

#### **Explanation of `FP_IO_MODE`**

This variable defines how the I/O pins are placed on the core periphery during floorplanning.

* `FP_IO_MODE = 0` → **Matching Mode**
  In this mode, the tool attempts to place input/output pins **based on logical grouping and connectivity**.
  For example, related pins (like a bus or interface signals) are grouped and placed adjacent to each other to maintain signal locality and reduce wirelength.

* `FP_IO_MODE = 1` → **Random Equidistant Mode**
  In this mode, the I/O pins are placed **evenly spaced** along the periphery of the core, but their order is randomized.
  This is a simpler scheme that can be useful when there is no initial information about signal grouping or during early prototyping.

#### **Usage Recommendation:**

* Use `mode 0` if you want to optimize for **wirelength and logical proximity**.
* Use `mode 1` for a **uniform, evenly spaced pin layout**, especially in early or exploratory stages of the design.

---

### **Configuration File Priority in OpenLane**

When working on a design such as `picorv32a`, you will find the following files in `openlane/designs/picorv32a/`:

![Screenshot 2025-05-16 201703](https://github.com/user-attachments/assets/69c40f2e-ed86-47e9-86bb-29c54cafa6b9)
![Screenshot 2025-05-16 201638](https://github.com/user-attachments/assets/e00f3cff-0a43-4ad0-96a9-c35e26b1370b)

| File Path                               | Priority (Low to High) | Purpose                      |
| --------------------------------------- | ---------------------- | ---------------------------- |
| `openlane/configuration/floorplan.tcl`  | Lowest                 | Default floorplan script     |
| `openlane/designs/picorv32a/config.tcl` | Medium                 | Design-specific overrides    |
| `sky130A_fd_sc_hd_config.tcl`           | Highest                | Technology-specific settings |

---

### **Example Configuration Values:**

#### From `config.tcl`:

```tcl
set ::env(CORE_UTILIZATION) 65
set ::env(FP_IO_VMETAL) 4
set ::env(FP_IO_HMETAL) 3
```

Note: OpenLane internally uses **one metal layer above** the value specified.
So `FP_IO_VMETAL 4` means **vertical pins will be routed on Metal5**.

#### From `floorplan.tcl` (default):

![Screenshot 2025-05-16 201540](https://github.com/user-attachments/assets/484287e3-d0e8-471e-9ee8-8ac1200b5ba4)

```tcl
set ::env(CORE_UTILIZATION) 50
set ::env(FP_IO_VMETAL) 3
set ::env(FP_IO_HMETAL) 4
```

---

### **Running the Floorplan Step**

After defining or adjusting the configuration variables, the floorplan can be generated using:

```bash
run_floorplan
```

This will:

* Initialize the die and core boundaries.
* Place pins along the I/O ring.
* Insert macros in pre-specified locations.
* Create blockages and define regions for standard cell placement.
* Lay the groundwork for the power network and subsequent routing.

![Screenshot 2025-05-16 222040](https://github.com/user-attachments/assets/54326547-24a2-478a-b9b8-8d12ea5d0454)

---
# Review floorplan files and steps to view floorplan
---

After **run_floorplan** go to openlane/design/picorv32a/runs and go into your latest runs. You will find config.tcl file here which will tells us all the configurations taken by the flow.
![Screenshot 2025-05-16 224923](https://github.com/user-attachments/assets/cdb23741-c787-4a86-841a-6e4e00060f40)
inside this config.tcl you can re check the **set ::env(FP_IO_VMETAL)** and **set ::env(FP_IO_HMETAL)** which will match with the content present in floorplan.tcl.

![Screenshot 2025-05-16 224134](https://github.com/user-attachments/assets/a83fb032-ed5b-47b6-932f-54b967ea0ecb)
![Screenshot 2025-05-16 230317](https://github.com/user-attachments/assets/7fb2b564-be9e-4777-8fd0-b1714cadf026)

VERY IMPORTANT POINT:


| File Path                                                | Priority (Low to High) | Purpose                      |
| -------------------------------------------------------- | ---------------------- | ---------------------------- |
| `openlane/configuration/floorplan.tcl`                   | Lowest                 | Default floorplan script     |
| `openlane/designs/picorv32a/config.tcl`                  | Medium                 | Design-specific overrides    |
| `openlane/designs/picorv32a/sky130A_fd_sc_hd_config.tcl` | Highest                | Technology-specific settings |

in openlane/configuration/floorplan.tcl the variables set were 
**set ::env(CORE_UTILIZATION) 50**
**set ::env(FP_IO_VMETAL) 3**
**set ::env(FP_IO_HMETAL) 4**
and the above variables were not set in **openlane/designs/picorv32a/config.tcl** and **openlane/designs/picorv32a/sky130A_fd_sc_hd_config.tcl**. Hence the flow tool the values from floorplan.tcl but if the variables were defined in **openlane/designs/picorv32a/sky130A_fd_sc_hd_config.tcl** then these values would have been considered as this is given highest priority.
For example in **/openlane/configurations/floorplan.tcl** **set ::env(FP_CORE_UTIL) is 50** 

![Screenshot 2025-05-16 231940](https://github.com/user-attachments/assets/5eb4068e-ed28-4332-bdce-338255a4d31d)

and in **openlane/designs/picorv32a/runs/sky130A_fd_sc_hd_config.tcl **set ::env(FP_CORE_UTIL) is 35**

![Screenshot 2025-05-16 232538](https://github.com/user-attachments/assets/2ef3d080-2b1a-4486-9459-ec27a44bbae9)

and highest priority is given to the later.
Now finally after floorplanning **set ::env(FP_CORE_UTIL) is 35** ( check in openlane/design/picorv32a/runs/16-06_16-47/config.tcl)

![Screenshot 2025-05-16 233221](https://github.com/user-attachments/assets/9c2d546c-b08c-46d5-bc91-54c42a8d3d36)
---
Now, our floorplan stage is complete and we would like to view our floorplan, for that go to openlane/designs/picorv32a/runs/16-06_16-47/results/floorplan. We will find a .def file (Design exchange format)
![Screenshot 2025-05-18 113606](https://github.com/user-attachments/assets/8ca5e0d7-7d09-4a8a-bac9-f75a7680d778)

Contents of the picorv32a.floorplan.def
![Screenshot 2025-05-18 114333](https://github.com/user-attachments/assets/ee20752f-6ad2-4388-8d20-222db853de53)

### **Understanding `DIEAREA` in DEF File**

In a DEF (Design Exchange Format) file, the `DIEAREA` statement defines the **physical boundary of the die**—i.e., the total rectangular area available on the silicon for placement of all components.

#### **Syntax:**

```
DIEAREA (x1 y1) (x2 y2);
```

* `(x1, y1)` – Coordinates of the **lower-left corner** of the die.
* `(x2, y2)` – Coordinates of the **upper-right corner** of the die.
* All values are in **Database Units (DBUs)**.

#### **Example:**

```
DIEAREA (0 0) (660685 671405);
```

This means:

* Lower-left corner: (0, 0)
* Upper-right corner: (660685, 671405)

---

### **Units in DEF File**

The DEF file also defines the database unit scale with:

```
UNITS DISTANCE MICRONS 1000;
```

This means:

* **1 micron = 1000 DBU**
* To convert from DBU to microns:

  $$
  {microns} = {DBU}/{1000}
  $$

---

### **Convert DIEAREA Dimensions to Microns**

* **Width** = 660685 ÷ 1000 = **660.685 μm**
* **Height** = 671405 ÷ 1000 = **671.405 μm**

---

### **Calculate Chip Area**

$$
\text{Area} = \text{Width} \times \text{Height}
= 660.685 \times 671.405 = 443554.61 \, \mu m^2
$$

---

### **Final Summary**

* **Chip Width**: 660.685 μm
* **Chip Height**: 671.405 μm
* **Chip Area**: 443,554.61 μm² (approximate)
---
---

### **Viewing Floorplan in Magic**

To view the floorplan in **Magic VLSI layout tool**, follow the steps below using the appropriate paths from your setup.

---
![Screenshot 2025-05-18 121428](https://github.com/user-attachments/assets/d39275f4-4675-4b30-92ea-a6662032ee19)

### **1. Launch Magic with the Technology File**

Start Magic by explicitly specifying the Sky130A technology file path:

```bash
magic -T /home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech &
```

This loads the Sky130A technology rules required for rendering and design-rule enforcement.

---

### **2. Read the Merged LEF File**

Once Magic launches, in the Magic console, load the **merged LEF** file, which contains macro and standard cell abstracts:

```tcl
lef read ./../tmp/merged.lef
```

Make sure you run this from the correct working directory where the `tmp` folder is accessible using this relative path.

---

### **3. Read the DEF File**

Next, read the floorplan DEF file:

```tcl
def read picorv32a.floorplan.def
```

This will load the complete physical design including standard cell rows, block placements, I/O pin positions, and more.

---

### **4. Final Layout View**

Once the DEF is read, Magic will render the floorplan layout. You can now:

* Zoom in/out using mouse scroll or `:` + `zoom`
* Select layers, cells, or macros for inspection
* Toggle layers or check routing overlays

![Screenshot 2025-05-18 134631](https://github.com/user-attachments/assets/43c00c23-9b5b-4219-8293-3851e8596b1f)

---
# Review floorplan layout in Magic
---
Now we can see our layout.
Note: To select layout : press s
      To fit layout on screen : press v
---

### **Interacting with the Floorplan in Magic**

After successfully loading the LEF and DEF files in Magic, you can interact with the layout using the following features:

---

### **1. Zoom In the Layout**

To zoom into the layout:

* Simply press **`z`** on your keyboard while in the layout window.

This allows you to get a closer view of specific layout features like pins, cells, or block boundaries.

---

### **2. Visualizing Pin Placement Mode**

Earlier, we set the input-output pin placement mode in the `floorplan.tcl` file as:

```tcl
set ::env(FP_IO_MODE) 1  ; # 1 = random equidistant mode
```
![Screenshot 2025-05-18 135747](https://github.com/user-attachments/assets/1f686a5e-b24e-481b-8ce3-48043215d947)

This means:

* The input/output pins will be **evenly spaced randomly** around the core boundary.
* You can visualize this distribution directly in the Magic floorplan layout.

---

### **3. Selecting Objects in the Layout**

To select an object (e.g., an input pin):

* Move your **cursor over the object** and press **`s`** (select).
* The selected object will be highlighted in the layout.
Here i have selected a Horizontal input pin
![Screenshot 2025-05-18 140028](https://github.com/user-attachments/assets/256cc6fa-1c7d-4b3a-a4df-de5e20eacd74)

---
### **4. Getting Object Information**

Once an object is selected:

* Go to the **`tkcon` window** (Magic’s console).
* Type:

```tcl
what
```
![Screenshot 2025-05-18 140253](https://github.com/user-attachments/assets/28aab061-4ac7-41f8-9097-a67528fbd2e8)
As set in floorpln.tcl set ::env(FP_IO_HMETAL) 4

Similarly selecting an horizontal pin 
![Screenshot 2025-05-18 141926](https://github.com/user-attachments/assets/6bf82d81-fc22-45bd-b404-dabf9a496a5a)
* Go to the **`tkcon` window** (Magic’s console).
* Type:

```tcl
what
```
![Screenshot 2025-05-18 141952](https://github.com/user-attachments/assets/7bfff745-2596-48e8-8093-e6eac208e7c4)
As set in floorpln.tcl set ::env(FP_IO_VMETAL) 3

This command will output detailed information about the selected object, such as:

* Pin name
* Type (input/output/clock)
* Layer information
* Location coordinates

---
Studying the details of the layout:
![Screenshot 2025-05-18 175905](https://github.com/user-attachments/assets/0bbfea65-c0f5-4e58-85aa-08440504ae75)

The IO Pins are placed equdistant because we had set the it earlier in mode 1 in floorpla.tcl
`FP_IO_MODE = 1` → **Random Equidistant Mode**
  In this mode, the I/O pins are placed **evenly spaced** along the periphery of the core, but their order is randomized.
  This is a simpler scheme that can be useful when there is no initial information about signal grouping or during early prototyping.

---

### **1. Decap Cells (Decoupling Capacitor Cells)**

**Decap cells** are special standard cells that consist primarily of large capacitive structures (typically connected between VDD and GND) and are used to:

![Screenshot 2025-05-18 174245](https://github.com/user-attachments/assets/9fad6408-1cce-42e3-8502-922c1282f7a3)

* Provide **local charge storage**.
* **Stabilize power supply** fluctuations due to dynamic switching.
* **Reduce IR drop** and **suppress ground/VDD noise** (e.g., voltage droop, ground bounce).

They do **not perform any logical function**, but act like **local reservoirs of charge** during sudden switching activity (transients).

---

### **2. Tap Cells**

**Tap cells** are special cells used to ensure proper connection of **n-well** or **p-substrate** to the **power supply (VDD/VSS)**.

In bulk CMOS:

* **N-well** regions need to be connected to **VDD**.
* **P-substrate** needs to be connected to **GND**.

If this is not done at regular intervals:

* **Latch-up** can occur.
* Devices may **float** and behave unpredictably.

* Tap cells provide these substrate/well contacts and are inserted periodically.

![Screenshot 2025-05-18 174535](https://github.com/user-attachments/assets/5d8cbb68-94c4-4b1d-b3d5-70b08e614ae9)

---

### **3. Why Are Tap Cells Placed Diagonally and Equidistantly?**

* Tap cells are typically placed **diagonally or in a grid**, ensuring **equidistant coverage** across the chip.
* This uniform distribution guarantees that **every region** of the layout is close enough to a substrate/well connection.
* The spacing is controlled to meet **DRC** and **reliability constraints** (e.g., minimum distance between substrate contacts).
* The placement strategy is usually set automatically by the **floorplanning or placement tool**.

---

### **4. Floorplan and Standard Cells**

* **Floorplanning** defines:

  * **Core and die area**
  * **IO placement**
  * **Macro placement**
  * **Power planning**
  * **Blockages**
  * But **not the placement of standard cells**

* Standard cells are placed later in the **placement** step.

However:

* In tools like **OpenLane**, before placement begins, some standard cells may appear in the **lower-left corner** of the core area.
  This is the **default location** where the tool initially dumps unplaced cells.

![Screenshot 2025-05-18 175236](https://github.com/user-attachments/assets/1e0c9cbb-c2f3-4d9f-aad5-b2e35047e9dc)

* This is not their final location and will be resolved in the **automated placement** step.
---

# Library building and Placement
---
## Netlist binding and initial place design
### Placement and Routing

**Step 1: Bind Netlist with Physical Cells**
All gates have a uniform block-like shape in physical form. These blocks (gates) are defined in the library. The library contains all necessary timing information, such as gate delays. It also specifies the width and height of each cell, along with the required conditions. Multiple physical shapes of the same gate are available in the library. The library offers different sizes for a particular gate — larger gates have lower resistance and are therefore faster. Thus, the library includes different versions (flavours) of the same gate.

![Screenshot 2025-05-20 131144](https://github.com/user-attachments/assets/48fdf5a9-7015-4c64-b86d-aaca9beaeb2c)
![Screenshot 2025-05-20 131127](https://github.com/user-attachments/assets/f9f56d15-6c4a-4611-9674-067f3ae6fbf2)
![Screenshot 2025-05-20 131219](https://github.com/user-attachments/assets/6043695b-8553-4263-8437-8771859c168f)
![Screenshot 2025-05-20 131804](https://github.com/user-attachments/assets/2ede6fc0-9ad6-4a4f-b9d9-ee22299a3a22)

Once the appropriate shapes and sizes are assigned to each gate, they are placed onto the floorplan.

![Screenshot 2025-05-20 132258](https://github.com/user-attachments/assets/e9b01dc4-592a-43ce-a6f2-f4c7388c2f45)

### Summary So Far

We now have a well-defined floorplan with input and output ports properly placed. A netlist is available, and every gate in the netlist has an assigned physical shape and size — giving us a physical view of the logic gates.

![Screenshot 2025-05-20 132338](https://github.com/user-attachments/assets/7223c26c-77fc-4f23-a12e-c25b3c98fe17)

### Next Step: Place the Netlist into the Floorplan

The netlist is now placed onto the floorplan. Some cells are already pre-placed, and during placement, these cells remain fixed. No new cells are placed in those regions.

Cells are positioned based on the locations of their input and output ports to meet timing requirements.

* Some cells are abutted (placed directly next to each other).
* Some cells are spaced further apart due to the distance between their input and output ports. This results in an optimized placement.

Optimized placement makes estimations such as wire length and capacitance and, based on those estimations, repeaters may be inserted.

![Screenshot 2025-05-20 133124](https://github.com/user-attachments/assets/0ef80da3-d3c2-4576-bbdc-3e21c22d196a)

----
### Optimize placement using estimated wire-length and capacitance
---
In this stage, wire length and capacitance are estimated. Based on these estimations, repeaters (buffers) are inserted.

**How repeaters help (Signal Integrity Concept):**
Repeaters are buffers that restore the degraded signal by regenerating a new signal identical to the original. Over long wires, signals experience degradation due to resistance and capacitance. This leads to slower transitions, increased delay, and potential signal integrity issues. Repeaters recondition the signal at intervals, maintaining sharp transitions and timing accuracy. This ensures reliable signal transmission across long interconnects. However, inserting repeaters increases area usage.

**Why capacitance is higher for longer wires:**
Capacitance is proportional to the wire length. Longer wires have more surface area adjacent to other conductors (wires or substrate), resulting in higher parasitic capacitance. This increased capacitance slows down signal propagation and increases delay.

![Screenshot 2025-06-18 120923](https://github.com/user-attachments/assets/f6214de1-f218-4bf8-8829-6151100da95a)

---
### Final placement optimization
---
**Why some cells are abutted:**
Certain logic cells are abutted to eliminate or minimize time delay between signals. Abutment reduces interconnect length, thus lowering delay and improving timing. This is especially important for logic operating at very high frequency, where even small delays can cause timing violations. Placing such logic close together ensures faster signal transfer.

**Why hold timing analysis is not done after placement:**
Hold timing analysis is not meaningful at this stage because it depends on actual delays in the clock network, which is not yet implemented. Since the clock is still ideal (i.e., assumed to have zero skew and zero delay), hold timing violations cannot be evaluated accurately.

**What is an ideal clock:**
An ideal clock is a theoretical clock with perfect characteristics — zero propagation delay, zero skew, and perfect edge alignment across the design. It does not model the real-world effects of clock distribution.

**Why setup timing analysis is done after placement:**
Setup timing analysis checks whether signals arrive at their destination registers before the clock edge. With estimated data path delays available after placement, setup timing analysis helps verify whether the placement meets required timing specifications. It ensures the design can operate at the target frequency.
---
### Need for libraries and characterization
---
**Need for Characterization**

Every design follows a standard IC design flow to be implemented on silicon.

**Logic Synthesis:**
This is the first step where the high-level functional description written in RTL (Register Transfer Level) is converted into a gate-level netlist. Logic synthesis maps the RTL code into a network of logic gates that performs the same functionality as described.

**Output of Logic Synthesis:**
The result is a gate-level netlist — a structured arrangement of standard logic gates that replicate the behavior of the original RTL design.

**Floorplanning:**
In this step, the gate-level netlist is imported, and the physical design begins by defining the size of the core and the die. The placement of I/O ports and major blocks is also decided here.

**Placement:**
Logic cells from the netlist are placed physically on the chip. The objective is to ensure that the initial timing requirements are met by placing cells in optimal positions.

**Clock Tree Synthesis (CTS):**
This step involves creating a clock distribution network. The goal is to minimize clock skew by ensuring that all flip-flops receive the clock signal simultaneously.

**Routing:**
This step connects the placed cells with metal interconnects as per the netlist, completing all required paths for data and clock signals.

**Static Timing Analysis (STA):**
Both setup and hold timings are analyzed in this step. The design is evaluated to ensure that all timing constraints are met under various process and environmental conditions.

**Need for Characterization:**
In all these steps, one common element is the use of **gates or cells**. For the design tools to correctly interpret and use these gates, they must be fully characterized.
**Library characterization** provides detailed information about each gate's behavior — including delay, power, area, input/output transition times, and timing arcs — across different operating conditions. Without this data, the tools cannot accurately perform synthesis, placement, CTS, routing, or timing analysis. Hence, characterization is essential for the tools to correctly understand and use the gates throughout the design flow.
---
### Congestion aware placement using RePlAce
---

**Placement Stage (Post-Floorplanning)**

After floorplanning, the next stage is **placement**. In this stage, we focus on **congestion-aware placement**, not timing-aware placement. The main goal here is to reduce **congestion** across the chip layout.

In **OpenLane**, placement is done in two stages:

### 1. **Global Placement**

* This is a **coarse placement** stage.
* There is **no legalization** at this point.
* The main objective is to minimize **wirelength** using the **HPWL (Half-Perimeter Wire Length)** metric.
* The OpenLane command for this step is: `run_placement`.
* Multiple iterations are run during global placement.
* With each iteration, the **overflow (OVFL)** — a measure of placement congestion — should **converge** (i.e., reduce toward zero).

### 2. **Detailed Placement**

* This stage includes **legalization**.
* **Legalization** ensures the following:

  * Standard cells are placed **inside standard cell rows**.
  * Cells must be **abutted** (placed directly next to each other with no unnecessary gaps).
  * There must be **no overlaps** between cells.
* Legalization ensures that the placement is **physically valid and manufacturable**.

### Final Check

* After placement and legalization, **legality checks** must be run to verify:

  * All standard cells are inside standard cell rows.
  * No overlaps exist.
  * Cells are abutted where required.
* If everything is legal and overflow is within acceptable limits, the placement stage is considered successful.

---

Now after floorplan, lets invoke openlane and perform run_placement.

![image](https://github.com/user-attachments/assets/b2ce041e-9ece-497a-8ae2-83afd51b271e)
![image](https://github.com/user-attachments/assets/a88974c7-f149-45b2-b0c9-bc05f33ba229)


To view our placement, invoke the same sky130A.tech file and the same merged.lef file but this time our def file will be picorv32a.placement.def

![Screenshot 2025-06-18 133228](https://github.com/user-attachments/assets/bd33be86-ead5-40e9-884a-65bc0b132106)

![Screenshot 2025-06-18 133444](https://github.com/user-attachments/assets/2369854a-7be9-4743-958a-a9e9814aae78)

Zooming in we can see the placement of the standard cells in the standard cell rows

![image](https://github.com/user-attachments/assets/33b79077-2db1-4c34-82b2-b2fd1e5b48f8)

---
## Cell design and characterization flows
---
### Inputs for cell design flow 
---
**Cell Design Flow**

Every **standard cell** — such as AND, OR, buffer, inverter, D flip-flop, latch, and ICG — goes through a typical **cell design flow** before it can be used in digital IC design. These cells are stored in the **standard cell library**, which includes:

* Different **functionalities**
* Various **drive strengths** (sizes)
* Multiple **threshold voltages (Vt)** for power-performance tradeoffs

![Screenshot 2025-06-18 150848](https://github.com/user-attachments/assets/bb73cb81-4236-425e-8ae7-fa521ef8501a)

### Example: Inverter

The **cell design flow** is divided into three main stages:

![Screenshot 2025-06-18 153146](https://github.com/user-attachments/assets/f30afe68-6a60-45c7-a87a-e26e9c84c5d5)

---

### **1) Inputs** *(Required for Designing the Standard Cell)*

* **PDKs (Process Design Kits):**

  * Contains **DRC (Design Rule Check)** and **LVS (Layout vs Schematic)** rules
  * Also includes **SPICE models** for simulation
* **Library Specifications:**

  * Constraints on area, delay, power, etc.
* **User-defined Specifications:**

  * Functional behavior, target drive strength, input capacitance, etc.

![Screenshot 2025-06-18 153446](https://github.com/user-attachments/assets/ef969b20-8282-47d4-bf1d-06ad3bf0aa5e)
![Screenshot 2025-06-18 153555](https://github.com/user-attachments/assets/852ee4f9-4834-4956-9c8a-7e47f10e08fb)
![Screenshot 2025-06-18 153910](https://github.com/user-attachments/assets/5981d8d3-e7bf-40c4-ab66-6021c62b8aa2)
![Screenshot 2025-06-18 153927](https://github.com/user-attachments/assets/6f593322-1896-4679-91ae-f49906ebea52)
![Screenshot 2025-06-18 154053](https://github.com/user-attachments/assets/c02fa695-0132-4a51-b7d8-1287dfd87cf5)
![Screenshot 2025-06-18 154111](https://github.com/user-attachments/assets/5987fd30-4d6a-4d89-9b8d-c640357220c4)
![Screenshot 2025-06-18 154130](https://github.com/user-attachments/assets/5e20f74c-5097-4057-af37-d00b28c6165d)

---

### **2) Design Steps** *(Core Design Process)*

* **Circuit Design:**
In circuit Design there are two steps.
First step is to implement the function itself and second step is to model the PMOS nad NMOS transistor in such a fashion in order to meet the libraray.

  * Transistor-level design using SPICE
  * Outputs a **circuit description** (e.g., netlist in Verilog or SPICE)

![Screenshot 2025-06-18 154433](https://github.com/user-attachments/assets/89b1bcf7-09d3-43d9-b5f9-5ec59a7ed293)


* **Layout Design:**
  In Layout Design First step is to get the function implemented through the MOS transistor through a set of PMOS and NMOS transistor and the second step is to get the PMOS network graph and the nNMOS network graph out of the design that has been implemented.

  * Physical layout of the cell respecting DRC
  * Perform **LVS** to ensure layout matches the schematic
  * Extract parasitics and generate **GDSII** and **extracted SPICE netlist (.cir)**

After getting the network graphs next step is to obtain the Euler's path. Eule's path is basically the path which is traced only once.

![Screenshot 2025-06-18 154811](https://github.com/user-attachments/assets/7bd436fd-02d6-401b-bce8-4e1127ee512f)

Next step is to draw stick diagram based on the Euler's path. This stick diagram is derived out of the circuit diagram.

![Screenshot 2025-06-18 154833](https://github.com/user-attachments/assets/669f25b0-c963-4a7e-bbc1-a2cdbe48bfe7)

Next step is to convert this stick diagram into a typical Layout, into a proper layout and then get the proper rule we have discissed earlier. Once we get the particular layout then we have the cell width, cell length and all the specifications will be there like drain current, pin locations and so on.

![Screenshot 2025-06-18 155056](https://github.com/user-attachments/assets/c54bf8c3-b5a3-4456-b6eb-9f7b44d0cabe)

* **Characterization:**

  * Simulate the cell across corners to extract

    * **Timing** (delay, setup/hold)
    * **Noise characteristics**
    * **Power consumption**
  * Output files: `.lib` containing these parameters
    
![Screenshot 2025-06-18 155144](https://github.com/user-attachments/assets/01d0370a-898b-468e-8754-52e1b6cb0b20)


---

### **3) Outputs** *(Consumed by EDA Tools)*

* **Circuit Description Language:**

  * Result of circuit design (e.g., Verilog, SPICE netlist)
* **GDSII & Extracted Netlist (.cir):**

  * Result of layout design
* **.lib Files (Timing, Noise, Power):**

  * Result of characterization, used in synthesis, placement, STA, etc.

---
These outputs are essential for the use of the cell in the digital design flow and are interpreted by EDA tools throughout synthesis, placement, routing, and verification.

---

### **Characterization Flow**

#### **1. Read the Model**

* Load the **SPICE models** (from PDK) for all devices.
* These models include electrical characteristics (e.g., mobility, threshold voltage) and are technology-specific.

#### **2. Read the Extracted SPICE Netlist**

* Load the **.cir (extracted SPICE netlist)** of the designed cell (e.g., buffer).
* This includes parasitic components from layout extraction.

#### **3. Define/Recognize the Behavior of the Cell**

* Define the **functionality** (e.g., buffer, inverter, NAND, etc.) for characterization setup.
* Recognize input/output ports and functional relationships.

#### **4. Read Subcircuits (e.g., Inverter in Buffer)**

* Parse and identify any **subcircuits** used within the main cell.
* This step ensures hierarchical cells are properly handled.

#### **5. Attach Power Supplies**

* Connect the **power (VDD)** and **ground (VSS)** sources to the cell.
* Use typical voltage levels as per library specs.

#### **6. Apply Stimulus**

* Provide **input vectors** or voltage waveforms (e.g., a rising/falling edge) to exercise the cell.
* This mimics real switching activity.

#### **7. Provide Output Capacitance**

* Connect **load capacitance** at the output node.
* Helps simulate realistic fanout and measure timing/power accurately.

#### **8. Run Simulation Command**

* Use appropriate SPICE simulation control depending on the analysis:

  * **Transient simulation** → `.tran` command (for delay, slew, dynamic power)
  * **DC simulation** → `.dc` command (for noise margins, voltage transfer characteristics)

![Screenshot 2025-06-18 163725](https://github.com/user-attachments/assets/ebb2b6fc-d52f-4cb1-a082-9a1533624d0d)

---

This flow produces the timing, power, and functional data required for generating `.lib` files, which are then used by digital EDA tools during synthesis, STA, and place-and-route.

### Feeding Inputs to Characterization Tool – **GUNA**

After completing all 8 steps of the characterization preparation, the next step is to **feed these inputs into a configuration file** that the characterization software **GUNA** can understand.

---

### **Step 9: Create Configuration File for GUNA**

The configuration file should include the following information derived from steps 1 to 8:

1. **SPICE Model Files** – Path to technology-specific transistor models
2. **Extracted Netlist** – Path to the `.cir` file of the standard cell
3. **Cell Functionality** – Definition of the cell type (e.g., buffer, inverter, etc.)
4. **Subcircuit Definitions** – Hierarchical references if subcells are present
5. **Power Supply Information** – Voltage levels for VDD and VSS
6. **Input Stimulus** – Signal waveforms or transition times for input pins
7. **Output Load Capacitance** – Capacitance values to model realistic fanout
8. **Simulation Type and Commands** –

   * `.tran` for transient
   * `.dc` for static or noise-related simulations

---

### **Step 10: Run GUNA**

Once the configuration file is set up and all required paths and parameters are correctly defined:

* **Run GUNA**
* It uses the given inputs to perform:

  * **Timing analysis**
  * **Power analysis**
  * **Noise characterization**

---

### **Final Output of GUNA**

GUNA generates standard cell models used by digital design tools:

* **.lib file** → Timing, power, and noise data (for synthesis and STA)
* Other optional outputs for visualization or debugging (waveforms, logs, etc.)

These outputs are now ready to be integrated into the standard cell library for use across the digital IC design flow.

![Screenshot 2025-06-18 163955](https://github.com/user-attachments/assets/d6f7e4ee-4642-448e-b146-8dc431bbca2e)

---
## General timing characterization parameters
---
### Timing threshold definitions
---
As seen in the previous section, where the inverter is connected back to back with power sources and stimulus applied, it becomes essential to understand the different threshold points of a waveform. This concept is known as **"Timing Threshold Definitions."**

In the figure below, the term **`slew_low_rise_thr`** represents a value close to 0, typically set at around **20%** of VDD, though it can also be **30%** depending on design requirements.

![Screenshot 2025-06-18 164428](https://github.com/user-attachments/assets/e6624a1b-7580-4df4-bba4-ac7837d6dc1f)

Slew_high_rise_thr

![Screenshot 2025-06-18 164601](https://github.com/user-attachments/assets/27a711ca-6303-4411-9e2a-d11398ede60b)

Slew_low_fall_thr

![Screenshot 2025-06-18 164648](https://github.com/user-attachments/assets/8b5d86e4-020d-4bc6-9016-8cb5b572fe94)

Slew_high_fall_thr

![Screenshot 2025-06-18 164938](https://github.com/user-attachments/assets/168be275-42f5-4e7b-a742-6f9ff65b1069)

in_rise_thr

![Screenshot 2025-06-18 165105](https://github.com/user-attachments/assets/c57f9f24-9cca-4545-bf77-769e7d3792d6)

in_fall_thr

![image](https://github.com/user-attachments/assets/112841e4-2cb2-46d3-987c-22d8226e4ef2)

out_rise_thr

![Screenshot 2025-06-18 165156](https://github.com/user-attachments/assets/00158c1b-984f-45ab-b7c8-2d7e083f861e)

out_fall_thr

![Screenshot 2025-06-18 165340](https://github.com/user-attachments/assets/af1d83d9-be86-4360-9990-3928e1131a3f)

---
## Propagation delay and transition time
---
Based on the above threshold values, we can calculate key timing parameters such as **propagation delay**, **current**, and **slew**.

To calculate **propagation delay**, we use a common threshold reference—typically **50%** of the supply voltage (VDD)—on both the input and output waveforms.

For example, to compute **rising delay**, the formula is:

> **Time Delay** = **Time(out\_rise\_thr)** − **Time(in\_rise\_thr)**
> (Both thresholds usually set at **50%**)

This means:

* Measure the time when the **input** crosses 50% during its rising transition.
* Measure the time when the **output** crosses 50% during its rising transition.
* Subtract the two to get the **propagation delay**.

This method provides a consistent and technology-independent way of capturing cell delay from waveform behavior.

![Screenshot 2025-06-18 170546](https://github.com/user-attachments/assets/99ec46e9-ee97-4ec7-b48f-e60aef74afe5)

In the above example, the `in_rise_thr` and `out_fall_thr` were both set at 50%. However, if the threshold point is shifted closer to the top of the waveform, the output may appear to transition before the input, resulting in a **negative delay**. Since negative delays are not acceptable, this highlights the importance of choosing the **correct threshold point**. A poorly chosen threshold can lead to inaccurate and misleading timing results.

![Screenshot 2025-06-18 170736](https://github.com/user-attachments/assets/b48f4666-dd22-4c68-8d8d-7ea843782421)

Let’s consider another example where the **threshold point is correctly chosen**, yet we still observe a **negative delay**. This happens when the **output transition begins before the input crosses the threshold**, causing the output to appear as if it changes **before** the input.

Even with proper threshold values, such a scenario leads to a **negative delay**, which is not physically acceptable in digital timing. This situation typically arises due to **improper stimulus**, **parasitic effects**, or **incorrect circuit behavior** during simulation.

Hence, in addition to choosing the correct threshold, it's crucial to ensure proper **input stimulus** and **realistic circuit conditions** to avoid such non-physical results.

![Screenshot 2025-06-18 171016](https://github.com/user-attachments/assets/1698123c-59f3-4ae2-a734-4373550efee1)

zooming in

![Screenshot 2025-06-18 171102](https://github.com/user-attachments/assets/3a9dc974-71e6-42bd-8947-7cbeb8edc836)

**For Rising Transition:**

```
Transition Time (Rise) = time(slew_high_rise_thr) - time(slew_low_rise_thr)
```

**For Falling Transition:**

```
Transition Time (Fall) = time(slew_high_fall_thr) - time(slew_low_fall_thr)
```
Example values
![Screenshot 2025-06-18 171719](https://github.com/user-attachments/assets/2dacc74b-9cc2-4c85-b93f-022e8148a8b5)

The following have been marked in the waveform below
slew_high_rise_thr
slew_high_fall_thr
slew_low_rise_thr
slew_low_fall_thr

![Screenshot 2025-06-18 172152](https://github.com/user-attachments/assets/4228b955-9480-4b3c-bf28-28ddc11ff247)

---
# Day 3 - Design library cell using Magic Layout and ngspice characterization
---
## Labs for CMOS inverter ngspice simulations
---
### IO placer revision
---
One of the key advantages of **OpenLane** is its flexibility—design parameters can be modified **on the fly** without restarting the entire flow.

### **Example 1: Adjusting Core Utilization**

If the initial core utilization is set to **50%** and you observe **congestion** in placement or routing, you can easily increase the utilization to **65%** in the configuration and **rerun the flow**. This helps in experimenting with different area optimizations efficiently.

---

### **Example 2: Changing I/O Pin Placement Strategy**

Initially, if input/output pins were placed **equidistant** from each other, but now you want to switch to a different placement strategy, OpenLane allows that too.

OpenLane supports **four I/O placement strategies** via the `ioPlacer` tool.

To change the strategy, update the environment variable:

```tcl
set ::env(FP_IO_MODE) 2
```

Then rerun floorplanning:

```tcl
run_floorplan
```
![Screenshot 2025-06-19 091400](https://github.com/user-attachments/assets/e73e4cb4-c83a-4c27-b382-b67ad5a41b16)

After running the command, check the updated floorplan.
Now, the **pins are stacked one above the other**, reflecting the new I/O placement mode.

![Screenshot 2025-06-19 091919](https://github.com/user-attachments/assets/e849560b-31a3-4cf4-8849-a2a99a369e82)
![Screenshot 2025-06-19 092023](https://github.com/user-attachments/assets/119602e9-9cb5-457a-b16a-dfc7a6f6671d)

This shows how OpenLane provides real-time flexibility to experiment with and refine your layout strategy.
---
### SPICE deck creation for CMOS inverter
---
### SPICE Simulations

The first step in SPICE simulations is to **create the SPICE deck**. A SPICE deck contains the **connectivity information** of the netlist. It also includes the **input sources** to be applied during simulation and the **tap points** where the output is measured.

* **Component Connectivity**:
  In the SPICE deck, the connectivity of all components must be defined, including the **substrate pin**, which affects the **threshold voltage** of PMOS and NMOS transistors.

  ![Screenshot 2025-06-19 093428](https://github.com/user-attachments/assets/19c92e68-9053-445a-9175-16e0a278acd9)

* **Component Values**:
  The **W/L ratios** (width/length) of the PMOS and NMOS transistors are specified. For now, the **same size** is used for both.

  ![Screenshot 2025-06-19 094159](https://github.com/user-attachments/assets/0a69d508-8235-44de-bea2-547d18e4d106)

* **Identify Nodes**:
  Nodes are the points between which components are connected. They are essential for defining the SPICE netlist.

  ![Screenshot 2025-06-19 094258](https://github.com/user-attachments/assets/0475a268-0b25-4421-b16b-8487dbcc1739)

* **Naming Nodes**:
  Common node names include: `in`, `Vss`, `Vdd`, and `out`.

  ![Screenshot 2025-06-19 094529](https://github.com/user-attachments/assets/b3038c60-a024-4781-abcc-b45d7486cf41)

---

### Starting the SPICE Deck

**MOSFET Syntax in SPICE:**

![Screenshot 2025-06-19 094725](https://github.com/user-attachments/assets/419a3657-f6c7-46fd-96d7-0aed9975b619)
![Screenshot 2025-06-19 100025](https://github.com/user-attachments/assets/b1eaf262-1229-4112-81b2-f8e7dd2e4329)


```
M<name> <drain> <gate> <source> <bulk> <model_name> L=<length> W=<width>
```
![Screenshot 2025-06-19 094743](https://github.com/user-attachments/assets/667e9f26-59d4-4a2e-b1ff-a3a051a0a7a3)

---
### SPICE simulation lab for CMOS inverter
---
Till now, we have described the **connectivity information of the CMOS inverter**. Next, we will define the connectivity of the **other components**, such as the **load capacitor** and **voltage sources**.

![Screenshot 2025-06-19 100222](https://github.com/user-attachments/assets/3012f072-56c7-4626-92f4-9ecd93bcfef2)

---

### **Load Capacitor (Output Capacitance)**

![Screenshot 2025-06-19 100139](https://github.com/user-attachments/assets/216b9ee9-dc45-446b-bd43-18e14d2cc9d4)

* The **load capacitor** is connected between the **`out`** node and **node `0`** (ground).
* The value of the capacitor is **10fF**.

```
Cload out 0 10f
```

---

### **Supply Voltage (Vdd)**

![Screenshot 2025-06-19 100153](https://github.com/user-attachments/assets/ccf9af42-bcdf-4034-a2a1-17278ba624e7)

* The **Vdd source** is connected between **`Vdd`** and **node `0`**.
* The voltage value is **2.5V**.

```
Vdd Vdd 0 2.5
```

---

### **Input Voltage (Vin)**

![Screenshot 2025-06-19 100206](https://github.com/user-attachments/assets/88b4307d-97b6-4106-9c86-682c78d27019)

* The **input voltage source** is connected between **`Vin`** and **node `0`**.
* The voltage is also **2.5V**.

```
Vin in 0 2.5
```

---

These definitions complete the required component connections for simulating the CMOS inverter with proper input, power, and output load conditions.

---
Now we need to add the **simulation commands** to perform a **DC sweep**. In this case, we're sweeping the input voltage `Vin` from **0V to 2.5V** with a **step size of 0.05V**. This allows us to observe how `Vout` changes as `Vin` varies.

---

### **DC Sweep Command**

![Screenshot 2025-06-19 100713](https://github.com/user-attachments/assets/1a360a75-cfb3-47c0-be44-3b2c7074fb0a)

```spice
.dc Vin 0 2.5 0.05
```

* `Vin` → name of the voltage source to sweep
* `0` → starting value
* `2.5` → ending value
* `0.05` → step size

---

This command will simulate the behavior of the CMOS inverter across all input voltages from 0V to 2.5V and generate the corresponding output values, helping us analyze the **VTC (Voltage Transfer Characteristic)**.

---
Final step is to include the **model files**, which contain the complete description of **NMOS** and **PMOS** transistors.

![Screenshot 2025-06-19 101221](https://github.com/user-attachments/assets/d8d0d636-8595-4d88-b88f-12517446107d)

![Screenshot 2025-06-19 101517](https://github.com/user-attachments/assets/ccddab8b-6f15-4e15-b80f-1d98605307f6)

---

Lets do the spice simulation for the following specifications

![Screenshot 2025-06-19 101716](https://github.com/user-attachments/assets/cd39fbc4-0935-4281-bc75-216178f2d6d4)

The plot obtained is

![image](https://github.com/user-attachments/assets/f34f72f9-fd0e-43c6-b460-333ffa557f2d)

Now, we perform another simulation where the **PMOS width is set to three times** the **NMOS width**. After running the simulation with this updated sizing, we obtain the output graph as shown below.

![Screenshot 2025-06-19 102333](https://github.com/user-attachments/assets/5d3b3c65-5fcf-4e10-a11e-6d185deb4682)

The plot obtained is

![Screenshot 2025-06-19 102419](https://github.com/user-attachments/assets/402f670d-9ce6-4c79-a9ec-f8e206cea17e)

The difference between the two graphs is that, in the **second graph**, the **transfer characteristic lies exactly in the middle** of the graph. In contrast, in the **first graph**, the **transfer characteristic is shifted to the left** of the center.

---
### Switching Threshold Vm
---
Both models with different transistor widths have their **own specific applications**. By comparing the waveforms from each, we observe that the **overall shape remains the same**, regardless of the voltage levels. This consistency indicates that **CMOS is a highly robust technology**.

When `Vin` is low, the output remains high, and when `Vin` is high, the output goes low—demonstrating that the **inverter characteristic is preserved** across different sizing ratios of NMOS and PMOS. This is one of the key reasons why **CMOS logic is widely used** in digital gate design.

One important parameter that reflects the robustness of an inverter is the **switching threshold, Vm** — the point where `Vin = Vout`. This point marks the transition level at which the inverter switches its state. A well-balanced inverter has this threshold near the **midpoint of the supply voltage**, contributing to **noise margin balance and signal integrity**.

![Screenshot 2025-06-19 115834](https://github.com/user-attachments/assets/7493b280-2594-40a2-b8c9-d0ec3380a905)

In this figure, we observe that at **Vm ≈ 0.9V**, the condition **Vin = Vout** is met. This point is critical for CMOS operation because at **Vm**, there is a high possibility that **both the PMOS and NMOS transistors are partially turned on**.

![Screenshot 2025-06-19 120235](https://github.com/user-attachments/assets/28ad5b9c-3d4c-454d-a710-2151015a0d3d)

When both transistors conduct simultaneously, it creates a direct path from **Vdd to Vss (power to ground)**, resulting in **leakage current**. This current can lead to **increased power consumption** and may affect circuit reliability if not properly controlled.

By comparing the two graphs, we gain a clear understanding of the **switching threshold voltage (Vm)** and how it plays a key role in defining the **operating region and power behavior** of a CMOS inverter.

![Screenshot 2025-06-19 120547](https://github.com/user-attachments/assets/a4946e35-477d-43ba-9d80-5a66cad0f954)

In the graph below, we can identify the **operating regions** of the **PMOS and NMOS transistors** at different points along the transfer characteristic curve.

The **direction of current flow** is also different for each:

* For **NMOS**, current flows from **drain to source** (typically from `Vout` to `GND`).
* For **PMOS**, current flows from **source to drain** (typically from `Vdd` to `Vout`).

By analyzing the graph, we can determine at each region (cutoff, linear, saturation) whether the NMOS or PMOS is conducting, and in what mode. This is helpful for understanding the **dynamic behavior and power dissipation** of the CMOS inverter across its input voltage range.

![Screenshot 2025-06-19 120804](https://github.com/user-attachments/assets/7cac2174-92cc-4229-ac14-2e07af53b66c)

---
### Static and dynamic simulation of CMOS inverter
---
Continuing the Discussion on Switching Threshold (Vm)

![Screenshot 2025-06-19 121426](https://github.com/user-attachments/assets/764c0091-1e42-4be4-9600-bbfd9591027c)

We now move forward by studying the effect of changing the **PMOS width-to-length ratio (W/L)** as an **integer multiple** of the **NMOS (W/L)**. The goal is to **evaluate the robustness** of the **switching threshold (Vm)** under different sizing conditions.

Earlier, we had already simulated the case where:

```
(W/L of PMOS) / (W/L of NMOS) = 1
```
![Screenshot 2025-06-19 121340](https://github.com/user-attachments/assets/89f3e795-ddbf-44e5-8e6d-6f9bcb2215d4)

---

### **Dynamic Simulation**

In this step, we shift from DC analysis to **dynamic (transient) simulation**.

![Screenshot 2025-06-19 121813](https://github.com/user-attachments/assets/b137565f-5d06-402b-9f9a-0f4fde33b729)

* An **input pulse** is defined in the SPICE deck.

This **pulse waveform** is applied to the **CMOS inverter** as the input signal, and we run a **transient analysis** using the `.tran` command.

![Screenshot 2025-06-19 121914](https://github.com/user-attachments/assets/b03d5821-29e1-4222-bdc6-6836d5ba6817)

---

### **Purpose of This Simulation**

Through this dynamic simulation, we can observe:

* **Rise delay** (low → high transition at output)
* **Fall delay** (high → low transition at output)
* How these delays **change with variations in Vm** (caused by different PMOS/NMOS sizing)

In this setup, **everything else remains constant**—only the input waveform and the simulation type are changed. This helps us study how **Vm impacts switching speed and symmetry**, which are critical for **timing analysis** and **circuit performance**.

To calculate the **delay** of a CMOS inverter, we need to **plot both the input and output waveforms against time**.

![Screenshot 2025-06-19 123136](https://github.com/user-attachments/assets/10fecc7c-0a26-4185-ad6e-de4322944c06)

---

### **Delay Calculation Method**

* **Delay** is measured from the point where the **input crosses 50% of VDD** to the point where the **output crosses 50% of VDD**.
* In this case, since **VDD = 2.5V**, the **50% threshold is 1.25V**.

---

### **Step-by-Step Process**

1. **Zoom in** on the waveform around the switching points.
2. **Note the timestamps** where:

   * **Vin = 1.25V**
   * **Vout = 1.25V**

---

### **Rise Delay**

* Input is **falling**, output is **rising**.
* Delay = Time (Vout reaches 1.25V) − Time (Vin falls to 1.25V)
* Delay = `1.16276 ns` − `1.01446 ns` = **0.1483 ns**

![Screenshot 2025-06-19 123216](https://github.com/user-attachments/assets/0001a631-acb3-4ce2-9eb7-a1214a807349)

![Screenshot 2025-06-19 123233](https://github.com/user-attachments/assets/b64f2405-c528-4b5a-aff1-4105d5675b90)

---

### **Fall Delay**

* Input is **rising**, output is **falling**.
* Delay = Time (Vout falls to 1.25V) − Time (Vin rises to 1.25V)
* Delay = `2.07653 ns` − `2.00486 ns` = **0.07167 ns**

![Screenshot 2025-06-19 123521](https://github.com/user-attachments/assets/38747413-0d14-4aa3-bf56-70bd2ea964ff)

![Screenshot 2025-06-19 123716](https://github.com/user-attachments/assets/1b697feb-51cc-44cd-828b-cf59c1efd59b)

---

This analysis gives a clear view of how the inverter responds to input changes and helps in evaluating its **timing performance**.

---
### Lab steps to git clone vsdstdcelldesign
---

 **What is `git clone`?**

The `git clone` command is used to **download a GitHub repository** (or any Git repo) **to your local machine**.

---

 **Syntax of `git clone`**

```bash
git clone <repository_url>
```

---

**Example Usage**

Let’s say you want to clone the [OpenLane](https://github.com/The-OpenROAD-Project/OpenLane) repository from GitHub.

1. **Copy the URL of the repository** (HTTPS link):

   ```
   https://github.com/The-OpenROAD-Project/OpenLane.git
   ```

2. **Open terminal or command prompt**, and run:

```bash
git clone https://github.com/The-OpenROAD-Project/OpenLane.git
```

This command will:

* Create a folder named `OpenLane`
* Download all the code, branches, and history from the repo into that folder

---

**Optional: Clone into a Custom Folder Name**

```bash
git clone https://github.com/The-OpenROAD-Project/OpenLane.git my_openlane
```

This clones the repo into a folder named `my_openlane`.

---

**After Cloning**

You can go into the cloned repo and start working:

```bash
cd OpenLane
```

---
To get the clone, copy the clone address from reporetery and paste in openlane terminal after the command git clone. this will create the folder called "vsdstdcelldesign" in openlane directory.

![Screenshot 2025-06-19 132343](https://github.com/user-attachments/assets/f4e8bf99-05d1-46cf-8b7b-89710820725c)

![Screenshot 2025-06-19 132638](https://github.com/user-attachments/assets/3e82ab7e-4080-48d2-b56a-0e74ee67261f)

copy the sky130.tech file in vsdstdcelldesign directory

![Screenshot 2025-06-19 142013](https://github.com/user-attachments/assets/621264be-e70a-4e2c-a6bf-cbead18884c9)

Now to view the invereter layout 

![Screenshot 2025-06-19 143954](https://github.com/user-attachments/assets/8f68752f-1813-4d5d-a69f-e807e81d94ad)

![Screenshot 2025-06-19 144108](https://github.com/user-attachments/assets/90b88ddd-9249-4a8c-bab6-507113f9b4ae)

---
## Inception of layout ̂CMOS fabrication process
---
### Create Active regions
---

### 1) **Selecting a Substrate**

We begin with a **p-type silicon substrate** that is:

* **Highly resistive**, typically in the range of **5–50 Ω·cm**
* **Well-doped** to achieve the desired electrical properties
* Has a crystal **orientation of (100)**, which is preferred for CMOS fabrication due to better carrier mobility and easier oxide growth

---

### 2) **Creating Active Regions for Transistors**

The **active regions** are the areas where **PMOS and NMOS transistors** will be formed. These regions are defined on the **p-type substrate** by creating **localized pockets**, where the actual devices will reside.

To ensure proper functioning and electrical isolation between these pockets, we create **isolation layers**.

#### **Isolation Layer Formation:**

* First, a **thin layer of silicon dioxide (SiO₂)** is deposited, typically around **40 nm** thick.
* Next, a **layer of silicon nitride (Si₃N₄)** is deposited over the SiO₂, with a thickness of approximately **80 nm**.

These layers form the foundation for **LOCOS (Local Oxidation of Silicon)** or **Shallow Trench Isolation (STI)**, which are used to electrically isolate individual transistors in integrated circuits.

![Screenshot 2025-06-19 145924](https://github.com/user-attachments/assets/c14a19e3-7c2c-40e0-a7fc-c7fecc75afc7)

![Screenshot 2025-06-19 145954](https://github.com/user-attachments/assets/3df40b6d-da7e-4c5f-b932-32f1062c19bd)

Before creating the pocket, we first **identify the regions** where the pockets need to be formed. Then, a **photoresist layer** of approximately **1 μm** thickness is **deposited** over the surface. Using **UV light exposure**, we create a **mask (Mask 1)** on this photoresist layer to define the desired regions.

![Screenshot 2025-06-19 150018](https://github.com/user-attachments/assets/05609b3d-8943-44f6-aa89-35e897816555)

The **unwanted areas** are **exposed to UV light**, and as a result, a **pattern is formed** on the photoresist layer. The **exposed regions** become soluble and are **washed away** during the **development process**, leaving behind the **desired pattern** for further processing.

![Screenshot 2025-06-19 150256](https://github.com/user-attachments/assets/feb7a456-c9d3-4942-8edc-121d7f6ff765)

In the next step, the **photoresist mask is removed**, and **etching is performed** on the **Si₃N₄ (silicon nitride) layer** in the **exposed areas**. This etching process selectively removes the Si₃N₄ only from regions not protected by the photoresist, thereby opening windows where the **active regions or isolation structures** will be formed.

![Screenshot 2025-06-19 150328](https://github.com/user-attachments/assets/aac6db53-5435-4eae-89e0-2e87110d8de5)

Now, the next step is to **remove the photoresist** using a **chemical reaction** (commonly called photoresist stripping). At this stage, the **Si₃N₄ layer itself acts as a protective mask** for the underlying **SiO₂ layer**.

Next, the wafer is placed in an **oxidation furnace**. If we perform the **LOCOS (Local Oxidation of Silicon)** process, the **exposed regions of SiO₂** will **grow thermally**, and a characteristic **bird's beak** structure will form at the edges of the oxide.

This **grown oxide** acts as an **isolation layer**, effectively **separating adjacent PMOS and NMOS transistors**, and **preventing unwanted communication** between them. This is how electrical isolation between two transistors is achieved during fabrication.

![Screenshot 2025-06-19 150418](https://github.com/user-attachments/assets/ba20d791-9de9-4bdd-adac-f0944ba2daf0)

![Screenshot 2025-06-19 150552](https://github.com/user-attachments/assets/85fbb589-eb6f-4274-bb30-b965314b8892)

The next step is to **remove the Si₃N₄ (silicon nitride) layer**, which served as a protective mask during oxidation. This is done using **hot phosphoric acid (H₃PO₄)**, which selectively etches away **Si₃N₄** without affecting the underlying **SiO₂**.

This step clears the wafer surface for subsequent processing steps, while retaining the **field oxide regions** formed during LOCOS for **transistor isolation**.

![Screenshot 2025-06-19 150658](https://github.com/user-attachments/assets/42aa17e6-2d54-4bb0-8156-9eae20bb673d)

---
### Formation of N-well and P-well
---

### 3) **N-well and P-well Formation**

We **cannot form both P-well and N-well simultaneously**, as the doping requirements are different. Therefore, we must **protect one region** while forming the other using a **photoresist layer**.

To form the **P-well**, we proceed as follows:

* First, **deposit a photoresist** layer on the wafer.
* Then, using **Mask 2** and **UV light exposure**, we **pattern the photoresist** to define the areas where the **P-well** is to be created.
* The **exposed regions** are developed, opening windows for **P-type dopant implantation** while protecting the rest of the wafer.

This selective process ensures **controlled well formation** in the desired regions. The same method is repeated later for **N-well formation**, using a different mask and dopant type.

![Screenshot 2025-06-19 151640](https://github.com/user-attachments/assets/354bd9b5-5cfc-4797-bf54-9b8eda886a03)

Now, the area where we want to form the **P-well** is **exposed** after the photoresist is patterned. The **mask is then removed**, and the wafer is subjected to **ion implantation** using **Boron** as the dopant.

* The implantation energy is typically around **200 keV**.
* This step introduces **P-type dopants** into the exposed silicon region, but at this stage, it is still referred to as a **P-type implant**.

To activate the dopants and drive them deeper into the substrate, a **high-temperature annealing** process is performed. After annealing, the doped region becomes a fully formed **P-well**.

![Screenshot 2025-06-19 151731](https://github.com/user-attachments/assets/5edcb685-e56c-45e2-901a-3378cdf4c956)

A **similar process** is followed to form the **N-well**:

* Apply a **new photoresist layer** and use **Mask 3** to define the N-well regions.
* Expose the wafer to **UV light**, pattern the photoresist, and **develop** it to expose only the areas where the N-well is to be formed.
* Remove the photoresist from exposed regions.
* Perform **ion implantation** using **Phosphorus ions** (N-type dopant), typically at an energy of around **200 keV**.
* Finally, carry out **high-temperature annealing** to activate the dopants and drive them into the silicon.

This completes the **N-well formation**.

![Screenshot 2025-06-19 151845](https://github.com/user-attachments/assets/9d53d2bd-d369-4d29-9557-0fbafd655594)

Till now, the **depth of the wells** (P-well and N-well) has not been fully established. To achieve the desired depth and proper dopant distribution, the wafer is placed into a **high-temperature furnace**.

This step is known as **drive-in diffusion**.

* During this process, the **implanted dopants diffuse deeper** into the silicon substrate.
* The **depth and concentration** of the wells are determined by the **temperature** and **duration** of this step.

This completes the proper formation of **P-well and N-well regions** with defined depths, making them ready for active device fabrication.

![Screenshot 2025-06-19 151929](https://github.com/user-attachments/assets/5153ae30-d87a-430c-9998-162fba4c5093)

![Screenshot 2025-06-19 151955](https://github.com/user-attachments/assets/cd9e2842-0618-4c08-99f4-c160f890be78)

![Screenshot 2025-06-19 152006](https://github.com/user-attachments/assets/0a6a156b-8284-40e2-91f2-4a955e63b02d)

---
### Formation of gate terminal
---
### 4) **Gate Formation**

The **gate terminal** is the most critical terminal of both **PMOS and NMOS transistors**, as it directly controls the **threshold voltage (V<sub>th</sub>)** of the device.

The **threshold voltage** is influenced by two main factors:

* **Doping concentration** in the channel region
* **Oxide capacitance** (which depends on oxide thickness and permittivity)

---

### **Step 1: Channel Doping Adjustment**

To adjust the **doping concentration** in the channel and help control the threshold voltage, we perform **channel doping** as follows:

* Apply **Mask 4** to define the gate region.
* Carry out **ion implantation** using **Boron ions** (a P-type dopant).
* The implantation is done at a **lower energy**, typically around **60 keV**, so the dopants stay close to the surface.

This step ensures the **channel is properly doped** before the actual gate structure is built, allowing for precise **threshold voltage tuning**.

![Screenshot 2025-06-19 152713](https://github.com/user-attachments/assets/27c338c5-590c-4936-b6e2-bb253362c780)

![Screenshot 2025-06-19 152735](https://github.com/user-attachments/assets/b41871f8-3778-495d-af66-9dfa60ca7d0d)

The **same process is repeated** for the **N-well** region as well:

* This time, we use **Mask 5** to define the required area.
* Perform **ion implantation** using **Arsenic ions** (an N-type dopant).
* The implantation is done at **low energy**, similar to the previous step, to control the **surface doping concentration**.

This step ensures proper **channel doping** for **PMOS transistors** formed in the N-well, contributing to accurate **threshold voltage control**.

![Screenshot 2025-06-19 152829](https://github.com/user-attachments/assets/582bdcac-db73-490a-a7eb-da273d142bb2)

![Screenshot 2025-06-19 152852](https://github.com/user-attachments/assets/eb3f8992-18c8-4588-acac-b7051712012d)

### 5) **Gate Oxide Formation and Polysilicon Deposition**

Before forming the final gate structure, we need to ensure that the **gate oxide layer** is of **high quality**, since it plays a critical role in device performance.

---

### **Step 1: Gate Oxide Removal and Regrowth**

* The previously formed **oxide layer** has been **damaged** due to earlier ion implantation and processing steps.
* Therefore, we **remove the damaged oxide** using an **HF (hydrofluoric acid)** solution.
* A new, high-quality **gate oxide layer** is then **thermally grown** to the **same thickness** as required, ensuring **reliability and uniformity**.

---

### **Step 2: Polysilicon Deposition**

* A layer of **polysilicon** is deposited **over the newly grown gate oxide**.
* This polysilicon is **heavily doped** to **reduce resistance**, making it suitable for use as the **gate terminal**.

---

### **Step 3: Gate Patterning**

* Apply **photoresist** and use **Mask 6** to define the **gate structure**.
* Using **photolithography and etching**, the **polysilicon layer is etched**, leaving behind the **gate terminals** exactly over the channel region of the NMOS and PMOS transistors.

This completes the formation of the **gate structure**, enabling precise control of the transistor switching behavior.

![Screenshot 2025-06-19 153009](https://github.com/user-attachments/assets/0749a2d9-bed7-4842-af43-7e7df07f4233)

After the **etching process**, the **photoresist is removed** using a stripping solution or plasma ashing. Once the photoresist is cleared:

* The **gate terminal**—made of **doped polysilicon**—is now clearly defined.
* It **sits precisely over the channel region** between the source and drain of both PMOS and NMOS.
* The underlying **gate oxide** remains intact under the polysilicon, forming the **MOS capacitor structure** essential for transistor operation.

At this stage, the **gate terminal is ready** to control current flow in the device by modulating the channel beneath it through applied voltage.

![Screenshot 2025-06-19 153058](https://github.com/user-attachments/assets/7cdcc399-2a5f-4f9e-ba83-ba5a216fce06)

---
### Lightly doped drain (LDD) formation
---
### 5) **LDD (Lightly Doped Drain) Formation**

To mitigate issues like the **hot electron effect** and **short channel effects** in scaled-down devices, we use a **graded doping profile** near the drain and source regions of transistors.

---

### **Doping Profiles Needed:**

* For **PMOS** (in N-well):
  → **P⁺**, **P⁻**, and **N** regions
* For **NMOS** (in P-well):
  → **N⁺**, **N⁻**, and **P** regions

This graded profile is achieved using **LDD structures** (Lightly Doped Drain).

---

### **Formation of LDD:**

* Using **Mask 7**, we open regions in the **P-well** where **NMOS transistors** will be formed.
* Then, perform **ion implantation** using **phosphorus** (an N-type dopant) at **low concentration** and **lower energy**.
  → This creates a **lightly doped N⁻ region** near the channel area of NMOS.

The same process is later repeated for PMOS using a **P-type dopant** (e.g., Boron) to create **P⁻ regions**.

These lightly doped extensions near the gate help in:

* Reducing **electric field strength** near the drain
* Controlling **drain-induced barrier lowering (DIBL)**
* Minimizing **hot carrier injection**
  Thus, **LDD formation is crucial for device reliability and performance** in deep submicron technologies.

![Screenshot 2025-06-19 154027](https://github.com/user-attachments/assets/ab3e93cc-6c27-4342-bb37-a7032c9698b2)

![Screenshot 2025-06-19 154038](https://github.com/user-attachments/assets/afb63e0b-f353-4f20-902e-692b2c164574)

![Screenshot 2025-06-19 154052](https://github.com/user-attachments/assets/04cb00b1-8667-43cc-b31a-fc0c0c21d66e)

The **same process is repeated for the N-well** region to form the LDD structure for **PMOS transistors**.

* We use **Mask 8** to expose the required regions in the **N-well**.
* Then, perform **ion implantation** using **Boron ions** (a P-type dopant) at **low concentration** and **low energy**.

This creates the **lightly doped P⁻ regions** near the channel of the PMOS transistor.

These **P⁻ regions**, along with the previously formed **P⁺ regions** (in later steps), help reduce electric field stress and improve device reliability—just like in NMOS.

![Screenshot 2025-06-19 154119](https://github.com/user-attachments/assets/8b7bcbe1-ea82-4311-aec7-6ca5e35f2874)

![Screenshot 2025-06-19 154141](https://github.com/user-attachments/assets/271e2005-8c1c-4e6a-b565-018a8985cc6f)

Now, to **protect the lightly doped regions (P⁻ and N⁻)** and to define the spacing before forming heavily doped source/drain regions, we **create spacers** along the sides of the gate.

To do this:

* A **thick layer of SiO₂ or Si₃N₄** is **deposited over the entire wafer**, covering the **gate terminal and surrounding areas**.
* This layer is then **anisotropically etched**, so that material remains only **along the sidewalls of the gate**, forming **spacers**.

These **spacers** serve to:

* **Physically separate** the gate from the next doping step
* **Protect the lightly doped drain extensions** (P⁻/N⁻) during the upcoming high-dose implant
* Define the final **source and drain junction depth and overlap**

This ensures the **structure remains intact** and maintains the desired **doping profile and device performance**.

![Screenshot 2025-06-19 154801](https://github.com/user-attachments/assets/3f6783e5-7edf-435c-9b4a-58f7122f0a0e)

Now, we perform **plasma anisotropic etching**, which selectively removes the deposited oxide or nitride layer **vertically**, while leaving material intact on the **sidewalls of the gate**.

As a result, **sidewall spacers** are formed along the gate structure.

These spacers:

* **Protect the lightly doped regions (LDD)**
* **Define the offset** between the gate and the upcoming heavily doped source/drain regions
* Help in **reducing short-channel effects** and **improving device reliability**

This completes the **spacer formation** step.

![Screenshot 2025-06-19 154837](https://github.com/user-attachments/assets/f9eba89d-c096-43a9-aa08-a647862fdaa7)

![Screenshot 2025-06-19 154915](https://github.com/user-attachments/assets/8c748c71-e486-4eb3-bd6a-8aed79f010ad)

---
### Source - drain formation
---
### 6) **Source–Drain Formation**

The next step is to **form the heavily doped source and drain regions** for both NMOS and PMOS transistors.

---

### **Step 1: Screen Oxide Deposition**

Before performing the heavy ion implantation, we **deposit a very thin layer of screen oxide** over the wafer surface.

* This **screen oxide** helps to **reduce channeling effects**, which can occur when high-energy ions penetrate too deeply through crystalline defects or at steep angles.
* It also provides **better control over dopant placement** and protects the underlying silicon during implantation.

This oxide layer is usually a few nanometers thick and is thermally grown or deposited just before the **source–drain implantation step**.

![Screenshot 2025-06-19 155819](https://github.com/user-attachments/assets/a98d4b71-4ad1-4348-acea-e9d92c336025)

Now, to form the **source and drain** regions for **PMOS**, we perform the following:

* Use **Mask 9** to expose the appropriate regions in the **P-well**.
* Then, carry out **ion implantation** using **arsenic ions** (an N-type dopant) at an energy of around **75 keV**.
* This creates the **N⁺ source and drain regions** in the P-well for **PMOS transistors**.

This **high-dose implant** ensures low-resistance source and drain contacts, completing the heavily doped N⁺ regions for PMOS devices.

![Screenshot 2025-06-19 155834](https://github.com/user-attachments/assets/47972f67-c547-43a4-964d-82a584c3e520)

![Screenshot 2025-06-19 155857](https://github.com/user-attachments/assets/869fe67f-3f11-4747-96a0-cf0dc6c028cd)

![Screenshot 2025-06-19 160000](https://github.com/user-attachments/assets/91916943-a6c3-4946-a716-650a4a094c04)

The **same process is repeated** to form the **source and drain regions** for **NMOS transistors**:

* Use **Mask 10** to expose the desired regions in the **N-well**.
* Perform **ion implantation** using **boron ions** (a P-type dopant) at an energy of around **50 keV**.
* This creates the **P⁺ source and drain regions** in the N-well, completing the **NMOS transistor structure**.

At this stage, both NMOS and PMOS transistors have their respective **source, drain, and gate terminals** fully defined and ready for subsequent processing steps like silicidation, contact formation, and metallization.

![Screenshot 2025-06-19 160013](https://github.com/user-attachments/assets/7a7192a9-bde1-400a-8f29-53f9cb528fa2)

![Screenshot 2025-06-19 160038](https://github.com/user-attachments/assets/69de8e82-282f-40f1-a6ff-9e65fb2cc77d)

![Screenshot 2025-06-19 160101](https://github.com/user-attachments/assets/f56c62f2-68ea-4802-a6ed-cf5fa6c49bd0)

Now, the partially fabricated CMOS wafer is placed into a **high-temperature annealing furnace** (typically around **1000 °C**).

This annealing step serves two key purposes:

* It **activates the dopants** in the **P⁺ and N⁺ regions**, allowing them to become electrically active.
* It causes **lateral and vertical diffusion**, helping the implanted dopants **fully form the source and drain regions** for both **NMOS and PMOS** transistors.

After this process, the **P⁺ and N⁺ implants** officially become the **functional source and drain terminals** of the CMOS devices.

![Screenshot 2025-06-19 160117](https://github.com/user-attachments/assets/a7d3a97d-e7db-4b55-a954-4999f3d94ef1)

![Screenshot 2025-06-19 160154](https://github.com/user-attachments/assets/836c23e1-3e14-4539-bf4f-18f9eb55ebd4)

---
### Local interconnect formation
---
### 7) **Steps to Form Contacts and Local Interconnects**

---

#### **Step 1: Remove Screen Oxide**

* The **thin screen oxide layer** (used earlier to prevent channeling during implantation) is now **removed by etching** to expose the **source, drain, and gate regions**.

---

#### **Step 2: Titanium (Ti) Deposition**

* A thin layer of **titanium (Ti)** is **deposited using sputtering**.
* Titanium is chosen because of its **very low resistivity**, which helps in forming good electrical contact with the underlying silicon.
* This layer is essential for forming **titanium silicide (TiSi₂)** in the next steps, which significantly reduces **contact resistance**.

This process sets the foundation for forming **local interconnects** and ensuring **reliable connections** between transistors and metal layers.

![Screenshot 2025-06-19 161102](https://github.com/user-attachments/assets/3a623ac5-0721-42f8-a2e6-1d87ad3d541d)

![Screenshot 2025-06-19 161123](https://github.com/user-attachments/assets/5dc276d7-3aa2-4176-acfc-5afcfe4f1d96)

![Screenshot 2025-06-19 161154](https://github.com/user-attachments/assets/192a2bcc-8125-4723-83a9-4a3bc09752d4)

![Screenshot 2025-06-19 161206](https://github.com/user-attachments/assets/783b2782-9c4e-4c0f-a5aa-5903f91221d6)

### **Next Step: Silicidation and Formation of Local Interconnects**

After depositing the **titanium (Ti) layer**, the wafer is subjected to a **rapid thermal annealing** process to initiate reactions:

---

####  **Silicidation Reaction**

* The wafer is **heated to 650–700 °C** in a **nitrogen (N₂) ambient** for about **60 seconds**.

* At this temperature, **titanium reacts with exposed silicon** regions (source, drain, and gate) to form **titanium silicide (TiSi₂)**.

  **Reaction:**
  `Ti + Si → TiSi₂`

* **TiSi₂** has **low contact resistance**, which improves the performance and speed of the CMOS devices.

---

####  **Formation of TiN (Titanium Nitride)**

* Simultaneously, **titanium also reacts with nitrogen** from the ambient to form **titanium nitride (TiN)**.

  **Reaction:**
  `Ti + N₂ → TiN`

* **TiN** does not form on silicon but rather over field oxide or other regions, and it is used for **local interconnects** due to its **good conductivity** and **barrier properties**.

![Screenshot 2025-06-19 161235](https://github.com/user-attachments/assets/c036f0b4-59b4-421e-9598-1ebe865a6c23)

![Screenshot 2025-06-19 161310](https://github.com/user-attachments/assets/44cfb55b-d631-4018-8685-0179a48520b6)

Now, using **Mask 11** and **photoresist**, we define the specific regions where **contacts** need to be formed.

* Apply **photoresist**, expose it through **Mask 11**, and develop the pattern to selectively expose **TiN** in unwanted areas.
* The exposed **TiN (Titanium Nitride)** is then **etched out** using the **RCA cleaning process**.

This step ensures that **TiN remains only in the desired regions**, forming **defined local interconnects**, while **opening contact windows** for metal connections in subsequent steps.

![Screenshot 2025-06-19 161350](https://github.com/user-attachments/assets/74071fe4-bcf0-4c60-83ac-260671090947)

![Screenshot 2025-06-19 161429](https://github.com/user-attachments/assets/96aa9bde-b1bf-41b3-b36d-7affe05b41d7)

![Screenshot 2025-06-19 161444](https://github.com/user-attachments/assets/83aaa104-c8c7-455d-9f8a-268aa822eb1b)

![Screenshot 2025-06-19 161502](https://github.com/user-attachments/assets/9f253496-bcd6-4487-a8bb-bb1f16e501bf)

Now, after **etching the unwanted TiN** and **removing the photoresist**, the **local interconnects** are successfully formed.

* The **TiN** remains only in the designated regions, serving as **conductive paths** between nearby source, drain, and gate terminals.
* These interconnects enable **local signal routing** within the CMOS structure before global metal layers are added.

This completes the **local interconnect formation** stage.

![Screenshot 2025-06-19 161516](https://github.com/user-attachments/assets/ff65d320-7993-4f1b-9319-1fb19db92d5e)

---
### Higher level metal formation
---
### 8) Higher Level Metal Formation

The process of forming higher-level metal interconnects follows a pattern similar to earlier interconnect steps, but begins with surface preparation.

#### Surface Planarization

At this stage, the wafer surface is highly non-planar due to the presence of gates, spacers, silicides, and local interconnects. Using a non-planar surface for global metal interconnections can lead to issues such as:

* Metal discontinuity
* Step coverage problems
* Lithography misalignment

To resolve this, the following steps are taken:

1. A **thick layer of SiO₂** is deposited over the entire surface. This oxide may be lightly doped to reduce its resistivity.
2. The wafer is then subjected to **CMP (Chemical Mechanical Polishing)**, which uniformly polishes the surface and removes topographical variations.

This results in a **flat and uniform surface**, making it suitable for creating reliable metal interconnect layers in the following steps.

![Screenshot 2025-06-19 162316](https://github.com/user-attachments/assets/76aea474-8dfa-4929-b5f5-a35027843532)

Now, using **Mask 12** and **photoresist**, we define the regions where metal contacts or interconnects need to be formed:

1. **Photoresist** is applied over the planarized SiO₂ layer.
2. The wafer is exposed using **Mask 12**, which defines the via/contact openings.
3. After development, the **exposed SiO₂** is **etched** to create **vias or trenches** where the metal will be deposited.

![Screenshot 2025-06-19 162328](https://github.com/user-attachments/assets/57c8179e-9890-4c4d-ae86-a81870e44093)

Now, remove the photoresist and deposit a thin layer of TiN (\~10 nm) over the wafer. TiN serves as an excellent adhesion layer for SiO₂ and also acts as a barrier between the bottom layer and the top metal interconnect layer.

![Screenshot 2025-06-19 162343](https://github.com/user-attachments/assets/e60a7c1a-c6e6-453c-b610-74fc1ed9b978)

Next step is to deposit a blanket layer of tungsten (W) over the wafer. After deposition, perform CMP (Chemical Mechanical Polishing) to planarize the surface.

![Screenshot 2025-06-19 162352](https://github.com/user-attachments/assets/19fba74c-4e58-40c0-b044-6dda7f5bec74)

This tungsten (W) fills the contact holes, enabling vertical connections. These holes need to connect to the higher metal layer, so we now deposit a layer of aluminium (Al) over the wafer.

![Screenshot 2025-06-19 162412](https://github.com/user-attachments/assets/c02d1559-e1d1-48cf-9f8b-a8f40d9b34d2)

Then, using **Mask 13** and **photoresist**, we perform **plasma etching** to remove the unwanted **tungsten (W) layer**, leaving contacts only at the specified locations.

![Screenshot 2025-06-19 162422](https://github.com/user-attachments/assets/e8a4a0ec-a426-4058-a7ed-30bbc691aa0f)

This completes the formation of the **first level of metal interconnects**. Now, we repeat the **same process** to form the **second level of metal interconnects**:

* Use **Mask 14** to **etch out the SiO₂ layer** and define vias for the second metal layer.
* Then use **Mask 15** to **etch the aluminium (Al) layer**, forming the desired metal routing for the second level.

![Screenshot 2025-06-19 162434](https://github.com/user-attachments/assets/702dabeb-ade2-403c-8854-a3f791d32409)

The upper layer of aluminium (Al) is slightly thicker compared to the lower layer of Al. Now, deposit a layer of SiO₂ or Si₃N₄ over the entire surface to protect the chip.

![Screenshot 2025-06-19 162443](https://github.com/user-attachments/assets/7b625455-d1d2-4320-b565-dfbd3111b19e)

And finally, after completing all the fabrication steps, our **CMOS structure** appears as shown—fully formed with multiple metal layers, interconnects, and protective passivation, ready for packaging and further testing.

![Screenshot 2025-06-19 162455](https://github.com/user-attachments/assets/33d5fe4a-062a-4837-be42-6a24b472e607)

---
### Lab introduction to Sky130 basic layers layout and LEF using inverter
---
In SKY130, each **color represents a specific layer** of the CMOS layout:

* The **first layer** (local interconnect) is shown in **blue-purple**.
* The **second layer**, **Metal 1**, appears in **light purple**.
* **Metal 2** is represented by the **pink** color.
* The **N-well** is indicated by a **solid dashed line**.
* **Green** shows the **N-diffusion** region.
* **Red** represents the **polysilicon gate**.
* **Brown** is used for the **P-diffusion** region.

In the **Tckon window**, you can select a region to identify the transistor type. For example, selecting a specific area shows it as **NMOS**, and similarly, you can check for **PMOS**.
This is how we **verify and inspect the CMOS structure**, ensuring it is functioning as expected.

![image](https://github.com/user-attachments/assets/68afb512-5236-4414-b50f-2b7feb5dc4b2)

we can see the information of layer by placing our cursor on different colors

![image](https://github.com/user-attachments/assets/ef9a5a76-091d-435f-9d7e-719c9d3f1a0c)

when the poly crosses N-diffusion then the device is a NMOS and if it crosses P-diffusion then the device is a PMOS.

![image](https://github.com/user-attachments/assets/73cc357e-a2f4-4847-95e5-3331ec74582c)

![image](https://github.com/user-attachments/assets/9b3577ab-c102-4219-bd71-d2676712f234)

Similarly, we will check the **output terminal** as well — by **double pressing "S"**, we can **select the entire connected structure** at the output node **Y**.

![image](https://github.com/user-attachments/assets/7a741d93-b875-4bc6-91d5-525ff4aecb29)

So, we can observe that **"Y" is connected to the local interconnect** in the **cell definition of sky130\_inv**.
We can also verify whether the **source of the PMOS is connected to VDD**, and similarly, check if the **source of the NMOS is connected to GND**.

---
### Lab steps to create std cell layout and extract spice netlist
---

To understand the **logical functioning of the inverter**, the first step is to **extract its SPICE netlist** and then simulate it using the **NGSPICE open-source tool**.

1. Open the **Tkcon** window and check the current path using the command:

   ```
   pwd
   ```
![Screenshot 2025-06-20 102113](https://github.com/user-attachments/assets/5e44f630-e7bf-414f-a9de-acfe698a4de2)

2. Create an extraction file by using the command:

   ```
   extract all
   ```
![Screenshot 2025-06-20 102113](https://github.com/user-attachments/assets/c731c7bf-ae35-4484-997f-022b2ed89260)

3. Go to the working directory and verify whether the file **sky130\_inv.ext** has been generated.

![Screenshot 2025-06-20 102148](https://github.com/user-attachments/assets/51cd8c03-fd53-407d-81c1-89eff9c1c728)

4. Now, to generate the SPICE netlist (including parasitic capacitances), use the following command:

   ```
   ext2spice cthresh 0 rthresh 0
   ```
![Screenshot 2025-06-20 125638](https://github.com/user-attachments/assets/089fccda-4f01-4410-87ba-5312218f52c0)

 This extracts **all parasitic capacitance** values. Note that this step **does not create any new folder**.

5. Finally, use the command:

   ```
   ext2spice
   ```
![Screenshot 2025-06-20 125638](https://github.com/user-attachments/assets/1e79d9db-46ea-458a-b1d0-006777bc4349)

This generates the **.spice file**, which can now be used for simulation in **ngspice**.

![Screenshot 2025-06-20 102918](https://github.com/user-attachments/assets/34f7b24a-d27d-4028-9c9c-fa52f6e8622c)

contents of the .spice file 

![image](https://github.com/user-attachments/assets/2f44194e-6956-4c4f-97c7-d300720ec9a5)

---
## Sky130 Tech File Labs
---
### Lab steps to create final SPICE deck using Sky130 tech
---
Now we have to edit the above file for our ngspice simulation.
To measure the smallest dimenion we do the following steps as shown in the pictures below:
Select the smallest grid box and then in the Tcon terminal type the command "box"

![Screenshot 2025-06-24 100746](https://github.com/user-attachments/assets/637d3399-acea-4a13-a233-0d14f8f408fa)

![Screenshot 2025-06-24 100815](https://github.com/user-attachments/assets/3f1ea963-7c06-477c-ba7e-06fbfbe179b9)

so our scale is 0.01u

---
![Screenshot 2025-06-20 130328](https://github.com/user-attachments/assets/50ab0942-7ff2-480c-9cd8-7af3bcd09b0a)

In the given netlist, we can observe complete details regarding the connectivity of the NMOS and PMOS transistors, along with the power supply connections.

Here:

* `X0` represents the **NMOS**, and
* `X1` represents the **PMOS**.

For both transistors, the connection order follows: **Gate, Drain, Substrate, Source**.

---

Now, to proceed with simulation:

We need to include the PMOS and NMOS model library files. These are located inside the `libs` folder within the `vsdstdcellsdesign` directory. To include them in the netlist, use the following commands:

![Screenshot 2025-06-24 101351](https://github.com/user-attachments/assets/bdb0bf02-b400-4977-91fc-838dbe2c6803)

```
.include ./libs/pshort.lib  
.include ./libs/nshort.lib
```

Next, define the power supply voltages:

```
VDD VPWR 0 3.3V  
VSS VGND 0 0V
```

Then, set up the input source using a pulse waveform:

```
Va A VGND PULSE(0V 3.3V 0 0.1ns 0.1ns 2ns 4ns)
```

Finally, add the commands required for simulation:

```
.tran 1n 20n  
.control  
run  
.endc  
.end
```
![Screenshot 2025-06-24 103827](https://github.com/user-attachments/assets/47478c2c-659b-4cb5-be8e-14d3556d5c01)

![Screenshot 2025-06-24 103654](https://github.com/user-attachments/assets/d5f9db3e-5e05-4ee8-9582-1bdf5d6340d8)

---
Now running the ngspice

![Screenshot 2025-06-24 104237](https://github.com/user-attachments/assets/685db0bd-8432-4a94-8b3a-df1722a538a2)

output of ngspice 

![Screenshot 2025-06-24 104641](https://github.com/user-attachments/assets/2f180e60-c6d8-4f27-9b73-9f120d8cd452)

Now, ploting the graph here by command, plot y vs time a.

![Screenshot 2025-06-24 112315](https://github.com/user-attachments/assets/426fcf27-f994-4c31-b1f5-c633c2764cb3)

![Screenshot 2025-06-24 112505](https://github.com/user-attachments/assets/556c8565-6a8f-46e6-9759-e0897a869497)

If we increase the value of C3 from 0.024fF to 2fF, the output waveform becomes noticeably smoother. This happens because the larger capacitance slows down the voltage transitions, effectively filtering out sharp edges and noise from the signal.

![Screenshot 2025-06-24 112815](https://github.com/user-attachments/assets/191e5a42-9b94-4582-9897-ca62eb6e1a10)

![Screenshot 2025-06-24 112854](https://github.com/user-attachments/assets/e2caa4b3-34f6-4a2c-9075-3eaf58f1ef45)

---
### Lab steps to characterize inverter using sky130 model files
---

Now that we have obtained the transient response, our next step is to **characterize the cell** by calculating four key parameters:

1. **Rise Time (tr)** – The time taken for the output waveform to transition from **20% to 80% of its maximum value** during a rising edge.
2. **Fall Time (tf)** – The inverse of rise time; it is the time taken for the waveform to fall from **80% to 20% of its maximum value** during a falling edge.
3. **Propagation Delay (tpd)** – The time delay between the input transition (either rising or falling) and the corresponding output transition crossing the 50% voltage level.
4. **Cell Fall Delay** – Specifically refers to the propagation delay when the **output transitions from high to low**, typically measured from the **rising edge of the input to the falling edge of the output** at their respective 50% voltage points.

Calculation of Rise time:
Maximum value of waveform is 3.3V (as defined in spice lib)
20% of 3.33 is:

$$
= \frac{20}{100} \times 3.33 = 0.666
$$

So, **0.666V**.

By zooming into our waveform near **0.66V** (which is **20% of 3.3V**), we observe that the corresponding time is approximately **2.18197 ns**.
Similarly, we calculate **80% of 3.3V**, which is:

$$
= \frac{80}{100} \times 3.3 = 2.64V
$$

Then, by locating the point on the waveform where the voltage reaches **2.64V** we note the corresponding time value = **2.24598 ns** 

The **rise time** can be calculated as:

$$
\text{Rise Time} = 2.24598 \, \text{ns} - 2.18197 \, \text{ns} = 0.06401 \, \text{ns}
$$

or approximately **64.01 ps**.

* **Fall Time (tf):**

$$
(4.09512 - 4.05264) \times 10^{-9} = 42.48 \, \text{ps}
$$

* **Propagation Delay (tpd):**

$$
(2.2106 - 2.15012) \times 10^{-9} = 60.48 \, \text{ps}
$$

This is measured from the **rising edge of the input** to the **falling edge or rising edge of the output** crossing the 50% point.

* **Cell Fall Delay:**

$$
(4.07735 - 4.04988) \times 10^{-9} = 27.47 \, \text{ps}
$$

This is specifically measured for the **output falling transition**, typically from the **input rising edge** (50%) to the **output falling edge** (50%).

---
### Lab introduction to Magic tool options and DRC rules
---
### CIF Format (Caltech Intermediate Form)

* **CIF (Caltech Intermediate Form)** is a standard ASCII text file format used for describing **integrated circuit (IC) layouts**.
* It is primarily used for exchanging layout data between different EDA (Electronic Design Automation) tools and for mask generation in semiconductor fabrication.

### Key Features:

* Text-based, human-readable format.
* Describes geometric shapes (polygons, rectangles) along with layer information.
* Contains scaling factors, cell definitions, and placement information.
* Simpler and more compact compared to GDSII (but less widely used now).

### Typical Uses:

* IC layout design transfer.
* Mask generation.
* Compatibility between different layout tools.

### Example Syntax:

```plaintext
DS Example ;         // Start of design
9 0 0 1000 1000;     // Boundary box
L 3;                 // Layer 3
P 4 0 0 100 0 100 100 0 100;  // Polygon with 4 points
DF ;                 // End of design
```

### Common File Extension:

`.cif`

###  **References for Magic DRC and Skywater PDK Design Rules:**

* To learn more about **Magic DRC (Design Rule Check)**, you can refer to the official Magic documentation:
  ➡️ [The Magic Technology File Manual – DRC Section](http://opencircuitdesign.com/magic/Technologyfiles/TheMagicTechnologyFileManual/DrcSection)

* The detailed **Skywater PDK Design Rules** are available here:
  ➡️ [Skywater PDK Documentation – Design Rules](https://skywater-pdk.readthedocs.io/en/main/rules/periphery.html)

* For additional reference, including files, models, and open-source resources, the official **Google Skywater PDK GitHub repository** can be accessed here:
  ➡️ [Google Skywater PDK GitHub Repository](https://github.com/google/skywater-pdk)

---
### Lab introduction to Sky130 pdk's and steps to download labs
---

Follow the steps:

First, go to the home directory.

To download the lab files for performing DRC corrections:

```
wget http://opencircuitdesign.com/open_pdks/archive/drc_tests.tgz
```
![Screenshot 2025-06-25 131302](https://github.com/user-attachments/assets/a77450e7-5a53-4609-9ffd-55ea39aecf48)

To extract the lab files from the downloaded file:

```
tar xfz drc_tests.tgz
```

Navigate inside the extracted folder `drc_tests`:

```
cd drc_tests
```

To list all the directories:

```
ls -al
```
![Screenshot 2025-06-25 131416](https://github.com/user-attachments/assets/e73d4185-afa7-4908-a521-78d5e3dc7e71)

To view the `.magicrc` file:

```
gvim .magicrc
```
![Screenshot 2025-06-25 131558](https://github.com/user-attachments/assets/1efe425a-69d6-4080-b4cf-af273e3e1dcf)
![Screenshot 2025-06-25 131630](https://github.com/user-attachments/assets/8a784d30-893a-4332-9666-1cc5f1f86cf1)

The `.magicrc` file serves as the startup script for Magic and specifies the location of the technology file. The technology file is available locally in the same directory and can be modified if needed.

To start Magic with better graphics support:

```
magic -d XR &
```
---
### Lab introduction to Magic and steps to load Sky130 tech-rules
---

Use the command below to open the Magic tool with improved graphics:

```
magic -d XR &
```

After Magic opens, go to the **File** menu and select **Open**, then choose the file:

```
met3.mag
```

This file contains different layout patterns, each associated with various **DRC violations**, represented as **rule numbers**. Each number corresponds to a specific design rule being violated in that region of the layout.

![Screenshot 2025-06-25 133028](https://github.com/user-attachments/assets/c06e14ab-ca7e-4ef7-a518-7d1b0f1da0b8)

These rule numbers can be found in the **Google-Skywater PDK documentation**, which provides detailed explanations of each design rule, including layer specifications, spacing, width, enclosure, and other constraints. The reference for these rules is available at:

```
https://skywater-pdk.readthedocs.io/en/main/rules/periphery.html
```
![Screenshot 2025-06-25 133455](https://github.com/user-attachments/assets/3d311ab8-8c3c-4ad2-82ac-792176724da8)

Now select any layout area and check the DRC violations using the **"Why"** option in the **Tkcon** window. This command will display the reason for the DRC error, along with the corresponding rule number and a brief description of the violation.

![Screenshot 2025-06-25 134635](https://github.com/user-attachments/assets/d193a726-18fc-4321-84e1-8e460bf4304f)

![Screenshot 2025-06-25 134846](https://github.com/user-attachments/assets/79060f3f-18da-43f0-ae53-fb257e0951cb)

To viualze metal 3 and vias, select a blank area in the layout window. Hover the mouse pointer over the **Metal3 contact icon**, then press the **'p'** key to pick that icon. 
Then execute the following command in the Tkcon tab:

```
cif see VIA2
```

A group of **black squares** will appear inside the selected area. These represent the **VIA2 layer**, which indicates the vias connecting **Metal2 to Metal3**.

![Screenshot 2025-06-25 165259](https://github.com/user-attachments/assets/41687127-7d2c-4bb0-9b9e-da605ce2a36f)

---
### Lab exercise to fix poly.9 error in Sky130 tech-file
---
Now, open the **poly.mag** file in the Magic tool using the following command in the **Tkcon terminal**:

```
load poly.mag
```

This will load the **poly layout**, which can then be analyzed or edited further as required.

![Screenshot 2025-06-25 170510](https://github.com/user-attachments/assets/ad107b51-90b7-4775-9848-4ba62fe8a4f6)

Now consider the rule **poly.9** and refer to the **Google-Skywater PDK documentation** to understand the details of this rule. 

![Screenshot 2025-06-25 170909](https://github.com/user-attachments/assets/00a1d644-4f63-4537-a134-58a0eb36df6b)

The rule **poly.9** in the Google‑SkyWater PDK specifies:

![Screenshot 2025-06-25 171006](https://github.com/user-attachments/assets/3875bc26-585f-476a-94e0-9b52f796a5cb)

![Screenshot 2025-06-25 171158](https://github.com/user-attachments/assets/86d63d3f-4fa8-4f96-8395-410df17ed955)


> **Minimum spacing between poly‑resistor and either poly (non‑resistor) or diffusion/tap:** **0.480 µm** ([github.com][1])

### To check it in your layout:

1. Identify the layout violation marked as **poly.9** in Magic.
2. Refer to the documentation (Periphery → Design Rules) where rule number 9 lists:

   * “Poly resistor spacing to poly or spacing (no overlap) to diff/tap” = **0.480 µm** ([github.com][1])
3. Use that as the reference rule for fixing the DRC violation.

To locate the error, refer to the **sky130A.tech** file, which is available in the **drc\_tests** directory. This file can be opened using any Linux text editor for inspection and analysis.

![Screenshot 2025-06-25 171646](https://github.com/user-attachments/assets/019480f2-b684-434e-a65f-cc18171e86f7)

Search for **'poly.9'** in the **sky130A.tech** file. You will see a few DRCs but apparently there are no attempts to fix DRCs associated to distance between polyresistor to poly. So we will add these DRCs manually. Apply the necessary corrections to the **'poly.9'** rule in both sections to resolve the DRC violation.

![Screenshot 2025-06-25 172157](https://github.com/user-attachments/assets/2e5b9f2e-30fc-422d-a92a-d48279f4c8f9)

![Screenshot 2025-06-25 172308](https://github.com/user-attachments/assets/c34399b7-f743-40c9-97f3-c2bcfdd8cf99)

![dummy](https://github.com/user-attachments/assets/c84fa17d-bb6c-4e78-adff-77c7490b2882)

we can see that the distance between npolyres and poly is 0.21u and as per the poly.9 DRCs checks any distance below 0.42u should viloate the rule so its clear that there are no DRCs check rules for distance between polyres and poly and hence we add them manually.
below are the pictures showing the additions to sky130A.tech 

![Screenshot 2025-06-25 175327](https://github.com/user-attachments/assets/9467a75d-7d47-415f-8a56-a571e5ed761e)

![Screenshot 2025-06-25 175358](https://github.com/user-attachments/assets/00eae76a-65cb-45c6-b6af-ed21de378642)

---
### Lab exercise to implement poly resistor spacing to diff and tap
---
To correctly implement the **poly resistor spacing**, modifications need to be made again in the **sky130A.tech** file. This involves adjusting the spacing rules under the relevant sections to ensure compliance with the design rule requirements.


now load the file using the command **tech load sky130A.tech** in the tcon window and then use the command **drc check**

![Screenshot 2025-06-25 181220](https://github.com/user-attachments/assets/c4810011-fbe5-4f2c-9ca4-7bc1e9ba13b5)

---
# Day 4 - Pre-layout timing analysis and importance of good clock tree
---
## Timing modeling using delay tables
---
### Lab steps to convert grid info to track info
---
Now, we need to extract the **`.lef` file** from the **`.mag` file** so that it can be used in the **picorv32a flow**.

There are specific guidelines that must be followed when designing standard cells:

* The **input and output ports** should be placed exactly at the **intersection of vertical and horizontal tracks**.
* The **width** of the standard cell should be an **odd multiple of the horizontal track pitch**, and the **height** should be an **odd multiple of the vertical track pitch**.

To check the track pitch details, open the **track.info** file located at:

```
pdk/sky130/libs.tech/openlane/sky130_fd_sc_hd/track.info
```

This file provides information about the routing tracks, which is essential for ensuring that the cell aligns correctly with the routing grid during physical design.

![Screenshot 2025-06-26 120757](https://github.com/user-attachments/assets/f4b0fe92-8ca1-4934-9b58-8fe1abc3bdc6)

![Screenshot 2025-06-26 120830](https://github.com/user-attachments/assets/29c498d6-f6f9-41b9-8d42-d9246a59eb2c)

![Screenshot 2025-06-26 121043](https://github.com/user-attachments/assets/e2137b70-6fa7-47af-9d19-f55462021324)

![Screenshot 2025-06-26 121230](https://github.com/user-attachments/assets/174d0f03-6a1f-44e4-a928-cfc776577366)

* The entry **`li1 x 0.23 0.46`** indicates that for the **li1 metal layer**, the **horizontal offset is 0.23** and the **pitch is 0.46**.
* Similarly, **`li1 y 0.23 0.46`** means the **vertical offset is 0.23** and the **vertical pitch is 0.46**.

According to the standard cell guidelines, the **ports should be placed at the intersection of the horizontal and vertical tracks** of the **li1 metal layer**, since the ports are defined in the **li1 layer**.

To verify this in **Magic**, press the **`g` key** to enable the grid. Upon zooming in, small boxes will appear which act as references for layout alignment.

![Screenshot 2025-06-26 123059](https://github.com/user-attachments/assets/cff2a8bc-273c-41ee-9d08-cd76e68aab97)

Next, we align this grid with the **track pitch values (offset = 0.23, pitch = 0.46)** to verify whether the ports **A** and **Y** are correctly placed at the intersections of the **horizontal and vertical tracks** of the **li1 metal layer**.

Now, open the Tkcon window and, using the reference from the track.info file, set the grid according to the given offset and pitch values. The commmands are shown in the picture below.

![Screenshot 2025-06-26 123618](https://github.com/user-attachments/assets/b82a6dda-1f56-40ae-aa24-57458a132644)

after pressing enter u see the following changes in the magic tool

![Screenshot 2025-06-26 123655](https://github.com/user-attachments/assets/1e993c55-9f17-456e-8811-50ea997a6a65)

so the routing of li1 layer can only happen along this grid as shown above.
we can also see that the input and output port is at the intersection of horizontal and vertical metal layer.

![Screenshot 2025-06-26 124033](https://github.com/user-attachments/assets/37cbbde0-448e-4609-87ac-a5e24e88fdc1)

The intersection ensures that the routing can connect to the port from both the **horizontal and vertical directions** effectively.
Now, we can observe that the ports are placed exactly at the **intersection of the tracks**, satisfying the first requirement. Additionally, within the cell boundaries, **3 grid boxes are covered**, which confirms that the **second requirement related to the cell width being an odd multiple of the track pitch is also satisfied**.

---

### Lab steps to convert magic layout to std cell LEF
---

### **`port class`**

Defines the **direction** of the port.

* **`INPUT`** – The port is an input.
* **`OUTPUT`** – The port is an output.
* **`INOUT`** – The port is bidirectional (can act as both input and output).

---

### **`port use`**

Defines the **functional purpose** of the port.

* **`SIGNAL`** – Regular signal port (input/output/inout).
* **`POWER`** – Power supply port (e.g., VDD).
* **`GROUND`** – Ground port (e.g., VSS).
* **`CLOCK`** – Clock signal port.
* **`ANALOG`** – Analog signal port (if applicable).

![Screenshot 2025-06-26 140556](https://github.com/user-attachments/assets/5d0ef364-5125-4ca0-817b-621924e4b253)

After these parameters are set (which is already configured for us), we are now ready to extract the **.lef** file from the **.mag** file.

before we extract lets give this cell a coustom name. Right now the cell name is sky130_inv.
follow the below image.

![Screenshot 2025-06-26 141953](https://github.com/user-attachments/assets/3c912022-1bbb-4288-a0b5-a665178a4adb)

![Screenshot 2025-06-26 142037](https://github.com/user-attachments/assets/7315204e-eca7-4a14-9bc8-6033e70871ee)

Now, open the layout file in Magic using the following command:

```
magic -T sky130A.tech sky130_vsdinv.mag &
```

To extract the **.lef** file, enter the following command in the **Tkcon window**:

```
lef write
```

![Screenshot 2025-06-26 142714](https://github.com/user-attachments/assets/4f36518b-b1da-4a3d-82cd-52d3d3cec215)

This will generate the **.lef** file in the **vsdstdcellsdesign** directory. You can verify its creation by using the command:

```
ls -ltr
```
![Screenshot 2025-06-26 142741](https://github.com/user-attachments/assets/48e15306-9543-4549-93dd-fd492d1bd2d7)

The contents of the .lef file generated is shown below

![Screenshot 2025-06-26 143312](https://github.com/user-attachments/assets/e174a46f-beaf-424d-8c98-737f12c5566b)

![Screenshot 2025-06-26 143337](https://github.com/user-attachments/assets/32a5d359-ba03-4a96-85e4-f9be737e52e1)

![Screenshot 2025-06-26 143350](https://github.com/user-attachments/assets/7fefbe7b-1423-4b08-8d39-852e767f633b)

---
### Introduction to timing libs and steps to include new cell in synthesis
---
Now that the **.lef** file has been generated, the next step is to integrate it into **picorv32a**. Before proceeding, the file needs to be moved to the **src** folder, where all the design files are located in one place.

To do this, use the **`cp`** command to copy the file:

```
cp sky130_vsdinv.lef /home/vsduser/Desktop/work/tools/openlane_working_dir/openlane/design/picorv32a/src
```

This will place the **.lef** file into the **src** directory, ready to be used in the picorv32a design flow.

![Screenshot 2025-06-26 165102](https://github.com/user-attachments/assets/1002222a-e54c-41f1-aad2-7ac44a25f5f2)

![Screenshot 2025-06-26 165155](https://github.com/user-attachments/assets/db78c8c1-2166-4ceb-a602-e9cdbb8c2fd3)

Now, we need to include the **custom cell** in the **OpenLane flow**, and the first step in the OpenLane flow is **synthesis**.

During the synthesis process, the **ABC step** maps the netlist to the cells present in the library. Therefore, it is necessary to have a library that includes the **definition of our custom cell** for successful synthesis.

To proceed, open the **library file** as shown in the image below and verify that the custom cell entry is present in it.

![Screenshot 2025-06-26 165851](https://github.com/user-attachments/assets/6765479d-5cd6-4b31-a30e-9e985b47e83a)

below are the contents of sky130_fc_sc_hd_typical.lib


![Screenshot 2025-06-26 170035](https://github.com/user-attachments/assets/c60c45c8-cd46-4510-9317-524f19d7a6ad)

![Screenshot 2025-06-26 170156](https://github.com/user-attachments/assets/582315ef-358b-4062-a0cd-f81b8c5a1973)

![Screenshot 2025-06-26 170213](https://github.com/user-attachments/assets/f220fded-613c-4bc5-883a-944fb93c49ce)

![Screenshot 2025-06-26 170232](https://github.com/user-attachments/assets/90e510be-ddc4-457f-af69-9ee4a7694617)

![Screenshot 2025-06-26 170248](https://github.com/user-attachments/assets/b0fdd69f-e0cb-4f66-8f48-de6390d5f560)

This is how the **library file** appears. There are multiple library files available, typically categorized based on process corners such as **typical**, **slow**, and **fast**. Each library represents different operating conditions:

* **Typical** – Standard or nominal process, voltage, and temperature conditions.
* **Slow** – Worst-case slow silicon performance.
* **Fast** – Best-case fast silicon performance.

Our custom cell needs to be added to all relevant libraries to ensure it is available across all corners during synthesis and further stages of the OpenLane flow.

now we will copy all the libraries into the src folder

![Screenshot 2025-06-26 165851](https://github.com/user-attachments/assets/e8c4bcf2-f7ca-4e05-9ca6-168a3b9aab47)

![Screenshot 2025-06-26 171206](https://github.com/user-attachments/assets/e2db740b-ca95-4ded-916e-4e6db2433718)

![Screenshot 2025-06-26 171402](https://github.com/user-attachments/assets/7141351c-0623-4d64-9cd3-030a026443f5)

Here, we need to modify the **`config.tcl`** file located in the **picorv32a** directory.

Open the **`config.tcl`** file and add the commands shown in the image below. These commands are necessary to include the custom cell in the OpenLane flow, allowing the synthesis and implementation process to recognize and use the newly created cell.

before addition:

![Screenshot 2025-06-26 171945](https://github.com/user-attachments/assets/258c8625-d3ef-419f-abe1-de9fb0668d35)

after addition:

![Screenshot 2025-06-26 172946](https://github.com/user-attachments/assets/7117cdbd-cae1-43c5-9c9e-d5e079e20846)

### OPENLANE:

Now, go to the **OpenLane** directory and execute the docker command.

Then, execute the following commands sequentially in the same session:

```
./flow.tcl -interactive
package require openlane 0.9
prep -design picorv32a -tag "latest directory name that i have in my runs folder" -overwrite // This is to continue my runs in the same directory as previous
set lefs [glob $::env(DESIGN_DIR)/src/*.lef]
add_lefs -src $lefs
run_synthesis
```

This process prepares the design, adds the custom **.lef** files to the flow, and initiates the **synthesis step** for the **picorv32a** design.

![Screenshot 2025-06-27 091911](https://github.com/user-attachments/assets/28e6a026-e5fb-4378-aa74-2dc0804bb72a)

![Screenshot 2025-06-27 092116](https://github.com/user-attachments/assets/268a2275-8522-483f-80b0-2884c315761b)

![Screenshot 2025-06-27 092257](https://github.com/user-attachments/assets/d2c7378d-90cf-438e-99ee-1e040e9396e4)

![Screenshot 2025-06-27 092402](https://github.com/user-attachments/assets/7c14d79c-6e6c-48dd-97b0-9aeea6190eec)

some results of synthesis 

![Screenshot 2025-06-27 093001](https://github.com/user-attachments/assets/1a16eefc-99fc-4fac-a186-a2bb6d55472a)

![Screenshot 2025-06-27 093014](https://github.com/user-attachments/assets/c261803e-0be6-42bd-a369-4f3385e3dbc3)

we see a huge slack violation in the synthesis stage itself. So now we have to correct this slack violation.
---
### Introduction to delay tables
---
### Power Aware CTS:

If the **enable pin** of an **AND gate** is set to **logic '1'**, the clock signal will propagate. If it is set to **logic '0'**, the clock will be blocked.

Similarly, for an **OR gate**, when the **enable pin** is set to **logic '0'**, the clock propagates, and when set to **logic '1'**, it blocks the clock.

The main advantage of this **clock blocking** mechanism is **power saving**. During the blocked periods, unnecessary clock switching activity is avoided in parts of the circuit, leading to significant power reduction in the clock tree.

![image](https://github.com/user-attachments/assets/9bb4ae1e-25f2-4471-9991-2d48742dd8bb)

Let's consider a clock tree where a buffer at the first stage is driving the load of two downstream buffers. In the **clock gating technique**, we replace this buffer with an **AND gate** to control the clock based on the enable signal.

By doing this swap, we will now observe whether the other characteristics—such as **delay, load driving capability, transition time, and power consumption**—remain the same or change due to this modification. These impacts will be analyzed in the following steps.

![Screenshot 2025-06-26 194648](https://github.com/user-attachments/assets/4b4d4a10-2322-4225-9c4f-9a6bc6aac921)

Before swapping the buffer with the gate, we have made the following assumptions:

1. The **input transition** and **load capacitance** remain the same before and after replacing the buffer with the gate.
2. The **driving strength** of the gate is assumed to be comparable to that of the buffer.
3. The overall **clock frequency** and **operating conditions** do not change.
4. Only the **functional block (buffer to AND gate)** is swapped, while the rest of the clock tree structure remains unchanged.
5. Any added logic for gating does not introduce functional errors; it only controls clock propagation based on the enable signal.

These assumptions will help in accurately analyzing the impact of the swap on parameters like **delay, transition, and power consumption** in the coming steps.

![Screenshot 2025-06-26 194700](https://github.com/user-attachments/assets/09705021-1c5b-4fd8-bf6c-e548d1e32914)

Assume the following capacitance values:

* **C1 = C2 = C3 = C4 = 25 fF**
* **Cbuf1 = Cbuf2 = 30 fF**

The total capacitance at each node is:

* **Node A → 60 fF**
* **Node B → 50 fF**
* **Node C → 50 fF**

### Observations:

* The circuit consists of **2 levels of buffering**.
* At each level, every node drives the **same load**.
* **Identical buffers** are used at the same level.
* The **output capacitance of the buffers is not constant** across the circuit; the load at each output varies.
* Due to this varying output load, the **input transition time also varies**.

As a result, the circuit experiences **multiple delay values** depending on the varying input transitions and output loads.

### How is this delay captured?

This is done using **delay tables**.

### Preparation of Delay Tables:

* A single buffer is extracted from the circuit.
* The **input transition** is varied within a defined range (e.g., **10 ps to 100 ps**).
* Simultaneously, the **output load** is also varied.
* The corresponding **delay values are measured and recorded**.
* This data is organized into a **tabular format**, forming the delay table that models how delay changes with input transition and output load.

![image](https://github.com/user-attachments/assets/be4c3efb-2cd1-49b8-b506-4e20839520d4)

---
### Delay Table Usage – Part 1
---
Let's take the example of the other buffers.
Using the delay table, we can check how the delay of each buffer changes with different input transition and output load. As the load and transition are different for every buffer, delay will vary.
The delay table captures this variation accurately by giving the delay corresponding to a particular input transition and load.

![Screenshot 2025-06-26 195122](https://github.com/user-attachments/assets/f854055e-abdc-4223-8a7b-8af4f54f4d2d)

For a practical example, let's say we have the **input transition of 40ps** for **buffer1** and the **output capacitance** of this buffer is **60fF**. The delay of the cell in this case lies between **x9-x10**.
The values which are not available in the delay table are extrapolated from the given data, so we can take the range in that case.

---
### Delay Table Usage – Part 2
---

Now we have to calculate the delay of **buffer2**, and after that, we can find the **latency at the 4 clock endpoints**.
Here, the **input transition is common for both the buffers**. Assuming the transition is around **60ps** and the **load at both buffers is 50fF**, it will give the delay of **y15**.
The total delay from input to output is **x9' + y15** (here, we are ignoring the delay of the wires). This means the **skew at any output point is zero**.
If the **load is not the same at every node**, then the **skew will not be zero**.

---
### Lab Steps to Configure Synthesis Settings to Fix Slack and Include VSDINV
---

We will try to modify the parameters of our cell by referring to the **README.md** file located in the **configuration folder** inside the **OpenLane directory**.
The **README.md** file contains detailed information about the **parameters of the cell**, which will help in adjusting the synthesis settings as needed.

![Screenshot 2025-06-27 104405](https://github.com/user-attachments/assets/f009b376-a1a4-4e7d-8a70-2b1649169d50)

What is WNS and TNS?
WNS (Worst Negative Slack): The worst (most negative) slack among all timing paths in the design. If WNS is negative, it indicates the most critical timing violation in the design.
TNS (Total Negative Slack): The sum of all negative slack values across all violating timing paths in the design. It indicates the overall severity of the timing violations.

![Screenshot 2025-06-27 093014](https://github.com/user-attachments/assets/0ef3a4c5-fd2a-4c6f-82b6-238cb1a2cc11)

![Screenshot 2025-06-27 103558](https://github.com/user-attachments/assets/78059997-c2d4-4d33-8132-4c0a7824a62a)

Let's see if we can repair this **slack**. For this, we perform a **timing-driven synthesis** where we try to balance between **delay and area**.

In the **README.md** file, we find that the strategy named **SYNTH\_STRATEGY** focuses on **timing-driven synthesis**.

Currently, the **chip area** is **147712.918400**.

* **TNS (Total Negative Slack)** is **-711.59**.
* **WNS (Worst Negative Slack)** is **-23.89**.

In the OpenLane window, type the command:

* Now, once again, we have to **prep the design** to update the variables:

```
prep -design picorv32a -tag 24-03_10-03 -overwrite
```

* Additional commands to **include the newly added LEF file** into the OpenLane flow:

```
set lefs [glob $::env(DESIGN_DIR)/src/*.lef]
add_lefs -src $lefs
```

* Command to **display the current value of `SYNTH_STRATEGY`:**

```
echo $::env(SYNTH_STRATEGY)
```

* Command to **set a new value for `SYNTH_STRATEGY`:**

```
set ::env(SYNTH_STRATEGY) "DELAY 3"
```

* Command to **check whether `SYNTH_BUFFERING` is enabled:**

```
echo $::env(SYNTH_BUFFERING)
```

* Command to **check the current value of `SYNTH_SIZING`:**

```
echo $::env(SYNTH_SIZING)
```

* Command to **set a new value for `SYNTH_SIZING`:**

```
set ::env(SYNTH_SIZING) 1
```

* Command to **display the current value of `SYNTH_DRIVING_CELL`** to verify whether it's set to the proper cell:

```
echo $::env(SYNTH_DRIVING_CELL)
```

* Now that the design is prepped and ready, run the **synthesis** using the following command:

```
run_synthesis
```
![Screenshot 2025-06-27 160158](https://github.com/user-attachments/assets/34ac4592-cb3c-481c-b905-71fd9f45047f)

![Screenshot 2025-06-27 160548](https://github.com/user-attachments/assets/a65bf3b9-8016-4c43-b44b-3938bd2236cb)

Now we see that the area has increased

![Screenshot 2025-06-27 161054](https://github.com/user-attachments/assets/ff745301-0286-46cd-a564-88583afbffdb)

and the slack is fixed

![Screenshot 2025-06-27 161009](https://github.com/user-attachments/assets/1e43a5ba-6392-4aeb-a8b5-701cbc9dfe7d)

Once the synthesis has accepted our **custom inverter**, we can now proceed to run **floorplan** and **placement** to verify that the cell is properly accepted in the **PnR flow**.

Now that our custom inverter is successfully integrated into the synthesis, we can run the **floorplan** using the following command:

```
run_floorplan
```
![Screenshot 2025-06-27 161617](https://github.com/user-attachments/assets/53c036d9-6d67-4fd7-8b80-1f859fab96ea)

![Screenshot 2025-06-27 161927](https://github.com/user-attachments/assets/162d2277-f7e6-4351-a97e-6e6056540e3b)

Since we are facing an unexpected, unexplained error while using the `run_floorplan` command, we can instead use the following set of commands. These are derived from the file:

```
Desktop/work/tools/openlane_working_dir/openlane/scripts/tcl_commands/floorplan.tcl
```

and from the Floorplan Commands section in:

```
Desktop/work/tools/openlane_working_dir/openlane/docs/source/OpenLANE_commands.md
```

These commands are internally sourced within the `run_floorplan` command:

```
init_floorplan
place_io
tap_decap_or
```

Using these commands step-by-step can help bypass the issue with `run_floorplan` and proceed with the floorplanning process manually.

![Screenshot 2025-06-27 163055](https://github.com/user-attachments/assets/9c712cb5-8855-4202-872a-f9bc497fbedd)

![Screenshot 2025-06-27 163126](https://github.com/user-attachments/assets/a2a65b4b-1995-4211-9251-4cc695d2f77d)

Now that the floorplan is done we can do placement.
run_placement 

![Screenshot 2025-06-27 163553](https://github.com/user-attachments/assets/6283456d-03c1-4050-8a9a-622723d8b2cb)

![Screenshot 2025-06-27 163743](https://github.com/user-attachments/assets/92c02110-ec19-44b8-9243-c8642bd338a4)

Now lets visualize our placement in magic tool 

![Screenshot 2025-06-27 165919](https://github.com/user-attachments/assets/18f11bdb-8950-4170-81bd-6f5064f1a973)

Screenshot of Custom Inverter in Placement DEF with Proper Abutment
After running placement, the custom inverter can be seen correctly placed inside the placement DEF file along with standard cells.

The abutment is proper, meaning the cell edges align perfectly with neighboring cells without overlaps or gaps.

![Screenshot 2025-06-27 170515](https://github.com/user-attachments/assets/fca95004-4967-4cb8-90f1-c05a1c586e23)

zooming in

![Screenshot 2025-06-27 170515](https://github.com/user-attachments/assets/ba83b4b7-5460-457e-a625-e7b3e1a8719b)

Command in Tkcon Window to View Internal Layers of Cells:

![Screenshot 2025-06-27 170542](https://github.com/user-attachments/assets/b78d2328-0b82-4d6f-bf06-0bef42972c0e)

Abutment of Power Pins with Other Cells Clearly Visible:
When zoomed in after running the above commands, the power rails (VDD and VSS) of the custom inverter are clearly aligned and abutted with the power rails of other standard cells from the library.

This proper abutment ensures continuous power connectivity across the row in the layout.

![Screenshot 2025-06-27 170612](https://github.com/user-attachments/assets/f8d1b1eb-7b07-4232-9291-a2e4b0233e53)

---
## Timing analysis with ideal clocks using openSTA
---
### Setup timing analysis and introduction to flip-flop setup time
---
### Timing Analysis (with Ideal Clock):

Let's begin the **setup analysis** using an **ideal clock (single clock)**.

* **Clock Frequency:** 1 GHz
* **Clock Period:** 1 ns

The analysis is performed between **0** and **T (1 ns)** clock period.

* A clock edge is sent to the **launch flip-flop** at **0 ns**.
* The next clock edge reaches the **capture flip-flop** at **T = 1 ns**.

Let's assume the **combinational delay is θ (theta)**.

According to **setup timing analysis**, this **combinational delay (θ)** must satisfy the condition:

```
θ < T
```

This ensures that the data launched at the first clock edge is captured correctly at the next clock edge, and the system operates correctly without setup timing violations.

![Screenshot 2025-06-27 200952](https://github.com/user-attachments/assets/557f3ead-cd64-4f2b-b41d-5cb2806ff6c0)

Now, let's open the **capture flop**, and we will observe that it contains a **combinational circuit** inside. This circuit includes multiple **MOSFETs**, various **logic gates**, along with associated **resistances** and **capacitances**.

Additionally, the **timing graph** for this particular flop shows the behavior of the signal as it travels through the internal nodes of the flop, indicating different delays introduced by the internal components like transistors and parasitics.

![Screenshot 2025-06-27 201120](https://github.com/user-attachments/assets/a924df63-6e8c-42e4-a80b-2ee4199a15b1)

When the clock is at **logic '0' or logic '1'**, the **delay of MUX1 and MUX2** affects or restricts the **combinational delay requirement**.

There is a **finite amount of time** required for the **D input** to stabilize before the clock edge. This time is referred to as the **setup time (S)**.

Hence, the data input must arrive and settle **'S' time units before the clock edge** to be correctly captured at **Qm**.

The **internal delay of MUX1 is equivalent to the setup time (S)**.

Therefore, the original condition:

```
θ < T
```

is modified to:

```
θ < (T - S)
```
---
### Introduction to Clock Jitter and Uncertainty:
---

* **Clock jitter** occurs when the clock, typically generated by a **PLL (Phase-Locked Loop)**, fails to produce clock edges at the exact expected times like **0, T, 2T...**
* This happens due to internal variations in the clock source.
* **Jitter** refers to the **temporary variation in the clock pulse timing**, causing the clock edges to arrive slightly earlier or later than expected.
* Jitter directly affects timing margins, increasing the risk of setup and hold violations.

![image](https://github.com/user-attachments/assets/26642583-dc04-4255-b3aa-ffc846e31c80)

Considering the **uncertainty time (US)**, the equation updates to:

```
θ < (T - S - US)
```

Assuming **S = 0.01 ns** and **US = 0.09 ns**, let's apply this condition.

Now, let's identify the **timing paths** in the circuit. Both **Stage 1** and **Stage 3 logic paths** operate under a **single clock domain**.

Next, we need to determine the **combinational path delay** for both **Stage 1** and **Stage 3** logic paths.

![image](https://github.com/user-attachments/assets/ad87ca08-59bd-4055-9bb8-8a0970f9f00f)

![image](https://github.com/user-attachments/assets/dc38faa7-98ff-428d-9d78-6a23bbc777fe)

---
### Lab steps to configure OpenSTA for post-synth timing analysis
---

Since we have achieved **0 WNS** after the improved timing run, we will now perform **timing analysis on the initial synthesis run**, which contains **multiple violations** as no parameters were applied to optimize the timing.
Below are the commands to **invoke the OpenLANE flow**, **include the new LEF**, and **run synthesis**.

* **Change the directory to the OpenLANE flow directory:**

```
cd Desktop/work/tools/openlane_working_dir/openlane
```

* **Invoke the OpenLANE Docker container:**
  Since the long Docker command is already aliased to `docker`, we can simply run:

```
docker
```

* **Start the OpenLANE flow in interactive mode:**

```
./flow.tcl -interactive
```

* **Load the required package for OpenLANE functionality:**

```
package require openlane 0.9
```

* **Prepare the design by creating the necessary files and directories. In this case, the design is `picorv32a`:**

```
prep -design picorv32a
```

* **Include the newly added LEF files into the OpenLANE flow:**

```
set lefs [glob $::env(DESIGN_DIR)/src/*.lef]
add_lefs -src $lefs
```

* **Set the `SYNTH_SIZING` variable to enable cell sizing:**

```
set ::env(SYNTH_SIZING) 1
```

* **Run synthesis for the design:**

```
run_synthesis
```

![Screenshot 2025-06-28 115910](https://github.com/user-attachments/assets/6770a960-7cd2-45ab-bcd2-d5d06c5eaa24)

![Screenshot 2025-06-28 115933](https://github.com/user-attachments/assets/e72889f4-5e0a-40fa-b0cc-ecc88166d0f9)

Newly created pre_sta.conf for STA analysis in openlane directory

![Screenshot 2025-06-28 120348](https://github.com/user-attachments/assets/0ebf01fd-18b0-4e28-af0d-eb801e8105cf)

The newly created **`my_base.sdc`** file for **STA (Static Timing Analysis)** is placed in the following directory:

```
openlane/designs/picorv32a/src
```

This file is created based on the reference from:

```
openlane/scripts/base.sdc
```

The **`my_base.sdc`** file defines timing constraints such as clock definitions, input/output delays, and other constraints necessary for accurate STA analysis during the OpenLANE flow for the **picorv32a** design.

![Screenshot 2025-06-28 124714](https://github.com/user-attachments/assets/82ba66fa-500b-44f1-a09c-5b756a2df835)

* **Change the directory to the OpenLANE working directory:**

```
cd Desktop/work/tools/openlane_working_dir/openlane
```

* **Run OpenSTA with the required configuration file:**

```
sta pre_sta.conf
```
![Screenshot 2025-06-28 121436](https://github.com/user-attachments/assets/39bd8a72-de42-4f36-8f5c-7f919ce56a93)

This command invokes the **OpenSTA** tool and runs the static timing analysis based on the constraints and setup defined in the **`pre_sta.conf`** file.

![Screenshot 2025-06-28 131205](https://github.com/user-attachments/assets/e854cc88-516b-40f6-8b97-9cf4a568686c)

![Screenshot 2025-06-28 131222](https://github.com/user-attachments/assets/99fe3996-aef9-4c0f-b297-f7d148554c81)

![Screenshot 2025-06-28 131239](https://github.com/user-attachments/assets/2d68c954-b0cb-409d-859d-764043eaba02)

![Screenshot 2025-06-28 131303](https://github.com/user-attachments/assets/c25cd4c6-ecbc-4a10-8759-48b6c8ac0815)

![Screenshot 2025-06-28 131323](https://github.com/user-attachments/assets/a3b199fa-7286-4870-9d50-a32d0c81cb54)

---
### Lab steps to optimize synthesis to reduce setup violations
---
Since higher fanout is contributing to increased delay, we can add parameters to reduce fanout and then perform synthesis again.

* **Prepare the design by creating the required files and directories for running the design `picorv32a`:**

```
prep -design picorv32a 
```

* **Add the newly created LEF files to the OpenLANE flow:**

```
set lefs [glob $::env(DESIGN_DIR)/src/*.lef]
add_lefs -src $lefs
```

* **Set the value for `SYNTH_SIZING` to enable cell sizing:**

```
set ::env(SYNTH_SIZING) 1
```

* **Set the value for `SYNTH_MAX_FANOUT` to limit maximum fanout and reduce delay:**

```
set ::env(SYNTH_MAX_FANOUT) 4
```

* **Check the current value of `SYNTH_DRIVING_CELL` to ensure the correct driving cell is selected:**

```
echo $::env(SYNTH_DRIVING_CELL)
```

* **Run synthesis for the design:**

```
run_synthesis
```

![Screenshot 2025-06-28 143454](https://github.com/user-attachments/assets/32a924f0-a142-4fb9-b796-6283b323f74d)

![Screenshot 2025-06-28 143759](https://github.com/user-attachments/assets/b2196759-79c9-4a5e-a5d4-e6a3d7449a64)

Now, run the sta pre_sta.conf command in a new terminal in openlane directory itself,

![Screenshot 2025-06-28 143934](https://github.com/user-attachments/assets/ab79d4c5-5456-4496-acb9-4d7c77a79d7c)

![Screenshot 2025-06-28 143957](https://github.com/user-attachments/assets/c1378e38-799d-42d6-99a7-8ddcde4cf2b0)

![Screenshot 2025-06-28 144020](https://github.com/user-attachments/assets/50e53f02-c595-414c-84ae-8ae0311bb6ee)

![Screenshot 2025-06-28 144057](https://github.com/user-attachments/assets/75c7e184-08ef-4a7b-8b48-8971db346f3e)

---
### Lab steps to do basic timing ECO
---

here is the **generalized form** of the commands with **`instance_name`** and **`net_name`** placeholders instead of specific names:

* **Report all connections to a net:**

```
report_net -connections <net_name>
```

* **Check the syntax of the replace command:**

```
help replace_cell
```

* **Replace the cell with a higher drive strength cell:**

```
replace_cell <instance_name> <new_cell_name>
```

* **Generate a custom timing report with details like net capacitance, slew, and input pins:**

```
report_checks -fields {net cap slew input_pins} -digits 4
```

###  **Example usage:**

If an instance named **`or_gate_inst`** needs to be replaced with a higher drive cell like **`sky130_fd_sc_hd__or3_4`**, the command would be:

```
replace_cell or_gate_inst sky130_fd_sc_hd__or3_4
```

This format can be used for any instance in the design.

below is the Driver net whose fanout is 4 by the cell driving it has a strenghth 2

![Screenshot 2025-06-28 161312](https://github.com/user-attachments/assets/7757f3eb-6ed2-4317-9a55-438744d3f92c)

![Screenshot 2025-06-28 161442](https://github.com/user-attachments/assets/fce66a23-04f6-4a46-9d53-762e7e4623b0)

the wns is -23.9

![Screenshot 2025-06-28 161501](https://github.com/user-attachments/assets/ed99d38c-4b71-4e76-8460-fd60699f850a)

![Screenshot 2025-06-28 162229](https://github.com/user-attachments/assets/c24d31cf-1222-4515-87bc-717185c2f513)

wns has reduced.

![Screenshot 2025-06-28 163033](https://github.com/user-attachments/assets/6be4e585-13cb-4125-87b2-2c03ddc7cf1c)

![Screenshot 2025-06-28 163101](https://github.com/user-attachments/assets/9f15c3c0-5f96-4a39-a143-d8e3ed1fcb46)

![Screenshot 2025-06-28 163227](https://github.com/user-attachments/assets/b9e3d730-1ab9-485e-bbee-a69df8806ace)

![Screenshot 2025-06-28 163259](https://github.com/user-attachments/assets/860fa128-f09d-4345-8fd6-6b0911422f14)

This is how we reduce slack.

---
## Clock tree synthesis TritonCTS and signal integrity
---
### Clock tree routing and buffering using H-Tree algorithm
---

### Clock Tree Synthesis:

Connect **clk1** to **FF1 and FF2 of stage 1**, **FF1 of stage 3**, and **FF2 of stage 4** using a **physical wire**.

![Screenshot 2025-06-28 164125](https://github.com/user-attachments/assets/1ce533a6-2c39-4cbe-b7c3-7f95776ecf6b)

Now let’s understand the issue here. Suppose there is some **physical distance** between **clk and FF1/FF2**, which leads to **t2 > t1**.
The **Skew = t2 - t1**, and ideally, the **skew should be 0 ps**.

![Screenshot 2025-06-28 164232](https://github.com/user-attachments/assets/da62db95-5521-49e3-8aff-12ac7f89f97a)

Previously, we built a **bad clock tree**, and now we will try to improve it in a **smarter way**. Here, the **clock (clk)** will enter from a **midpoint**, allowing it to reach all flip-flops at **approximately the same time**. Similarly, we will connect **clk2** to the flip-flops using the **midpoint approach**.

![Screenshot 2025-06-28 164344](https://github.com/user-attachments/assets/b9ddd968-4a04-4232-b669-b32ffcbf4d0c)

Now let's look at **Clock Tree Synthesis (Buffering)**. Suppose we have a **clock route** that needs to reach specific locations and **clock endpoints**. Along this path, there are multiple **capacitances and resistances** present.

![image](https://github.com/user-attachments/assets/4a7b7a05-89da-40f8-a963-70a6abeacfa3)

Due to the **wire length** and the presence of **RC networks**, the waveform at the output does not match the input. To resolve this issue, we use **repeaters**. The key difference between repeaters used for the **clock** and those used for the **data path** is that **clock repeaters maintain equal rise and fall times**.

The first step is to **remove the existing clock route**, place **two repeaters**, and allow the clock signal to pass through them. In this setup, the waveform generated at the input will properly propagate to the output. We can add **as many repeaters as needed** to maintain the **continuous flow of the clock signal** until the output.

![image](https://github.com/user-attachments/assets/46d040ff-4935-4ce5-b19c-9eb7546e6535)

---
### Crosstalk and clock net shielding
---
### Clock Net Shielding:

Until now, we have constructed the clock tree in a way that the **skew between the launch flop and capture flop is zero**, where **skew refers to the latency difference between the clock ports of the flop pins**.

**Clock net shielding** is applied to critical clock nets in the design. It involves **shielding the clock net**, meaning we **protect the clock signal from interference from the outside world**. This shielding acts like a **house for the clock**, ensuring signal integrity and reducing noise and coupling effects.

![Screenshot 2025-06-28 164851](https://github.com/user-attachments/assets/b9b930fb-1c27-4832-b59b-54c2eb2c8a3d)

If the **clock net is not protected**, we can face two major issues: **Glitch** and **Delta Delay**.

Let’s consider one clock net. Whenever there is a **switching activity** on the **aggressor net**, the **coupling capacitance** between adjacent wires can cause interference. If this capacitance is significant, **any switching activity on the aggressor will directly affect the nearby clock net**, leading to signal integrity problems like glitches or unexpected delays.

![Screenshot 2025-06-28 164951](https://github.com/user-attachments/assets/622e02d7-f391-46d4-b900-bc3ea6c3b8d0)

**Shielding** is a technique used to **protect the net from problems like glitch and delta delay**. In shielding, an **extra wire is placed between two signal wires** where **coupling capacitance** is generated. This extra wire is either **connected to ground (GND) or VDD** to absorb interference.

When switching from **logic '1' to logic '0'**, the presence of coupling causes a **bump**, resulting in **delta delay**. Due to this, the **skew is no longer zero**. The impact of **crosstalk-induced delta delay** is that it causes the clock skew to become **non-zero**, affecting timing integrity.

![Screenshot 2025-06-28 165105](https://github.com/user-attachments/assets/6e432faa-50d2-4afe-9bde-d2048a236c4b)

By shielding we are breaking the coupling capacitance between the aggraser and victim. Shields don't switch.

---
### Lab steps to run CTS using Triton
---

We now need to replace the old netlist with the newly generated netlist obtained after slack reduction, and then proceed with floorplanning, placement, and CTS.

![Screenshot 2025-06-28 220738](https://github.com/user-attachments/assets/30532d5c-2032-4b61-9167-1b8d0dabebdd)

The image shown above represents the netlist before applying any modifications.

We need to create a copy of this old netlist and then add the newly generated netlist, which will be used in the OpenLane flow for further processes.

Follow these commands to make the copy:

1. Navigate to the directory:

```bash
cd Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/02-04_05-27/results/synthesis/
```

2. List the contents of the directory:

```bash
ls -ltr
```

3. Copy the netlist with a new name:

```bash
cp picorv32a.synthesis.v picorv32a.synthesis_old.v
```

4. Verify the copied file by listing the contents again:

```bash
ls -ltr
```
Now we will do synthesis again then floorplan , placement and cts in the openlane directory itself by the following commands,

```tcl
prep -design picorv32a -tag 02-04_05-27 -overwrite

set lefs [glob $::env(DESIGN_DIR)/src/*.lef]
add_lefs -src $lefs

set ::env(SYNTH_STRATEGY) "DELAY 3"
set ::env(SYNTH_SIZING) 1

run_synthesis
init_floorplan
place_io
tap_decap_or
run_placement

# If any error occurs during CTS, use the following command
unset ::env(LIB_CTS)

run_cts
```

This flow initializes the design with the specified tag, adds necessary LEF files, applies synthesis with a delay-driven strategy, and continues through floorplanning, IO placement, tap/decap insertion, placement, and clock tree synthesis (CTS). If CTS errors out, the `unset ::env(LIB_CTS)` command can be used to resolve the issue before rerunning CTS.

![Screenshot 2025-06-28 221554](https://github.com/user-attachments/assets/377fe24a-bd01-4236-bd72-136d8efff4a0)

![Screenshot 2025-06-28 221608](https://github.com/user-attachments/assets/2ea17d3f-fd51-490a-9fa8-d91732172f02)

![Screenshot 2025-06-28 221641](https://github.com/user-attachments/assets/be961c8c-a8fa-445f-9e53-0334c44697c1)

![Screenshot 2025-06-28 221753](https://github.com/user-attachments/assets/fa1a4dbe-b59d-483e-ac47-0cb36f51751d)

![Screenshot 2025-06-28 221838](https://github.com/user-attachments/assets/e156c26c-bc70-407b-966f-02c53f2cfd22)

![Screenshot 2025-06-28 222009](https://github.com/user-attachments/assets/bbf4705d-1d74-4441-8eae-8c25a59b6a4d)

![Screenshot 2025-06-29 094409](https://github.com/user-attachments/assets/043e9510-8df3-46ef-9a73-8536afca9bde)

After run_cts we get a new netlist (.v) in the location shown in below image.

![Screenshot 2025-06-29 094628](https://github.com/user-attachments/assets/6deef137-eb6f-4e93-ae16-b41d9aa12504)

### Why Do We Get a New Netlist After `run_cts`?

When you run Clock Tree Synthesis (CTS) using `run_cts` in OpenLane (or any digital design flow), a new netlist is generated because the clock tree is inserted into the design.

### Reason for New Netlist:

* The initial netlist after synthesis only contains:

  * Combinational logic
  * Sequential elements (flip-flops, latches)
  * Basic clock definitions without clock tree buffers or proper clock distribution

* The clock tree synthesis (CTS) step:

  * Adds clock buffers or inverters.
  * Builds a balanced clock distribution network.
  * Reduces clock skew and ensures the clock reaches all sequential elements reliably within timing constraints.

### Modifications in the New Netlist:

* Insertion of:

  * Clock buffers such as CLKBUF, INV, BUFX
  * Clock tree routing connections
* Updates to:

  * Wire connections (nets)
  * Instance list (new cells added for the clock tree)

### File Naming:

* The netlist after CTS is typically named like:

  * `picorv32a.cts.v`
    This represents the design with the clock tree inserted.

### Summary:

* Synthesis netlist: Contains functional logic without a clock tree.
* CTS netlist: Contains functional logic along with a clock distribution network (clock buffers and routing).

This CTS-updated netlist is then used for further steps like routing and signoff checks.

---
### Lab steps to verify CTS runs
---
and
---
### Lab steps to analyze timing with real clocks using OpenSTA
---
Continuing after run_cts

### Commands to Run OPENROAD and Create the Database

```bash
# Command to start OpenROAD tool
openroad
```

### Load Design Files into OpenROAD

```tcl
# Read LEF file (contains technology and physical information)
read_lef /openLANE_flow/designs/picorv32a/runs/29-06_03-58/tmp/merged.lef

# Read DEF file (contains placement and routing information)
read_def /openLANE_flow/designs/picorv32a/runs/29-06_03-58/results/cts/picorv32a.cts.def
```

### Create and Load an OpenROAD Database

```tcl
# Create an OpenROAD database from the loaded LEF and DEF
write_db pico_cts.db

# Load the created database
read_db pico_cts.db
```

### Load Netlist, Library, and Constraints

```tcl
# Read netlist generated after CTS
read_verilog /openLANE_flow/designs/picorv32a/runs/29-06_03-58/results/synthesis/picorv32a.synthesis_cts.v

# Read the timing library for the design
read_liberty $::env(LIB_SYNTH_COMPLETE)

# Link the design with the library
link_design picorv32a

# Read the custom SDC file containing constraints
read_sdc /openLANE_flow/designs/picorv32a/src/my_base.sdc
```

### Setup Clocks and Generate Timing Report

```tcl
# Set all clocks as propagated clocks
set_propagated_clock [all_clocks]

# Check syntax and options for the report_checks command
help report_checks

# Generate a detailed timing report
report_checks -path_delay min_max -fields {slew trans net cap input_pins} -format full_clock_expanded -digits 4
```

### Exit OpenROAD

```tcl
exit
```
![Screenshot 2025-06-29 104204](https://github.com/user-attachments/assets/9cad1e1e-1585-4e93-84c5-7dd7fe69c8e4)

![Screenshot 2025-06-29 105214](https://github.com/user-attachments/assets/e187354b-61b3-4475-aabb-0009a912c7ed)

![Screenshot 2025-06-29 110104](https://github.com/user-attachments/assets/abe034cd-3594-4cdb-910b-b3b51d3706bc)

![Screenshot 2025-06-29 110204](https://github.com/user-attachments/assets/2c4d961c-ca20-40a1-b81f-9cecd7b5c38d)

![Screenshot 2025-06-29 110401](https://github.com/user-attachments/assets/c8874a3f-610b-4224-a8d4-f2cd694fa415)

![Screenshot 2025-06-29 110421](https://github.com/user-attachments/assets/27825137-bdb5-478e-94c4-3d347999e25b)

---
## Timing analysis with real clock using openSTA
---
### Setup timing analysis using real clocks
---

The clock tree in a real circuit appears slightly different from an ideal clock because it includes components like buffers and wires. The clock signal reaches the launch and capture flip-flops through a series of buffers. As a result, the clock signal does not arrive at the flip-flop exactly at time t = 0 due to the delay introduced by these buffers.

Therefore, the setup timing equation is modified. Initially, the ideal condition was:

```
θ < T
```

With the real clock tree, it becomes:

```
(θ + 1 + 2) < (T + 1 + 3 + 4)
```

Here:

* `θ` represents the data path delay.
* `1` and `2` are the clock delays to the launch flip-flop.
* `3` and `4` are the clock delays to the capture flip-flop.
* `T` is the clock period.

This equation accounts for the additional clock delays introduced by the clock tree elements like buffers and wires.

![Screenshot 2025-06-29 112233](https://github.com/user-attachments/assets/d67dbdcf-6050-4bf6-aac5-b3c27c317f8a)

Let’s define **“1 + 2” as ∆1**, and **“1 + 3 + 4” as ∆2**, where the skew is given by **(∆1 − ∆2)**.

![image](https://github.com/user-attachments/assets/0969e4d6-3cd6-4874-b7ec-d25897c50d86)

Here, we also need to consider **propagation skew (S)** and **uncertainty delay (US)**. So, the final equation becomes:

```
(θ + ∆1) < (T + ∆2 - S - US)
```

We can also interpret this as:

* **(θ + ∆1)** → **Data arrival time**
* **(T + ∆2 - S - US)** → **Data required time**

If **(Data required time - Data arrival time)** is **positive**, the timing is met. If it is **negative**, it is referred to as **slack**.

---

### Hold Timing Analysis:

Hold timing analysis is slightly different from setup timing analysis. Here, the first clock pulse is sent to both the **launch flip-flop** and the **capture flip-flop** simultaneously.

The hold condition states that:

```
Hold time (H) < Combinational delay (θ)
```

Or simply:

```
θ > H
```

This ensures that data does not get captured too early at the capture flip-flop.

![Screenshot 2025-06-29 112625](https://github.com/user-attachments/assets/2ce393a7-5e98-449f-8570-dcf55223519c)

Hence, a finite time **‘H’** is required for **‘Qm’** to reach **‘Q’**, which means the **internal delay of MUX2 is equal to the hold time**.

Now, when we consider the real clock network, the equation changes to:

```
(θ + ∆1) > (H + ∆2)
```
![Screenshot 2025-06-29 112727](https://github.com/user-attachments/assets/c250bfcf-1eee-412f-9d96-068f863325b2)

---
### Hold timing analysis using real clocks
---
The combinational delay should be greater than the hold time of the capture flip-flop. When the clock reaches the launch flip-flop, it experiences approximately a 2-buffer delay (∆1), and when it reaches the capture flip-flop, it goes through approximately a 3-buffer delay (∆2). The uncertainty remains the same for both flip-flops since the clock is applied to both from the same clock edge. Now, let’s incorporate the uncertainty value into the equation.

![image](https://github.com/user-attachments/assets/1cae9dfb-915b-4d5b-ae1c-4952cb0a2123)

Slack is calculated as Data arrival time minus Data required time. Slack should either be positive or zero. If slack becomes negative, it is referred to as a violation.

![Screenshot 2025-06-29 113001](https://github.com/user-attachments/assets/af5dec81-bd9c-43fd-aeb9-e071e9865378)

Let's identify the timing paths from design, with single clock

![Screenshot 2025-06-29 113021](https://github.com/user-attachments/assets/8e73295b-261e-4956-9fa6-b6b4a4c7f9d3)

![Screenshot 2025-06-29 113034](https://github.com/user-attachments/assets/615e0143-ca5b-4cf6-b0fd-b1bbee637576)

![Screenshot 2025-06-29 113042](https://github.com/user-attachments/assets/f05e9953-8d8e-4e9a-9328-e5cfc9a57957)

---
### Lab steps to execute OpenSTA with right timing libraries and CTS assignment
---
and 
---
### Lab steps to observe impact of bigger CTS buffers on setup and hold timing
---

Explore post-CTS OpenROAD timing analysis by removing the **`sky130_fd_sc_hd__clkbuf_1`** cell from the clock buffer list variable **`CTS_CLK_BUFFER_LIST`**. The following commands are used in the OpenLANE flow to perform OpenROAD timing analysis after modifying **`CTS_CLK_BUFFER_LIST`**:

```tcl
# Check the current value of CTS_CLK_BUFFER_LIST
echo $::env(CTS_CLK_BUFFER_LIST)

# Remove 'sky130_fd_sc_hd__clkbuf_1' from the list
set ::env(CTS_CLK_BUFFER_LIST) [lreplace $::env(CTS_CLK_BUFFER_LIST) 0 0]

# Verify the updated CTS_CLK_BUFFER_LIST
echo $::env(CTS_CLK_BUFFER_LIST)

# Check the current value of CURRENT_DEF
echo $::env(CURRENT_DEF)

# Set CURRENT_DEF to the placement DEF
set ::env(CURRENT_DEF) /openLANE_flow/designs/picorv32a/runs/24-03_10-03/results/placement/picorv32a.placement.def

# Run CTS after modifying the buffer list
run_cts

# Verify CTS_CLK_BUFFER_LIST again
echo $::env(CTS_CLK_BUFFER_LIST)

# Launch OpenROAD tool
openroad

# Read LEF file
read_lef /openLANE_flow/designs/picorv32a/runs/24-03_10-03/tmp/merged.lef

# Read DEF file
read_def /openLANE_flow/designs/picorv32a/runs/24-03_10-03/results/cts/picorv32a.cts.def

# Create OpenROAD database
write_db pico_cts1.db

# Load the created database
read_db pico_cts.db

# Read the post-CTS netlist
read_verilog /openLANE_flow/designs/picorv32a/runs/24-03_10-03/results/synthesis/picorv32a.synthesis_cts.v

# Read the liberty file
read_liberty $::env(LIB_SYNTH_COMPLETE)

# Link design and library
link_design picorv32a

# Load the custom SDC file
read_sdc /openLANE_flow/designs/picorv32a/src/my_base.sdc

# Set all clocks as propagated
set_propagated_clock [all_clocks]

# Generate the timing report
report_checks -path_delay min_max -fields {slew trans net cap input_pins} -format full_clock_expanded -digits 4

# Report clock skew for hold
report_clock_skew -hold

# Report clock skew for setup
report_clock_skew -setup

# Exit OpenROAD
exit

# Verify CTS_CLK_BUFFER_LIST once more
echo $::env(CTS_CLK_BUFFER_LIST)

# Reinsert 'sky130_fd_sc_hd__clkbuf_1' to the beginning of the list
set ::env(CTS_CLK_BUFFER_LIST) [linsert $::env(CTS_CLK_BUFFER_LIST) 0 sky130_fd_sc_hd__clkbuf_1]

# Check CTS_CLK_BUFFER_LIST after reinserting
echo $::env(CTS_CLK_BUFFER_LIST)
```
![Screenshot 2025-06-29 115256](https://github.com/user-attachments/assets/a7cb4bb8-220d-431d-bc89-e7afcb3cbb74)

![Screenshot 2025-06-29 115643](https://github.com/user-attachments/assets/88db73a4-a54f-4cad-a2ca-ff741c47c280)

![Screenshot 2025-06-29 120535](https://github.com/user-attachments/assets/d24be58f-84bb-4e42-bad6-74ff632e7786)

![Screenshot 2025-06-29 120743](https://github.com/user-attachments/assets/517f7d16-66fd-45b0-9ef9-fdba09a07f80)

![Screenshot 2025-06-29 120815](https://github.com/user-attachments/assets/ab245693-79a8-476a-ba48-fce3efee3efd)

![Screenshot 2025-06-29 120938](https://github.com/user-attachments/assets/1a8c0366-23aa-47cb-9e16-0157fc466a59)

![Screenshot 2025-06-29 121217](https://github.com/user-attachments/assets/fb4d45f0-0d3b-4f7b-83a2-56f9697394f5)

---
# Day 5 -Final step for RTL2GDS using tritinRoute and openSTA
---
## Routing and design rule check (DRC)
---
### Introduction to Maze Routing – Lee’s algorithm
---

The next and final stage in the physical design process is **Routing and DRC**.

### **Routing:**

Routing is the process of determining the best and shortest possible connection between two endpoints, where one is the **source** and the other is the **target**, with minimal twists and turns in the path.

### **Maze Routing (Lee’s Algorithm):**

This method ensures that the routing paths do not form zig-zag patterns. Most of the routes follow **L-shaped or Z-shaped paths**. The algorithm starts by creating a set of **grids**, known as the **routing grid**, which is used at the backend for routing. These grids have defined dimensions and form the routing space.

In this grid, there are two main points: the **source** and the **target**. The algorithm’s goal is to find the best possible route between these two points using the routing grid.

The first step of the algorithm involves **labeling all the adjacent grids** around the source. Only the **horizontal and vertical adjacent grids** are labeled, while the **diagonal grids are ignored**, as illustrated in the image below.

![Screenshot 2025-06-29 124905](https://github.com/user-attachments/assets/fa421d8c-23e1-4703-911d-5da03e12130a)

---
### **Lee’s Algorithm Conclusion:**
----

The grids are labeled with successive integers step by step until the target point is reached. In the given example, the target is reached when the label reaches the integer **9**.

![Screenshot 2025-06-29 125038](https://github.com/user-attachments/assets/c2a409e0-c780-4c26-b39a-b44aacb65b6e)

Now, there are multiple possible paths to reach the target from the source, but the goal is to select the best and shortest possible path. It is preferable to avoid zig-zag paths and instead choose routing paths that are primarily in ‘L’ shape for better efficiency.

![Screenshot 2025-06-29 125147](https://github.com/user-attachments/assets/1c3d3b52-3730-4d93-b258-5302b9141edf)

Now, let’s consider another example for routing and follow the exact same steps as demonstrated in the previous example.

![Screenshot 2025-06-29 125252](https://github.com/user-attachments/assets/f32a4f42-630c-438e-93c7-bb1760c84dd7)

![Screenshot 2025-06-29 125619](https://github.com/user-attachments/assets/79e7436d-634a-4137-9a67-abd7997a6c86)

---
### Design Rule Check
---
To proceed with DRC, we need to follow certain steps known as DRC cleaning.
Let’s consider the example of the circuit discussed above. Suppose there are two parallel wires, the design rule specifies that there must be a minimum required distance maintained between these two wires.

![Screenshot 2025-06-29 125935](https://github.com/user-attachments/assets/8b815424-256b-4287-96a0-8f4017d4f668)

Rule 1 – Wire Width:
The width of the wire must meet a minimum requirement, which is determined based on the optical wavelength of the lithography technique being used.

![Screenshot 2025-06-29 130023](https://github.com/user-attachments/assets/aa3954c4-8d12-4631-9d07-2c27b3449d9e)

Rule 2 – Wire Pitch:
The minimum pitch between two wires must be maintained as specified, as illustrated in the figure below.

![Screenshot 2025-06-29 130034](https://github.com/user-attachments/assets/29594dba-a2ec-4e46-a657-bab9efc92f9c)

Rule 3 – Wire Spacing:
The spacing between two wires should follow the required minimum distance, as demonstrated in the image below.

![image](https://github.com/user-attachments/assets/654e68be-c884-4502-9bdb-dbac9c147b6a)

Let’s consider another aspect of the design rule check using the same example.

![Screenshot 2025-06-29 130901](https://github.com/user-attachments/assets/a6b89089-b4c3-4c06-97db-1d8427461e02)

The solution to this signal short problem is to move one of the wires to a different metal layer. Typically, the upper metal layers are wider compared to the lower ones.

![Screenshot 2025-06-29 131002](https://github.com/user-attachments/assets/0647f67e-9ab9-435f-9067-4da21fcbfca3)

After this solution, we add two new DRC rules should be check.

Rule 1) Via Width:- via width should be some minimum value.

![Screenshot 2025-06-29 131109](https://github.com/user-attachments/assets/cbdda84d-d40d-4c59-b69c-3b26b9772323)

Rule 2 – Via Spacing:
The spacing between vias should adhere to the specified minimum value.

![image](https://github.com/user-attachments/assets/483eeed5-19af-44e0-89cf-b3a38d559d86)

After routing and DRC, the next step is parasitic extraction. The resistance and capacitance present on every wire are extracted and used for the subsequent steps in the flow.

![Screenshot 2025-06-29 131311](https://github.com/user-attachments/assets/1e5006ab-1184-4df6-b85e-83ffc1749476)

---
## Power Distribution Network and routing
---
### Lab steps to build power distribution network
---

The commands used in the previous terminal session are as follows:

```tcl
docker

./flow.tcl -interactive

package require openlane 0.9

prep -design picorv32a -tag 29-06_03-58 //we are not using -overwrite so that we can continue from our last run

echo $::env(CURRENT_DEF) //to see until which step we performed in the previous run
```

Up to this point, **CTS has been completed**, and now we are moving on to the **routing stage**. However, before starting routing, it is necessary to generate the **PDN (Power Distribution Network)** using the following command:

```tcl
gen_pdn
```

---

The command:

```tcl
echo $::env(CURRENT_DEF)
```

**Meaning:**
This command is used to **display the current DEF file path** that OpenLANE is using at that stage of the flow.

**Significance:**

* **`CURRENT_DEF`** is an environment variable that holds the path to the **latest DEF (Design Exchange Format) file** generated during the design flow.
* The DEF file contains the physical layout information of the design at the current stage, whether it is after placement, CTS, or routing.

**Purpose of Running This Command:**

* To check and verify which DEF file OpenLANE is currently pointing to.
* It confirms whether the flow is using the **placement DEF, CTS DEF, or routed DEF**, based on the progress of the design flow.
* It is useful for verification, debugging, or when performing manual steps like CTS, routing, or timing analysis.

**In simple terms:**
It tells you *“Which layout file am I currently working with?”*

![Screenshot 2025-06-30 093545](https://github.com/user-attachments/assets/57615753-b989-4594-8f86-46f3ba2ac31f)

![Screenshot 2025-06-30 093714](https://github.com/user-attachments/assets/1b1d4e29-ad34-4448-ab63-86796391847b)

![Screenshot 2025-06-30 093911](https://github.com/user-attachments/assets/63de5e47-bc76-43e3-b82e-4d985308c09c)

It appears that the net **VGND** represents the **total number of nodes on the grid matrix**, indicating that it has been successfully created.
The chip receives power through the **VDD and GND pads**, which then flows through the **power tracks** and ultimately reaches the cells to supply them with power.

---
### Lab steps from power straps to std cell power
---

![Screenshot 2025-06-30 094547](https://github.com/user-attachments/assets/b143c84a-02a6-4192-954c-cc755e7a6e67)

### 1. **Padframe (Outer Yellow Blocks):**

* These are **I/O pads and corner pads** placed around the boundary of the chip.
* They serve as connection points between the chip and the external world (packaging, PCB, etc.).

### 2. **Power Pad Connections:**

* **VDD (Red) and GND (Blue)** pads are placed at regular intervals on the padframe.
* Power enters the chip through these pads.

### 3. **Block Power Ring:**

* Thick horizontal and vertical red (VDD) and blue (GND) lines form a **power ring** around the core area.
* This ring helps distribute power uniformly into the core.

### 4. **Power Stripes:**

* Vertical and horizontal power lines (stripes) extend from the power ring into the core area.
* They provide power deeper into the chip, reaching the **standard cells**.

### 5. **Standard Cell Power Connections:**

* Inside the core, **standard cell rows** are connected to the power grid through horizontal and vertical lines.
* This ensures that each **standard cell** receives a stable VDD and GND supply.

### 6. **Standard Cell Rows (Green Region):**

* This is where the majority of the logic gates are placed.
* The cells are aligned in rows for efficient routing and power delivery.

### 7. **Macro Cell (RAM - Pink Block):**

* A large block typically like SRAM or any hard macro.
* It has its own **block power ring** for dedicated and stable power.

### 8. **Block Halo:**

* A reserved area around the macro cell to prevent routing congestion and to separate standard cells from the macro.

### 9. **I/O to Core Spacing:**

* This spacing is provided between the padframe and the core to facilitate routing tracks for signals and power.

---

### **Power Flow Summary:**

* Power flows from **VDD and GND pads → Power Rings → Power Stripes → Standard Cells and Macros**.

This structure ensures reliable power delivery while minimizing voltage drops and IR drop issues across the chip.

the same details are shown in our gen_pdn output

![Screenshot 2025-06-30 095630](https://github.com/user-attachments/assets/075fac90-96ed-4b15-896c-cdbbe47ce661)

### **Commands to Load PDN DEF in Magic (from another terminal):**

```bash
# Navigate to the directory where the PDN DEF file is located
cd Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/30-06_07-09/tmp/floorplan/

# Load the PDN DEF file into Magic
magic -T /home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech \
lef read ../../tmp/merged.lef \
def read 17-pdn.def &
```
![Screenshot 2025-06-30 161550](https://github.com/user-attachments/assets/4dfba53d-2ebb-499b-950e-6cfc38168a25)

Image of the pdn def

![Screenshot 2025-06-30 161735](https://github.com/user-attachments/assets/57cb827c-9e25-4c0b-a41f-a17712d4a0c8)

![Screenshot 2025-06-30 162042](https://github.com/user-attachments/assets/8bb43c26-fa09-44ef-9951-3bf719b6ed4e)

![Screenshot 2025-06-30 161953](https://github.com/user-attachments/assets/3590a698-8e55-4c56-9a00-c2f3fe81c2a5)

![Screenshot 2025-06-30 162015](https://github.com/user-attachments/assets/57e0f62a-8a66-4f0e-807d-19eda2a063b9)

### **2. Perform Detailed Routing Using TritonRoute and Explore the Routed Layout**

### **Commands to Perform Routing:**

```tcl
# Check the current DEF file in use
echo $::env(CURRENT_DEF)

# Check the current routing strategy being applied
echo $::env(ROUTING_STRATEGY)

# Run detailed routing using TritonRoute
run_routing
```
![Screenshot 2025-06-30 162447](https://github.com/user-attachments/assets/bb5c0d5e-2f2f-4247-ace8-568bbc76369d)

Screenshots of relevant results generated from run_routing

![Screenshot 2025-06-30 163309](https://github.com/user-attachments/assets/df2d8124-e14b-47df-ac66-3a16d8de01b9)

![Screenshot 2025-06-30 183748](https://github.com/user-attachments/assets/482d7ee3-0c2e-4ab7-ba97-7f86c1f34669)

![Screenshot 2025-06-30 183804](https://github.com/user-attachments/assets/11806d17-8bc2-4782-9d3a-e8d5e6ec7c13)

![Screenshot 2025-06-30 183828](https://github.com/user-attachments/assets/d0a28e89-1e07-421a-bd14-2c689d4ca3f9)

### **Commands to Load Routed DEF in Magic (from another terminal):**

```bash
# Navigate to the directory where the routed DEF file is located
cd Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/30-06_07-09/results/routing/

# Load the routed DEF file into Magic
magic -T /home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech \
lef read ../../tmp/merged.lef \
def read picorv32a.def &
```

![Screenshot 2025-07-01 100047](https://github.com/user-attachments/assets/5c3d4eec-e016-4906-a173-eaaaad775979)

![Screenshot 2025-07-01 100107](https://github.com/user-attachments/assets/da82d485-4592-4b7e-ae25-80e66f9de3a0)

![Screenshot 2025-07-01 100209](https://github.com/user-attachments/assets/01525f19-20cd-4033-b438-73e271bb042f)

![Screenshot 2025-07-01 100246](https://github.com/user-attachments/assets/48066240-3b65-4b74-be67-80c73c87d239)

![Screenshot 2025-07-01 100330](https://github.com/user-attachments/assets/981a7e96-def7-4ef9-a8af-e58679c50b8a)

### **Post-Route Parasitic Extraction Using SPEF Extractor**

### **Commands for SPEF Extraction Using External Tool:**

```bash
# Navigate to the SPEF extractor directory
cd Desktop/work/tools/SPEF_EXTRACTOR

# Run the SPEF extraction command
python3 main.py /home/vsduser/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/30-06_07-09/tmp/merged.lef /home/vsduser/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/30-06_07-09/results/routing/picorv32a.def
```

### **Post-Route OpenSTA Timing Analysis with Extracted Parasitics (SPEF) Using OpenROAD**

### **Commands to Run in OpenLANE Flow:**

```tcl
# Launch OpenROAD tool
openroad

# Read LEF file
read_lef /openLANE_flow/designs/picorv32a/runs/30-06_07-09/tmp/merged.lef

# Read routed DEF file
read_def /openLANE_flow/designs/picorv32a/runs/30-06_07-09/results/routing/picorv32a.def

# Create OpenROAD database
write_db pico_route.db

# Load the created database
read_db pico_route.db

# Read post-CTS netlist
read_verilog /openLANE_flow/designs/picorv32a/runs/30-06_07-09/results/synthesis/picorv32a.synthesis_preroute.v

# Read liberty file for the design
read_liberty $::env(LIB_SYNTH_COMPLETE)

# Link the design and library
link_design picorv32a

# Read the custom SDC file
read_sdc /openLANE_flow/designs/picorv32a/src/my_base.sdc

# Set all clocks as propagated clocks
set_propagated_clock [all_clocks]

# Read the extracted SPEF file
read_spef /openLANE_flow/designs/picorv32a/runs/30-06_07-09/results/routing/picorv32a.spef

# Generate timing report
report_checks -path_delay min_max -fields {slew trans net cap input_pins} -format full_clock_expanded -digits 4

# Exit OpenROAD
exit
```

![Screenshot 2025-07-01 101721](https://github.com/user-attachments/assets/9366d2c2-a02e-44e0-84e0-9cf57c6d78be)

![Screenshot 2025-07-01 102145](https://github.com/user-attachments/assets/3aa3eb70-93fd-4e05-b438-5a277b06836e)

![Screenshot 2025-07-01 102407](https://github.com/user-attachments/assets/f6a7d935-fb24-402a-ae13-4504c6c1bcc2)

![Screenshot 2025-07-01 102550](https://github.com/user-attachments/assets/247caafb-96d8-4b0e-9289-01e181b39b52)

![Screenshot 2025-07-01 102618](https://github.com/user-attachments/assets/ca000fb6-6b52-473a-bb3b-3ad8ab609dea)

---

# References

* [Google SkyWater PDK](https://github.com/google/skywater-pdk)
* [VSD Standard Cell Design by Nickson Jose](https://github.com/nickson-jose/vsdstdcelldesign)
* [Ngspice – Open Source Circuit Simulator](https://sourceforge.net/projects/ngspice/)
* [VSD Workshop GitHub Material](https://github.com/)
* [Introduction to Industrial Physical Design Flow (PDF)](https://www.vlsisystemdesign.com/wp-content/uploads/2017/07/Introduction-to-Industrial-Physical-Design-Flow.pdf)
* [NPTEL – Physical Design of Digital VLSI Systems by Prof. Indranil Sengupta](https://nptel.ac.in/courses/117105150)

---

# Acknowledgement

I sincerely express my gratitude to Mr. Kunal Ghosh, Co-founder of VLSI System Design (VSD) Corp. Pvt. Ltd., and Mr. Nickson Jose for their remarkable guidance and for conducting the **DIGITAL-VLSI-SOC-DESIGN-AND-PLANNING** workshop. Their clear instruction, deep expertise, and well-structured sessions greatly enhanced my understanding of physical chip design, OpenLANE workflows, and practical design methodologies. The workshop was thoughtfully organized and delivered, providing me with valuable insights into the complete physical design process. I am truly thankful to both Mr. Kunal Ghosh and Mr. Nickson Jose for their dedication to knowledge sharing and for offering such an enriching learning experience.

---

