
# Optimization in Synthesis

### Labs on "Incomplete if case"

The files that are going to be use for this lab are: 

-- ![image alt](https://github.com/SaiAkash-Chinthakindi/vsdworkshop/blob/main/Day5/images/day6_files_for%20Optimisation_in_synthesis.png?raw=true)

The codes corresponding to the Lab:

-- ![image alt](https://github.com/SaiAkash-Chinthakindi/vsdworkshop/blob/main/Day5/images/day6_files_for%20Optimisation_in_synthesis_code.png?raw=true) 

1) **incomp_if.v**

The code:

-- ![image alt](https://github.com/SaiAkash-Chinthakindi/vsdworkshop/blob/main/Day5/images/incomp_if.png?raw=true)

We are going to perform the RTL simulation on the verilog file

```bash 
iverilog incomp_if.v tb_incomp_if.v
```
To get the RTL file
```bash
./a.out
```
To view the waveform
```bash
gtkwave tb_incomp_if.vcd
```
![image alt](https://github.com/SaiAkash-Chinthakindi/vsdworkshop/blob/main/Day5/images/day6_gtkwave_incomp_if_rtl_graph.png?raw=true)
After performing the synthesis operation on the verilog file the obtained circuit is:

-- ![image alt](https://github.com/SaiAkash-Chinthakindi/vsdworkshop/blob/main/Day5/images/day6_graph_after_synthesis_incomp_if.png?raw=true)

From the circuit we can say that then the Enable(i0) is high the output will follow the i1 input but as soon as the i0 goes low the output will have the value of i1 before the Enable goes low and it will remain same for the entire low duration. and the tool is also infering a Latch.

1) **incomp_if2.v**

The code:

-- ![image alt](https://github.com/SaiAkash-Chinthakindi/vsdworkshop/blob/main/Day5/images/day6_incomp_if2_code.png?raw=true) 

We are going to perform the RTL simulation on the verilog file

```bash 
iverilog incomp_if.v tb_incomp_if2.v
```
To get the RTL file
```bash
./a.out
```
To view the waveform
```bash
gtkwave tb_incomp_if2.vcd
```
![image alt](https://github.com/SaiAkash-Chinthakindi/vsdworkshop/blob/main/Day5/images/day6_gtkwave_incomp_if2_rtl_graph.png?raw=true)
After performing the synthesis operation on the verilog file the obtained circuit is:

-- ![image alt](https://github.com/SaiAkash-Chinthakindi/vsdworkshop/blob/main/Day5/images/day6_graph_after_synthesis_incomp_if2.png?raw=true)



