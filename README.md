# VSD RTL Design Workshop – Summary (Day 1 to Day 5)

This README provides a detailed summary of the work completed from **Day 1 to Day 5** in the VSD RTL Design and Synthesis Workshop.

---

## 📘 Day 1 – Introduction, Linux Commands & Basic Simulation

### **What I Learned**
- Basic Linux commands for navigation, file creation, editing, and running tools.  
- Difference between **RTL**, **testbench**, and **simulation output**.  
- How to compile and simulate Verilog code using **iverilog** and view waveforms using **GTKWave**.  
- Understood how a testbench drives a design and how signals behave over time.

### **Tasks Done**
- Wrote simple Verilog modules (basic combinational circuits).  
- Created corresponding testbenches to verify outputs.  
- Generated `.vcd` waveform files and analyzed them using GTKWave.

👉 This day built the foundation for RTL design and simulation tools.

---

## 📗 Day 2 – RTL Synthesis with Yosys

### **Key Concepts**
- What synthesis means: converting RTL code into a **gate-level representation** using standard-cell libraries.  
- Introduction to **Yosys commands** for analyzing, optimizing, and synthesizing RTL designs.  
- Importance of the `synth -top <module>` command for specifying the top module.

### **What I Did**
- Loaded RTL code into Yosys.  
- Ran synthesis and generated a **gate-level netlist**.  
- Observed mapping of RTL operators into cells like **AND, OR, XOR, DFF** from the library.  
- Understood the difference between **RTL simulation** and **synthesized hardware**.

👉 This day helped connect software-level Verilog with real hardware logic.

---

## 📙 Day 3 – Gate-Level Simulation (GLS) & Debugging Mismatches

### **Main Learning Points**
#### What is GLS?
- Gate Level Simulation (GLS) is running the same testbench but using the **synthesized netlist** instead of RTL.

#### Why GLS is Important
- To confirm synthesis didn’t change the logic.  
- To detect mismatches early.

### **Concepts Studied**
- The netlist is logically the same as RTL with matching inputs and outputs.  
- The same testbench can be reused for both RTL and netlist.  
- Common causes of **synthesis–simulation mismatches**:
  - Missing sensitivity list  
  - Uninitialized signals  
  - Blocking vs non-blocking issues  
  - Inferred latches  

### **Tasks Done**
- Compiled and simulated the **netlist** with the existing testbench.  
- Compared waveforms between RTL sim and GLS.  
- Identified mismatch causes and learned how to fix them in RTL code.

👉 This day focused on real synthesis behavior and debugging practical issues.

---

## 📕 Day 4 – Sequential Logic, Flip-Flops & Optimization Techniques

### **Learning Objectives**
- Difference between **combinational** and **sequential** logic.  
- How **flip-flops**, **registers**, and **clocked logic** behave in hardware.  
- Optimization techniques applied by synthesis tools to sequential logic.

### **Topics Covered**
- Removing unnecessary registers  
- Cleaning up state machines  
- Timing improvements  
- Area reduction without affecting functionality  

### **Hands-On Tasks**
- Worked with sequential circuits in Verilog.  
- Observed Yosys optimizations on real examples.  
- Understood how register placement influences design timing.

👉 This day strengthened understanding of sequential circuits and hardware optimization.

---

## 📒 Day 5 – Behavioral Modeling, Case/If Constructs & Latch Avoidance

### **What I Learned**
- How behavioral Verilog constructs like **if-else**, **case**, and **for loops** translate into hardware.  
- Difference between:
  - A **procedural for loop** (used inside always blocks)
  - A **generate-for loop** (used to create multiple hardware instances)
- How missing assignments in conditional statements lead to **inferred latches**.
- How synthesizers interpret priority logic (if-else ladders) vs parallel logic (case statements).

### **Key Concepts**
- **If / Else Chains**
  - Priority-based logic  
  - Must assign all outputs in every branch to avoid latch formation  

- **Case Statements**
  - More structured and parallel  
  - Missing a `default` clause → risk of inferring unintended latches  
  - Useful for state machines and decoders  

### **Tasks Done**
- Wrote examples of incomplete case and if statements to observe how latches appear in synthesis.  
- Corrected them by adding proper assignments and default branches.  


👉 This day focused on writing **clean, synthesizable Verilog** and avoiding hidden hardware pitfalls.

---

# 🛠 Tools Used

- **Icarus Verilog (iverilog)** – For compiling and simulating RTL  
- **GTKWave** – For viewing waveforms  
- **Yosys** – For synthesis and netlist generation  
- **Sky130 / Standard Cell Libraries** – For technology mapping  
- **Linux Shell** – For running commands and managing files  

---

