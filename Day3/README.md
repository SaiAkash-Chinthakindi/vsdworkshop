
# Combinational and Sequential Optimizations

## Introduction to optimisations

Optimizations basically mean improving the design so it uses less hardware and works faster. The tool tries to remove extra logic, combine expressions, and clean up anything that isn’t needed. It doesn’t change the function, it just makes the circuit more efficient.

### Combinational logic optimisation

It is the squeezing the logic to get the most optimised design in terms of Area and power savings.

The Techniques used are:

- The constant propagation technique which is direct optimisation.

- The Boolean logic optimisation which convertes a larger boolean equation into an optimised and efficient logic expression using techniques like K-map or Quine Mcklusky.

### Sequential logic optimisation

Sequential logic optimization is when we try to improve the parts of the circuit that use flip-flops. The tool tries to remove extra registers, simplify the state logic, and make the timing better.

There are two techniques used: 

- Basic technique which is sequence constant propagation

- Advanced techniues involving - state optimisation, Retimimg and Sequential logic cloning.

## Lab on Combinational logic optimisations

We are going to use the below mentioned files for this Lab.

We are going to perform optimisation on **opt_check.v** file. 

verilog code of the **opt_check.v**

-- image of the verilog code will be here

- To get the files that we are going to use for this lab:

```bash
ls *opt_check*
```
-- image of the lab_files

- We have to invoke the yosys using the command
```bash
yosys
```
- We have to read the .lib file 
```bash
read_liberty -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
```
- We have to read the verilog file
```bash
read_verilog opt_check.v
```
- We have to keep the opt_check as the top module for synthesis
```bash
synth -top opt_check
```
- The command to do constant propagation and optimisation
```bash
opt_clean -purge
```
- To perform the synthesis operation 
```bash
abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
```
- to show the optimised circuit 
```bash
show
```

--image of the optimised circuit i.e and gate

Similarly to perform optimisation on **opt_check2.v**,**opt_check3.v**,**opt_check4.v** file. we are going to follow the same steps as above. 

Verilog code for the **opt_check2.v**

-- image of the verilog code will be here

-- image of the output circuit will be here


Verilog code for the **opt_check3.v**

-- image of the verilog code will be here

-- image of the output circuit will be here

Verilog code for the **opt_check4.v**

-- image of the verilog code will be here

Optimised boolean equation of the circuit
-- image of the optimised boolean circuit

-- image of the output circuit will be here

Verilog code for the **multiple_modules_opt.v**

-- image of the verilog code will be here

Optimised boolean equation of the circuit
-- image of the optimised boolean circuit

-- image of the output circuit will be here

Verilog code for the **multiple_modules_opt2.v**

-- image of the verilog code will be here

Optimised boolean equation of the circuit
-- image of the optimised boolean circuit

-- image of the output circuit will be here


## Lab on Sequential logic optimisations

In this lab we are going to see optimisation of different D- flip flop.

- circuit1 = **dff_const1.v**

-- verilog code of the circuit1

from the above circuit we can say that whenever the reset is 1 the output of the flip flop is 0 asynchronously. but when the reset is 0 and there is an input at D, then there will be change in the output of the flip flop only at the posedge of the clock.

First we are to going to see the simlation part of the code

code of the simulation of the circuit and see the waveform:

```bash
iverilog dff_const1.v tb_dff_const1.verilog
```

-- image of the gtkwave of the above circuit.

To perform the optimisation on the circuit

- We have to invoke the yosys using the command
```bash
yosys
```
- We have to read the .lib file 
```bash
read_liberty -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
```
- We have to read the verilog file
```bash
read_verilog dff_const1.v
```
- We have to keep the dff_const1 as the top module for synthesis
```bash
synth -top dff_const1
```
- as we are dealing with dff we are going to import libraries for the flip flop using command
```bash
dfflibmap -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
```
- To perform the synthesis operation 
```bash
abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
```
- to show the optimised circuit 
```bash
show
```

-- image of the output wave will be here.

- circuit2 = **dff_const2.v**

-- verilog code of the circuit2

from the above circuit we can say that even when the reset goes low and there is an input at dff(d = 1), the output will always remain 1.

The output waveform of the code:

-- output gtkwave of the code will be here.

The optimised circuit :

-- the optimised circuit will be here

- circuit3 = **dff_const3.v**

-- verilog code of the circuit3

The output waveform of the code:

-- output gtkwave of the code will be here.

The optimised circuit :

-- the optimised circuit will be here

- circuit4 = **dff_const4.v**

-- verilog code of the circuit4

The output waveform of the code:

-- output gtkwave of the code will be here.

The optimised circuit :

-- the optimised circuit will be here

- circuit5 = **dff_const5.v**

-- verilog code of the circuit5

The output waveform of the code:

-- output gtkwave of the code will be here.

The optimised circuit :

-- the optimised circuit will be here















