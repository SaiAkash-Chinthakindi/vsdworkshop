
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

```
module opt_check (input a , input b , output y );
    assign y = a?b:0;
endmodule
```

- To get the files that we are going to use for this lab:

```bash
ls *opt_check*
```
-- ![image alt](https://github.com/SaiAkash-Chinthakindi/vsdworkshop/blob/main/Day3/images/day4_list_of_files_comb.png?raw=true)

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

-- ![image alt](https://github.com/SaiAkash-Chinthakindi/vsdworkshop/blob/main/Day3/images/day4_comb_optimi_circuit_and.png?raw=true)

Similarly to perform optimisation on **opt_check2.v**,**opt_check3.v**,**opt_check4.v** file. we are going to follow the same steps as above. 

Verilog code for the **opt_check2.v**

```
module opt_check2 (input a , input b , output y );
    assign y = a?1:b;
endmodule
```

-- ![image alt](https://github.com/SaiAkash-Chinthakindi/vsdworkshop/blob/main/Day3/images/day4_comb_optimi_circuit2.png?raw=true)


Verilog code for the **opt_check3.v**

```
module opt_check3 (input a , input b ,input c, output y );
    assign y = a?(c?b:0):0;
endmodule
```

-- ![image alt](https://github.com/SaiAkash-Chinthakindi/vsdworkshop/blob/main/Day3/images/day4_comb_optimi_circuit3.png?raw=true)

Verilog code for the **opt_check4.v**

```
module opt_check3 (input a , input b ,input c, output y );
    assign y = a?(b?(a & c):c):(!c);
endmodule
```

Optimised boolean equation of the circuit
-- ![image alt](https://github.com/SaiAkash-Chinthakindi/vsdworkshop/blob/main/Day3/images/day4_comb_optimi_circuit4_circuit_representation.png?raw=true)

-- ![image alt](https://github.com/SaiAkash-Chinthakindi/vsdworkshop/blob/main/Day3/images/day4_comb_optimi_circuit4.png?raw=true)

Verilog code for the **multiple_modules_opt.v**

```
module sub_module1(input a, input b , oputput y);
  assign y = a & b;
endmodule

module sub_module2(input a , input b , oputput y);
  assign y = a ^ b;
endmodule

module multiple_module_opt(input a , input b, input c, input d, output y);
  wire n1,n2,n3;
  
  sub_module1 U1 (.a(a), .b(1'b1), .y(n1));
  sub_module1 U2 (.a(n1), .b(1'b0), .y(n2));
  sub_module2 U3 (.a(b), .b(d), .y(n3));
  
  assign y = c | (b & n1);
endmodule

```

Optimised boolean equation of the circuit
-- ![image alt](https://github.com/SaiAkash-Chinthakindi/vsdworkshop/blob/main/Day3/images/day4_comb_optimi_multiple_modules_circuit_optimisation_representation.png?raw=true)

-- ![image alt](https://github.com/SaiAkash-Chinthakindi/vsdworkshop/blob/main/Day3/images/day4_comb_optimi_multiple_modules_circuit_representation.png?raw=true)

Verilog code for the **multiple_modules_opt2.v**

```
module sub_module(input a, input b, output y);
  assign y = a & b;
endmodule

module multiple_module_opt2(input a , input b, input c, input d, oputput y);
 wire n1,n2,n3;
 
 sub_module U1(.a(a), .b(1'b0), .y(n1));
 sub_module U1(.a(b), .b(c), .y(n2));
 sub_module U1(.a(n2), .b(d), .y(n3));
 sub_module U1(.a(n3), .b(n1), .y(y));
 
endmodule
```

Optimised boolean equation of the circuit
-- ![image alt](https://github.com/SaiAkash-Chinthakindi/vsdworkshop/blob/main/Day3/images/day4_comb_optimi_multiple_modules_circuit2_optimisation_representation.png?raw=true)

-- ![image alt](https://github.com/SaiAkash-Chinthakindi/vsdworkshop/blob/main/Day3/images/day4_comb_optimi_multiple_modules2_circuit_representation.png?raw=true)


## Lab on Sequential logic optimisations

In this lab we are going to see optimisation of different D- flip flop.

- circuit1 = **dff_const1.v**

-- ![image](https://github.com/SaiAkash-Chinthakindi/vsdworkshop/blob/main/Day3/images/dff_const1.png?raw=true)

from the above circuit we can say that whenever the reset is 1 the output of the flip flop is 0 asynchronously. but when the reset is 0 and there is an input at D, then there will be change in the output of the flip flop only at the posedge of the clock.

First we are to going to see the simlation part of the code

code of the simulation of the circuit and see the waveform:

```bash
iverilog dff_const1.v tb_dff_const1.verilog
```

-- ![image alt](https://github.com/SaiAkash-Chinthakindi/vsdworkshop/blob/main/Day3/images/day4_sequ_circuit1_gtkwave.png?raw=true)

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

-- ![image alt](https://github.com/SaiAkash-Chinthakindi/vsdworkshop/blob/main/Day3/images/day4_sequ_circuit1_optimised_circuit.png?raw=true)

- circuit2 = **dff_const2.v**

-- ![image](https://github.com/SaiAkash-Chinthakindi/vsdworkshop/blob/main/Day3/images/dff_const2.png?raw=true)

from the above circuit we can say that even when the reset goes low and there is an input at dff(d = 1), the output will always remain 1.

The output waveform of the code:

-- ![image alt](https://github.com/SaiAkash-Chinthakindi/vsdworkshop/blob/main/Day3/images/day4_sequ_circuit2_gtkwave.png?raw=true)

The optimised circuit :

-- ![image alt](https://github.com/SaiAkash-Chinthakindi/vsdworkshop/blob/main/Day3/images/day4_sequ_circuit2_optimised_circuit.png?raw=true)

- circuit3 = **dff_const3.v**

-- ![image](https://github.com/SaiAkash-Chinthakindi/vsdworkshop/blob/main/Day3/images/dff_const3.png?raw=true)

The output waveform of the code:

-- ![image alt](https://github.com/SaiAkash-Chinthakindi/vsdworkshop/blob/main/Day3/images/day4_sequ_circuit3_gtkwave.png?raw=true)

The optimised circuit :

-- ![image alt](https://github.com/SaiAkash-Chinthakindi/vsdworkshop/blob/main/Day3/images/day4_sequ_circuit3_optimised_circuit.png?raw=true)

- circuit4 = **dff_const4.v**

-- ![image](https://github.com/SaiAkash-Chinthakindi/vsdworkshop/blob/main/Day3/images/dff_const4.png?raw=true)

The output waveform of the code:

-- ![image alt](https://github.com/SaiAkash-Chinthakindi/vsdworkshop/blob/main/Day3/images/day4_sequ_circuit4_gtkwave.png?raw=true)

The optimised circuit :

-- ![image alt](https://github.com/SaiAkash-Chinthakindi/vsdworkshop/blob/main/Day3/images/day4_sequ_circuit4_optimised_circuit.png?raw=true)

- circuit5 = **dff_const5.v**

-- ![image alt](https://github.com/SaiAkash-Chinthakindi/vsdworkshop/blob/main/Day3/images/dff_const5.png?raw=true)

The output waveform of the code:

-- ![image alt](https://github.com/SaiAkash-Chinthakindi/vsdworkshop/blob/main/Day3/images/day4_sequ_circuit5_gtkwave.png?raw=true)

The optimised circuit :

-- ![image alt](https://github.com/SaiAkash-Chinthakindi/vsdworkshop/blob/main/Day3/images/day4_sequ_circuit5_optimised_circuit.png?raw=true)















