
# Introduction to verilog RTL Design and Synthesis

## Simulator 

It is a tool used for checking the Design, The RTL design is checked for adherence the specifications by checking the design.

**iverilog** is the tool used for this workshop.

It looks for the changes in the input signals, and upon changes to the input signals the outputs are evaluated.If there is no change in the input the simulator will not Evaluate the output.

## Design

It is the actual verilog code or the set of verilog codes which has intended functionality to meet the reuired specifications.

## Testbench

It is the Setup to apply stimulus to the design the check the design functionality.


## **iverilog** based Simulator Flow

![image alt](https://github.com/SaiAkash-Chinthakindi/vsdworkshop/blob/main/Day1/images/iverilog_gtkwave_2.png?raw=true)

The output of the simulator will be a vcd file(value change dump),and For viewing the vcd file we are going to use gtk wave(which is used for viewing the waveform output).
## iverilog and gtkwave

The steps to load the design in iverilog and viewing the Waveforms in gtkwave.

- Compile the design and testbench

``` bash
iverilog good_mux.v tb_good_mux.v
```
- Run the simulation
``` bash
./a.out
```
- view the Waveform
```bash
gtkwave tb_good_mux.vcd
```

![App Screenshot](https://via.placeholder.com/468x300?text=App+Screenshot+Here)

![App Screenshot](https://via.placeholder.com/468x300?text=App+Screenshot+Here)
## iverilog and gtkwave

The steps to load the design in iverilog and viewing the Waveforms in gtkwave.

- Compile the design and testbench

``` bash
iverilog good_mux.v tb_good_mux.v
```
- Run the simulation
``` bash
./a.out
```
- view the Waveform
```bash
gtkwave tb_good_mux.vcd
```

![App Screenshot](https://via.placeholder.com/468x300?text=App+Screenshot+Here)

![App Screenshot](https://via.placeholder.com/468x300?text=App+Screenshot+Here)
## iverilog and gtkwave

The steps to load the design in iverilog and viewing the Waveforms in gtkwave.

- Compile the design and testbench

``` bash
iverilog good_mux.v tb_good_mux.v
```
- Run the simulation
``` bash
./a.out
```
- view the Waveform
```bash
gtkwave tb_good_mux.vcd
```

![App Screenshot](https://via.placeholder.com/468x300?text=App+Screenshot+Here)

![App Screenshot](https://via.placeholder.com/468x300?text=App+Screenshot+Here)
## Introduction to yosys and Logic Synthesis

### Synthesizer

It is the tool used for converting the RTL Design to netlist.

**yosys** is the Synthesizer used in this course.

The Design is converted into gates and the connections are made between the gates. This is given out as a file called netlist.

### Verify the Synthesis

- The netlist that is generated after the synthesis and the testbench used to verify the RTL design are passed to iverilog Simulator.
- The vcd file will be genetated and to view the waveform we are going to use gtkwave.

**Note:** 
- The set of primary inputs and the primary outputs will remain same between the RTL design and the Synthesized netlist and the same testbench can be used.
- the Stimulus should be same as output observed during RTL Simulation.

### .lib file

It is the collection of logic modules includes basic logic gates like and,or,not etc..

-- It may contain different flavours of same gate.

- 2 input and gate

  -- slow

  -- medium

  --fast

- 3 input and gate

  -- slow

  -- medium

  -- fast


## Yosys and Sky130 PDks

### Lab on Yosys

The Lab is about how the RTL design is going to be Synthesised using Yosys

The commands are as follow:
- first we are going to invoke the yosys using command 
```bash 
yosys
```

- now we are going to read the library 
```bash
read_liberty -lib ../lib/sky120_fd_sc_hd__tt_025C_1v80.lib
```
- read the design 
```bash
read_verilog good_mux.v
```
- we have to synthesise the module
```bash
synth -top good_mux
```
- now we have to generate the netlist
```bash
abc -liberty ..lib/sky120_fd_sc_hd__tt_025C_1v80.lib
```
- To see the logic it has realised enter the comand.
```bash
show
```
- To command to see the Netlist of the verilog file 
```bash
write_verilog -nossr good_mux_netlist.verilog
```
