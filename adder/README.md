# Adder example

As a simple example of the FPGA hardware acceleration, we can use the adder example ([original source](https://www.youtube.com/watch?v=2ErFDGSv5EE) more info on that [here](/adder/README.md#there-is-more))  found in this repository:
1. Clone this repository to your PC.
1. Get the `adder.bit` and `adder.hwh` files onto your PYNQ Z2, you can do this using the upload button in the Jupyter Notebooks user interface (or using [this alternative](https://pynq.readthedocs.io/en/latest/getting_started/pynq_z2_setup.html#accessing-files-on-the-board))
1. From within a Jupyter Notebooks, in Python, upload the overlay to the FPGA, like so:
```python
from pynq import Overlay
overlay = Overlay("adder.bit")

help(overlay)  # This provides info about the overlay
```
4. Somewhere at the top of the `help(overlay)` output, there is the mention of an IP Block named `add_0`, after running `help(overlay.add_0)`, there are mentions of `read()` and `write()` functions.
4. Use those functions to interact with the FPGA to make it do addition. To do so you can use the adresses  `0x10` and `0x18` to write. The read address is `0x20`. This can be implemented as follows:

```python
overlay.add_0.write(0x10, 3)
overlay.add_0.write(0X18, 6)
overlay.add_0.read(0x20)  # What will be the output!?
```
6. Further investigation, for example using `dir(overlay.add_0)` reveals `register_map`, which in turn reveals `a`, `b` and `c`. Those are the registers, by doing `help(overlay.add_0.register_map.a)` one can read that this register is write-only, likewise is `.b`. However, `.c` is read-only. With this information it takes only a little bit of creativity to try the following:
```python
overlay.add_0.register_map.a = 3
overlay.add_0.register_map.b = 9
overlay.add_0.register_map.c
```
7. What's the output? Note that this is can be more convenient, as one does not need to know/remember the addresses!

This above way of interacting with the FPGA is the default one. It is called a Memory Mapped Input Output (MMIO), as it literally writes and reads (read: inputs and outputs) to those specific memory addresses. One could [write a Python driver](https://pynq.readthedocs.io/en/latest/overlay_design_methodology/overlay_tutorial.html#Creating-a-Driver) to make it more user friendly.

# There is more

This repository provided a ready-made overlay for the adder. But you could also make it yourself. 

The [original source](https://www.youtube.com/watch?v=2ErFDGSv5EE) uses High Level Synthesis (HLS) to create an IP block that is then used in Vivado to generate the overlay. That tutorial still uses Vivado HLS to achieve this, the newer version of that software is called Vitis HLS. By swapping out Vivado HLS with Vitis HLS, one should still be able to follow that tutorial.

The above tutorial essentially uses [this documentation](https://pynq.readthedocs.io/en/latest/overlay_design_methodology/overlay_tutorial.html#Overlay-Tutorial) in order to implement the following HLS code:

```c
void add(int a, int b, int& c) {
#pragma HLS INTERFACE ap_ctrl_none port=return
#pragma HLS INTERFACE s_axilite port=a
#pragma HLS INTERFACE s_axilite port=b
#pragma HLS INTERFACE s_axilite port=c

    c = a + b;
}
```

