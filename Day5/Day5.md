
# Optimization in Synthesis

### Labs on "Incomplete if case"

The files that are going to be use for this lab are: 

-- the image of the files fo the incomplete if

The codes corresponding to the Lab:

-- the image of the code of the incomplete if 

1) **incomp_if.v**

The code:

-- image of the code of incomp_if 

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
After performing the synthesis operation on the verilog file the obtained circuit is:

-- image of the circuit after performing the synthesis

From the circuit we can say that then the Enable(i0) is high the output will follow the i1 input but as soon as the i0 goes low the output will have the value of i1 before the Enable goes low and it will remain same for the entire low duration. and the tool is also infering a Latch.

1) **incomp_if2.v**

The code:

-- image of the code of incomp_if2 

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
After performing the synthesis operation on the verilog file the obtained circuit is:

-- image of the circuit after performing the synthesis



