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
###  OpenLANE Directory structure in detai
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









