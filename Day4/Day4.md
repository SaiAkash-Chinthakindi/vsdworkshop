
# GLS, blocking vs Non-blocking and Synthesis - Simulation mismatch

### What is GLS?

GLS stands for Gate Level Simulation. It means running the testbench with the synthesized netlist as the design under test. The netlist is logically the same as the RTL, so the same testbench will work for both. The inputs and outputs in the RTL and netlist match, and GLS helps us check that the design still behaves correctly after synthesis.

![image alt](https://github.com/SaiAkash-Chinthakindi/vsdworkshop/blob/main/Day4/images/day5_GLS_layout.png?raw=true)

### Why GLS?

- To verify the logical correctness of delay after Synthesis
- To Ensure the timing of the design is met and for this the GLS needs to run with delay annotation.

### Synthesis Simulation mismatch

The Synthesis and Simulation mismatch may occure due to some reasons:

- missing Sensitivity list : Missing sensitivity list means the always block doesn’t include all the inputs it depends on. Because of that, RTL simulation may give wrong or stale outputs while the synthesized hardware still reacts correctly, causing a mismatch.

- Blocking vs Non-Blocking Assignments
- Non Standard verilog coding

### Lab on GLS Synthesis Simulation mismatch

The files that are going to be used for this lab are: **ternary_operator_mux.v** , **bad_mux.v**, **good_mux.v**

1) **ternary_operator_mux.v**

To perform the RTL simulation on the file we have to use the command:
```bash
iverilog ternary_operator_mux.v tb_ternary_operator_mux.v
```
To get the vcd file use the command:
```bash
./a.out
```
To display the wave form use command:
```bash
gtkwave tb_ternary_operator_mux.vcd
```
Now, we have to perform the synthesis operation on the verilog file.

-- ![image alt](https://github.com/SaiAkash-Chinthakindi/vsdworkshop/blob/main/Day4/images/day5_ternary_operator_optimised.png?raw=true)

To perform the GLS operation on the obtained netlist. we have to use the command :

```bash
iverilog ../my_lib/verilog_model/primitives.v ../my_lib/verilog_model/sky130_fd_sc_hd.lib ternary_operator_mux_net.v tb_ternary_operator_mux.v
```
use the command below to get the vcd file
```bash
./a.out
```
-- ![image alt](https://github.com/SaiAkash-Chinthakindi/vsdworkshop/blob/main/Day4/images/day5_ternary_operator_gtkwave_netlist.png?raw=true)

1) **bad_mux.v**

To perform the RTL simulation on the file we have to use the command:
```bash
iverilog bad_mux.v bad_mux.v
```
To get the vcd file use the command:
```bash
./a.out
```
To display the wave form use command:
```bash
gtkwave tb_bad_mux.vcd
```
Now, we have to perform the synthesis operation on the verilog file.

-- ![image alt](https://github.com/SaiAkash-Chinthakindi/vsdworkshop/blob/main/Day4/images/day5_bad_mux_gtkwave.png?raw=true)

To perform the GLS operation on the obtained netlist. we have to use the command :

```bash
iverilog ../my_lib/verilog_model/primitives.v ../my_lib/verilog_model/sky130_fd_sc_hd.lib bad_mux_net.v tb_bad_mux.v
```
use the command below to get the vcd file
```bash
./a.out
```
-- ![image alt](https://github.com/SaiAkash-Chinthakindi/vsdworkshop/blob/main/Day4/images/day5_bad_mux_gtkwave_netlist.png?raw=true).

From the obtained gtkwave from RTL simulation and GLS simulation we can see that in RTL simulation the output is not following the input with respect to the select lines but in the case of GLS simulation the outputs are following the inputs with respect to the select lines. from the above graphs we can say that there is synthesis simulation mismatch.


### Lab on Synthesis-Simulation mismatch for Blocking Statement

We are going to use the file **blocking_caveat.v**

First we are going to perform RTL simulation on the verilog file
```bash
iverilog blocking_caveat.v tb_blocking_caveat.v
```
To get the vcd file
```bash
./a.out
```
To get the gtkwave for the RTL simulation
```bash
gtkwave tb_blocking_caveat_net.v
```
-- ![image alt](https://github.com/SaiAkash-Chinthakindi/vsdworkshop/blob/main/Day4/images/day5_blocking_caveat_RTL_gtkwave.png?raw=true)

After performing the synthesis operation and getting the netlist for the the verilog code the obtained GLS waveform is:

-- ![image alt](https://github.com/SaiAkash-Chinthakindi/vsdworkshop/blob/main/Day4/images/day5_blocking_caveat_GLS_gtkwave.png?raw=true).

From the two graphs we can see that in the RTL simulation the d input is taking the previous value of the x because of the blocking statement but in the case of the GLS the output d is driven by the present values of the input change. so, we can say that there is a Synthesis-Simulation mismatch for Blocking Statement.

