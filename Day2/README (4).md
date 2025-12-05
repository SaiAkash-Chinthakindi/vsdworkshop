
# Timing libs, Hierarchical vs Flat synthesis and effective loop coding styles

## Introduction to Timing .libs

- It is a library file that contains all the basic logic gates of different flavours and by using this library we are going to convert the our verilog Behavioural discription to logic gate that are connected as per the requirement.

- The name of the file that contains logic gates is:
```bash 
sky130_fd_sc_hd__tt_025C_1v80.libs
```
- The below images show first 50 lines of the library file
-- [image alt](https://github.com/SaiAkash-Chinthakindi/vsdworkshop/blob/main/Day2/images/day2_sky130_lib.png?raw=true)

-- ![image alt](https://github.com/SaiAkash-Chinthakindi/vsdworkshop/blob/main/Day2/images/day2_sky130_lib1.png?raw=true)

- The first line tells the name of the library i.e sky130 nanometer library and the "tt" stands for typical and 025C is the Temperature.

   - The libraries can be slow, fast and typical libraries.

-- ![image alt](https://github.com/SaiAkash-Chinthakindi/vsdworkshop/blob/main/Day2/images/lib_description.png?raw=true)

- For a Silicon design to work there are three main important factors to be considered.  

     1)Process: There will be different processes due to variation in fabrication.   
     2)Voltage: There will be variation in the Behaviour of the circuit for different voltages.  
     3)Temperature: The Semiconductors are very Senstive to temperature.  

- We want our Silicon Circuit to work as per the requirement irrespective of the change in the above three parameters.So, we need to consider the factors while designing the circuit.

- The libraries will be characterised to model these variations

## What does .lib file tells about?

The library file tells about the Technology being used for building the cells that is "CMOS".It tells about the delay model, time unit, voltage unit, leakage power_unit,current_unit,resistance_unit,capacitive load_unit and the **operating conditions**.

-- ![image alt](https://github.com/SaiAkash-Chinthakindi/vsdworkshop/blob/main/Day2/images/day2_libray_file.png?raw=true)

## What is the .lib file going to contain?

It contains all the types of Standard cells that are available.with each cell showing different features of the cell like the leakage_power() values for different possible combinations of the inputs.

--![image alt](https://github.com/SaiAkash-Chinthakindi/vsdworkshop/blob/main/Day2/images/day2_cell_lekage.png?raw=true)

The below images shows different types of Cells 

--![image alt](https://github.com/SaiAkash-Chinthakindi/vsdworkshop/blob/main/Day2/images/day2_different_cells.png?raw=true)

Example: If we consider AND gate

--image of an AND gate with library 

since there are two inputs total 4 combinations are possible.

--![image alt](https://github.com/SaiAkash-Chinthakindi/vsdworkshop/blob/main/Day2/images/day2_and2_0.png?raw=true)

from the above we can see that as we are going from and2_0 to and 2_4 the area is increasing which indicates that the and2_4 cell is having wider transistors and will be faster in processing which lead to increase of more power consumption.

For the smaller cell, The delay will be more and the area will be less.

# Hierarchical vs Flat synthesis

## Hierarchical synthesis

Hierarchical synthesis is a process of breaking a Top module containing multiple module into smaller modules and synthesising each module seperately instead of flattening the entire circuit into one big netlist.

For example: if we consider multiple_modules.v file which contains two sub_modules in it.  

      sub_module 1 is AND gate  
      sub_module 2 is OR gate 


- verilog code for multiple_modules.v 
-- ![image alt](https://github.com/SaiAkash-Chinthakindi/vsdworkshop/blob/main/Day2/images/day2_verilog_code_multiple_modules.png?raw=true)

- these two sub_modules are synthesised seperately.
-- ![image alt](https://github.com/SaiAkash-Chinthakindi/vsdworkshop/blob/main/Day2/images/day2_hierarchical_synth.png?raw=true)

- netlist representing the Hierarchy of sub_module1 and sub_module2

-- ![image alt](https://github.com/SaiAkash-Chinthakindi/vsdworkshop/blob/main/Day2/images/day2_hier.png?raw=true)

## Flat synthesis

In this synthesis process we are removing all module hierarchy and synthesizing the entire design as one big gate level block for maximum optimization.

- the command used to write out a flat netlist is 
```bash
yosys> flatten
```
- netlist representing the multiple_modules after flatten

--![image alt](https://github.com/SaiAkash-Chinthakindi/vsdworkshop/blob/main/Day2/images/day2_flatten.png?raw=true)

--![image alt](https://github.com/SaiAkash-Chinthakindi/vsdworkshop/blob/main/Day2/images/day2_image_of%20the%20flatten.png?raw=true)

## Various flop coding styles and optimization

### Why flops ?

Flops are generally used for storing 1-bit of data.Flops can be Edge-triggered or level-triggered depending on the requirement. we basically use flop along with the combinational circuits as they dont have the memory element to store the output.So, we use flops to hold the output of the combinational ciruit and make the circuit work in a proper sequence.

If there are many combinational circuits connected together.There might be a possibility that the outputs may not be stable which can result in a glitch and in order to avoid glitches and synchronize the whole design we use flops that updates the output only on the clock.

--images of the comb and the flops

the above images shows the connections of the combinational circuit with D- Flip Flop which is also known a data Flip Flop.

### Lab on Coding styles of Flops

In this Lab we are going to see different coding styles of flops

- Flop with Asynchronous reset 

In this type of flop the output of the flip flop will be set to 0 irrespective of the clock. There can be two types of asynchronous reset : negative-edge trigger and positive-edge trigger reset

code:
```
code should be written here 
```

Output graph:

--image of the output graph will be here

synthesis:

the code to access the design for the D-Flip flop from the standard cell library
```bash
dfflibmap -liberty ../lib/sky130_fd_sc_hd___tt_025C_1v80.lib
```

-- image of the synthesis graph goes here

- Flop with syncronous reset

In this type of flop the output will change to 0 only at the posedge or negedge of clock i.e the input is synchronous with the clock.

code:
```bash
code should be writtel here
```
output graph:

--image of the output graph will be here

synthesis:

-- image of the synthesis graph goes here

- Flop with asynchronous set

In this type of flop irrespective of the clock the output will be set to 1.

code: 
```
code will go here
```

output graph: 

--image og the output graph will be here.

synthesis:

-- image of the synthesis grapth goes here

- Flop with Asynchronous reset and synchronous reset

In this types of Flop the output will be set to 0 in two cases
1) the output will be set to 0 irrespective of the clock i.e     is asynchronous reset
2) the output will be set to 0 during the positive edge of the clock
in other cases the output will follow the input.

code:
```
the code will be here
```

output:
-- output graph will be here

synthesis:

-- image of the synthesis graph goes here

### Lab on Special Optimizations

1) If we want to multiply any number by 2 or any power of 2 (like 2¹ = 2, 2² = 4, 2³ = 8, 2⁴ = 16), the output is simply the number shifted to the left by that many positions. In binary, a left shift by n bits is the same as multiplying the number by 2ⁿ.

Example:

-- code for the mult_2

-- image for the mult_2


2) If we multiply a 3-bit number by 9 and the output is 6 bits long, the result will have the same 3-bit pattern repeated in both the upper 3 bits and the lower 3 bits. This is because multiplying by 9 is like multiplying by (8 + 1), so the number appears once shifted and once in its original place.

Example :   
if we multiply 4 with 9 and the output y is 6-bits in lenght([5:0]y)

the binary representation of 4 is 100 
if we multiply it by 9 which we can write it as 4 * [8 + 1]

the output will be (4 * 8) + (4 * 1)

from the above case as we are multiplying with the power of 2 
the 4 will be shifted to left by 3 units = (100000) and will be added with 4 

the result will be = (100000 + 100)
                   = 100100
                  
-- code for the mult_9

-- image of the circuit of mult_9

netlist produced after performing the synthesis operation

-- image of the mult_8_netlist















