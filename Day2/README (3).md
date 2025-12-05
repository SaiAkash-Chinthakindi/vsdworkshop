
# Timing libs, Hierarchical vs Flat synthesis and effective loop coding styles

## Introduction to Timing .libs

- It is a library file that contains all the basic logic gates of different flavours and by using this library we are going to convert the our verilog Behavioural discription to logic gate that are connected as per the requirement.

- The name of the file that contains logic gates is:
```bash 
sky130_fd_sc_hd__tt_025C_1v80.libs
```
- The below images show first 50 lines of the library file
  
-- ![image alt](https://github.com/SaiAkash-Chinthakindi/vsdworkshop/blob/main/Day2/images/day2_sky130_lib.png?raw=true)

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
--![image alt](https://github.com/SaiAkash-Chinthakindi/vsdworkshop/blob/main/Day2/images/day2_hierarchical_synth.png?raw=true)

- netlist representing the Hierarchy of sub_module1 and sub_module2

--![image alt](https://github.com/SaiAkash-Chinthakindi/vsdworkshop/blob/main/Day2/images/day2_hier.png?raw=true)

## Flat synthesis

In this synthesis process we are removing all module hierarchy and synthesizing the entire design as one big gate level block for maximum optimization.

- the command used to write out a flat netlist is 
```bash
yosys> flatten
```
- netlist representing the multiple_modules after flatten

--![image alt](https://github.com/SaiAkash-Chinthakindi/vsdworkshop/blob/main/Day2/images/day2_flatten.png?raw=true)

--![image alt](https://github.com/SaiAkash-Chinthakindi/vsdworkshop/blob/main/Day2/images/day2_image_of%20the%20flatten.png?raw=true)











