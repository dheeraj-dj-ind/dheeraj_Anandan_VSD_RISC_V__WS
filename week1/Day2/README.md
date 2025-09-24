# Introduction to .lib File
The `.lib` file is a crucial part of ASIC and VLSI design flows, serving as the standard cell library description for synthesis and timing analysis. It is a bucket of standard cells that are used by the synthesizer during synthesis process

## 1. What Does the File Signify

![alt image](images/liberty_file.png)

`.lib` files encode the complete behavioral and timing specification of standard library cells used by physical design and synthesis tools. Some of the notable significances are - 
- tt - Stands for typical transistors
- 025C - Indicates the average operation temperation 
- 1v80 - The voltage of operation or the supply voltage 
- CMOS - The technology of device
- Units of time(ns), voltage(V), power(nW), current(mA), resistance(kohm), capacitance(pF)
- Different variations of the same gate and different gates 

## 2. Comparing Gates with Different Flavor

![alt image](images/comparing_std_cells.png)

The `.lib` file includes multiple drive strengths and threshold flavors for cells (like AND2X1, AND2X2, AND2X4), enabling Power-Performance-Area (PPA) trade-offs.
- More the number of inputs, larger your cell area becomes - Signifies wider transistors, consumes more power 

## 3. Difference Between Hier and Flat Synthesis

- **Design Organization:**  
  Hierarchical synthesis divides the design into functional modules and synthesizes each module separately, making it easier to manage and debug large projects.  
  Flat synthesis processes the entire design as a single unit, which can become difficult to manage as complexity increases.

- **Optimization Across Boundaries:**  
  Hierarchical synthesis does not optimize logic between modules, potentially missing cross-module improvements but provides faster runtime for big designs.  
  Flat synthesis enables maximum optimization across all parts of the design, but at the cost of significantly higher resource usage and longer synthesis times.

## 4. Commands for Hier and Flat Synthesis

**For Hier Synthesis, use the regular commands:**

```bash 
read_liberty -lib ../lib/sky130_fd_sc_hd_tt_025C_1v80.lib
read_verilog multiple_modules.v
synth -top multiple_modules
abc -liberty ../lib/sky130_fd_sc_hd_tt_025C_1v80.lib
show 
write_verilog -noattr multiple_modules_net.v
!gvim multiple_modules_net.v
```
![Hierarchical Synthesis](images/hierarchical%20design.png)

**For Flat Synthesis, use these commands:**

```bash 
read_liberty -lib ../lib/sky130_fd_sc_hd_tt_025C_1v80.lib
read_verilog multiple_modules.v
synth -top multiple_modules
abc -liberty ../lib/sky130_fd_sc_hd_tt_025C_1v80.lib
flatten
show 
write_verilog -noattr multiple_modules_net.v
!gvim multiple_modules_net.v
```

![Flattened Synthesis](images/flatten%20multiple%20module.png)

**Difference between flatten and hier netlist**

![Hier vs Flatten Netlist](images/hierarchical%20Vs%20Flaten%20syn.png)


## 5. Submodule Synthesis and Why Do We Need It



Submodule synthesis allows isolation and optimization of critical blocks, improving timing and testability for large designs.
- When we have multiple modules of the same design, rahter than synthesizing them one by one, we can synthesize the module once and replicate it multiple times which saves time and speed.
- When the design is massive, the tool takes more time to synthesize. We can give the tool one submodule at a time and stich the other submodules together, making it more efficient.

```bash 
$ yosys
read_liberty -lib ../lib/sky130_fd_sc_hd_tt_025C_1v80.lib
read_verilog multiple_modules.v
synth -top sub_module1
abc -liberty ../lib/sky130_fd_sc_hd_tt_025C_1v80.lib
show 
write_verilog -noattr multiple_modules_net.v
!gvim multiple_modules_net.v
```

![alt image](images/sub_module%20syn.png)

## 6. Why Do We Need Flip Flops
Flip flops are edge-triggered memory elements essential for state retention, synchronization, and pipelining in sequential circuits.
- In combinational circuits, the output changes after the propogation delay of the inputs, this results in glitching.
- If a circuit has only combinational circuits, the output will be very unstable. This is were flops come into picture.
- Flip flops are used to stabilize the combinational circuit output by storing it. It's output changes only at the clock edge, thereby restricting gliches. 
- But, we need to initialize the flop so that the combinational ckt has a reference input. That's why we use pins called set and reset.


---

## 7. Different Coding Styles for Flops

### a) Async Reset
An asynchronous reset allows the flip-flop or register to be reset immediately, independent of the clock signal.
The reset takes effect as soon as the reset signal is asserted, providing quick initialization or clearance of outputs.

![Asycnronous Reset Waveform](images/async_rst_dff_waveform.png)
![Asyncronous Reset Report](images/dff_async_rst_report.png)
![Asyncronous Reset Synthesis Output](images/dff_asynrst_syn.png)


### b) Async Set
An asynchronous set allows the flip-flop or register to be set immediately, independent of the clock signal. The output is set to 1 depending on async_set signal. The reset takes effect as soon as the reset signal is asserted, providing quick initialization or clearance of outputs.

![Asycnronous Set Waveform](images/asyncset_dff_waveform.png)
![Asyncronous Set Synthesis Output](images/dff_async_set_syn.png)


### c) Sync Reset

![alt image](images/sync-reset.jpg)

A synchronous reset only affects the flip-flop or register output on a clock edge, making reset behavior predictable and easier to analyze. Reset changes are synchronized with the clock, leading to simpler timing closure and fewer chances of metastability.
Synchronous resets are generally recommended in large digital designs for improved robustness and easier static timing analysis.

![Sycnronous Set Waveform](images/sync_dff_rst_waveform.png)
![Syncronous Set Synthesis Output](images/dff_sync_rst_syn.png)



## 8. Interesting Optimizations

### a) Multiply by 2
Rather than using hardware, we can just append a 0 to the output.\
The output of multiply by 2 is {a,0}
![Mul2 Synthesis](images/mul2_syn.png)
![Mul2 Netlist](images/mul2_netlist.png)


### b) Multiply by 9

Multiply by 9 is simply equal to Multiply by 8 + Multiply by 1.\
Multiply by 8 is equal to the same number appended by 000 and multiply by 1 is the number itself.\
Therefore Multiply by 9 = {aa}.
![Mul8 Synthesis](images/mul8_syn.png)
![Mul8 Netlist](images/mul8_netlist.png)





















