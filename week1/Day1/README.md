# Introduction to Iverilog, Testbench and Simulation

## 1. What is a simulator
A simulator is a software tool that mimics the behavior of hardware designs, allowing verification of digital circuits by running test scenarios without physical hardware.

## 2. What is a design and testbench
- **Design:** The actual hardware module or system described using Hardware Description Language (HDL).
- **Testbench:** A separate module that generates stimulus signals and checks outputs of the design to validate its behavior.

## 3. How does a simulator work
Simulators compile the HDL source code into an executable form and run it, emulating the digital circuit's operations and generating timing waveforms or textual outputs for verification.

## 4. Iverilog based simulation flow
The flow includes compiling Verilog files with `iverilog`, running the output with `vvp`, and viewing waveforms using tools like GTKWave.

## 5. Environment set up to run labs
Install Icarus Verilog (`iverilog`) and GTKWave. Ensure the PATH environment variable includes their binaries. Use a text editor or IDE supporting Verilog development.

## 6. Working with Iverilog and GTKWave

### a) To open design and testbench in Iverilog
Use the command:

### b) Executing a.out file
Run the compiled simulation with:

### c) Viewing waveforms using GTKWave
Generate dump files (`.vcd`) in your testbench and open them:

## 7. Viewing file structure of design implemented
Organize your project files in folders such as `src/` for design and `tb/` for testbench. The structure can be viewed via your file explorer or command line.

## 8. Introduction to Yosys

### a) What is a synthesizer
A synthesizer converts HDL code into a gate-level netlist suitable for hardware implementation.

### b) How to verify that synthesis is correct
Verification is done by comparing simulation results of the post-synthesis netlist against the original RTL simulation.

### c) What is logic synthesis
Logic synthesis translates behavioral HDL models into a network of logic gates.

## 9. What does the .lib file contain

### a) Why do we need different flavours of gates
Different gate flavors optimize for speed, power, and area under various process conditions.

### b) Information on signal period and signal speed
.lib files provide timing information about gate delays related to signal transitions and timing margins.

### c) Why do we need fast and slow transistors
Fast transistors are used for high-speed paths; slow transistors optimize power and reduce leakage on non-critical paths.

### d) Selection of cells
Cell selection balances timing, area, and power criteria based on design requirements.

## 10. Synthesizer process
The process includes reading HDL, mapping logic to standard cells, optimizing timing and area, and generating gate-level netlist.

## 11. Working on Yosys

### a) Invoke Yosys
Run yosys by typing `yosys` in your terminal.

### b) Read liberty file
Use the `read_liberty` command to import technology libraries.

### c) Reading design
Use `read_verilog` to load your design files.

### d) Modules to synthesize
```bash
synth -top good_mux
```

### e) Convert RTL to gates
```bash
abc -liberty ../lib/sky130_fd_sc_hd_tt_025c_1v80.lib
```

### f) Showing logic that has been realized
```bash
show
```
### g) Writing netlist
```bash
write_verilog good_mux_netlist.v
```

### h) Viewing netlist
```bash
!gvim good_mux_netlist.v
```

### i) How to obtain netlist in a simpler way
```bash 
write_verilog -noattr good_mux_netlist.v
```

