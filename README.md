# DIGITAL VLSI SOC DESIGN AND PLANNING
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

# Day 1 - Inception of open-source EDA, OpenLANE and sky130 PDK
## How to talk to computers
### Introduction to QFN-48 Package, chip, pads, core, die and IPs
Absolutely — here’s a more detailed version of your outline, while still keeping it clear and concise. This version can fit well in a presentation, document, or technical write-up.

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

Here's a clear and slightly expanded version of your explanation, with technical details filled in and arranged in logical order. This can serve as part of documentation, a presentation, or a tutorial step-by-step:

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
Here's the updated section of your explanation with the `FP_IO_MODE` command included along with a clear explanation of what it does:

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

The **transition time** (also called **slew**) is calculated using the difference between the high and low threshold points on a waveform.
For a **rising transition**:
$$
\text{Transition Time (Rise)} = \text{time(slew\_high\_rise\_thr)} - \text{time(slew\_low\_rise\_thr)}
$$
For a **falling transition**:
$$
\text{Transition Time (Fall)} = \text{time(slew\_high\_fall\_thr)} - \text{time(slew\_low\_fall\_thr)}
$$
These thresholds typically correspond to **20% and 80%** of VDD, but can vary depending on library settings.

