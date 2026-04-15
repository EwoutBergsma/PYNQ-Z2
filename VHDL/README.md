# VHDL

Note, THIS FILE IS A WORK IN PROGRESS, please refer to the pdf, it is better, currently.

This file is based on the Vivado V2017.2 Tutorial, by William D. Richard September 19 2017, updated in September 10 2018. 

VHDL is the text-based way to describe the same digital hardware that Vivado can show graphically in its Block Design view. As we saw in the FIR filter example in this repo, in Vivado, the block diagram lets you connect IP blocks visually, while VHDL lets you define custom logic, module interfaces, and behavior in code; Vivado then combines both during synthesis and implementation. A common workflow is to build the high-level system in the block diagram and use VHDL for custom modules that get added as blocks into that design.

## VHD file

Create a source file named `example.vhd` in a text editor before starting.

```vhdl
LIBRARY IEEE;
USE IEEE.STD_LOGIC_1164.ALL;

ENTITY andx IS
    PORT (
        a      : IN STD_LOGIC;
        b      : IN STD_LOGIC;
        c      : IN STD_LOGIC;
        d      : IN STD_LOGIC;
        e      : IN STD_LOGIC;
        output : OUT STD_LOGIC
    );
END andx;

ARCHITECTURE nonsense OF andx IS
    SIGNAL temp1 : std_logic;
    SIGNAL temp2 : std_logic;
BEGIN
    temp1 <= a AND b AND c;
    temp2 <= d AND e;
    output <= temp1 AND temp2;
END nonsense;
```

## Create the project

1. Open Vivado and click `Create New Project`.
2. Read the intro screen, click `Next`, choose a project name and project directory, then continue.
3. Select `RTL Project`.
4. When you reach Add Sources, click `Add Files` and select your `example.vhd` file.
5. Do **not** enable Copy sources into project. Keep your working source file in the project root so you do not accidentally edit a copied version in a nested directory.
6. Set both the Target Language and Simulator Language to VHDL.
7. Skip constraints for now and click `Next`.

8. Select the target device **xc7a100tcsg324-1**.

<img src="images/04-select-device.png" width="700" alt="Select the Artix-7 xc7a100tcsg324-1 device">

9. Click **Finish**. You should now see a normal Vivado project with your source file loaded.

<img src="images/05-project-created.png" width="700" alt="Vivado project after creation">

## Simulate the design

1. Before simulating, run **Synthesis**.

<img src="images/06-run-synthesis.png" width="700" alt="Run synthesis before simulation">

2. If you only want to simulate, you can stop after synthesis completes. There is no need to run implementation yet.

3. Right-click **Run Simulation** and start a behavioral simulation.

<img src="images/07-run-simulation.png" width="700" alt="Run behavioral simulation">

4. In the **Objects** window, right-click each input signal and **Force Constant** values for your test cases.

5. The original walkthrough first forces signal `a` to logic `0`.

<img src="images/08-force-input-a.png" width="700" alt="Force signal a to logic 0">

6. In the **Tcl Console**, run the simulation for 10 ns:

```tcl
run 10 ns
```

7. Change the input stimulus values and run another 10 ns:

```tcl
run 10 ns
```

8. Use the zoom controls to inspect the waveform more closely.

9. When all five inputs are forced to `'1'`, the output should go high after the next simulation run.

## Inspect the generated logic

1. Open **Elaborated Design** if you want to see the logic implied directly by the VHDL source.

2. Open **Synthesized Design** to see the optimized hardware. In this example, the logic collapses into a **single LUT**.

<img src="images/09-synthesized-design.png" width="700" alt="Synthesized design shown as a single LUT">

## Add board pin constraints

1. In the synthesized design view, expand the schematic until you can see the **6 I/O Ports** view.

2. Assign the package pins for the five inputs and one output.

3. Set the **I/O standard** for all ports to **LVCMOS33**.

<img src="images/10-assign-pins.png" width="700" alt="Assign package pins and set LVCMOS33">

A direct XDC version of the same assignments looks like this:

```xdc
set_property PACKAGE_PIN J15 [get_ports {a}]
set_property PACKAGE_PIN L16 [get_ports {b}]
set_property PACKAGE_PIN M13 [get_ports {c}]
set_property PACKAGE_PIN R15 [get_ports {d}]
set_property PACKAGE_PIN R17 [get_ports {e}]
set_property PACKAGE_PIN H17 [get_ports {output}]

set_property IOSTANDARD LVCMOS33 [get_ports {a b c d e output}]
```

4. When Vivado prompts you to save the constraints, create an `.xdc` file.

5. After adding or changing constraints, synthesis becomes out of date. Run **Synthesis** again.

## Implement the design and generate a bitstream

1. Run **Implementation** after synthesis finishes.

2. When place-and-route completes, open the implemented design.

<img src="images/11-open-implemented-design.png" width="700" alt="Open implemented design after implementation completes">

3. Review any reports you want, then click **Generate Bitstream**.

4. When bitstream generation finishes, open **Hardware Manager**.

## Program the FPGA

1. Connect the FPGA board to your PC or laptop.

2. In **Hardware Manager**, choose **Open Target** and connect to the board.

3. Once the device is visible, click **Program device**.

<img src="images/12-program-device.png" width="700" alt="Program the FPGA from Hardware Manager">

4. After programming finishes, test the design using the board switches and LED.

<img src="images/13-test-on-board.png" width="700" alt="Test the design on the board using switches and LEDs">

## Notes and gotchas

- The biggest trap in this workflow is checking **Copy sources into project**. That can leave you editing a copied file instead of your real working source.
- In this tutorial flow, synthesis is run before simulation.
- If you are only validating behavior, you can stop after simulation and skip implementation/bitstream generation.
- The synthesized hardware can look much simpler than the source-level elaborated logic.
- If you change pin assignments or I/O standards, rerun synthesis before implementation.

## There is more

Once this flow works, the next natural improvements are:

- Replace the GUI pin entry with a hand-edited `.xdc` file
- Add a proper VHDL testbench instead of forcing signals manually
- Compare **Elaborated Design** vs **Synthesized Design** to learn how Vivado optimizes logic
- Move from this simple combinational example to a design with clocks, resets, and on-board peripherals
