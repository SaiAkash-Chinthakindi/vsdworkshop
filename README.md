# VSD RTL Design Workshop (Day 1 – Day 4)

This repository contains my work from the **VSD RTL Design and Synthesis Workshop**.  
Each folder (`Day1` to `Day4`) has the Verilog codes, testbenches and scripts I used while learning RTL design, simulation and synthesis.

---

## Repository Structure

- `Day1/` – Basic Linux, simulation setup and first RTL runs  
- `Day2/` – RTL design, synthesis with Yosys and netlist generation  
- `Day3/` – Gate-level simulation (GLS) and synthesis–simulation debug  
- `Day4/` – Sequential logic, optimizations and timing-related checks  

---

## Day 1 – Setup, Basics and First Simulations

- Got familiar with **Linux commands**, directory navigation and file handling.  
- Wrote simple **Verilog RTL** modules and basic **testbenches**.  
- Ran simulations using open-source tools (like `iverilog` and `gtkwave`) to view waveforms.  
- Understood the difference between **RTL code**, **testbench**, and **simulation output**.

---

## Day 2 – RTL to Gate-Level (Synthesis with Yosys)

- Introduced to **Yosys** for RTL **synthesis**.  
- Used `synth -top <module_name>` to tell Yosys which module is the top design.  
- Generated a **gate-level netlist** from the RTL.  
- Observed how RTL operators are mapped into **standard cells** from the library.

---

## Day 3 – Gate-Level Simulation (GLS) and Mismatch Analysis

- Learned what **GLS (Gate Level Simulation)** is:
  - Running the **same testbench** but using the **netlist** as the design under test (DUT).
  - Netlist is logically same as RTL, and has the same inputs/outputs.
- Ran GLS to check that the **synthesized netlist** behaves like the RTL.  
- Studied possible **synthesis–simulation mismatches**, such as:
  - Missing sensitivity list in `always` blocks  
  - Uninitialized signals or different tool assumptions  

---

## Day 4 – Sequential Logic and Optimizations

- Focused on **sequential logic** (flip-flops, registers, state elements).  
- Looked at **sequential logic optimizations**:
  - Removing unnecessary registers  
  - Cleaning up state logic  
  - Making timing and area better without changing functionality.  
- Reviewed how tools perform **logic optimization** on both combinational and sequential parts of the design.

---

## Tools Used

- **Verilog** for RTL design and testbenches  
- **Icarus Verilog / iverilog** for simulation  
- **GTKWave** for waveform viewing  
- **Yosys** for synthesis and netlist generation  
- **Linux shell** for compilation, running scripts and file management  

---

## How to Use This Repo

1. Go into the required day folder, for example:
   ```bash
   cd Day1
