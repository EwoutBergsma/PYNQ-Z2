## Adder example

As a simple example of the FPGA hardware acceleration, we can use the adder example ([original source](https://www.youtube.com/watch?v=2ErFDGSv5EE) but it is a bit outdated)  found in this repository:
1. Clone this repository to your PC.
1. Get the `adder.bit` and `adder.hwh` files onto your PYNQ Z2, you can do this using the upload button in the Jupyter Notebooks user interface.
1. From within a Jupyter Notebooks, in Python, upload the overlay to the FPGA, like so:
```python
from pynq import Overlay
overlay = BaseOverlay("adder.bit")

help(overlay)  # This provides info about the overlay
```
4. From within Jupyter Notebooks, interact with the FPGA to make it do addition. To do so you can use the adresses  `0x10` and `0x18` to write. The read address is `0x20`. This can be implemented as follows:

```python
overlay.write(0x10, 3)
overlay.write(0x18, 6)
overlay.read(0x20)
```

The [original source](https://www.youtube.com/watch?v=2ErFDGSv5EE) uses High Level Synthesis (HLS) to create an IP block that is then used in Vivado. That tutorial still uses Vivado HLS to achieve this, the newer version of that software is called Vitis HLS. By swapping out Vivado HLS with Vitis HLS, one should still be able to follow that tutorial.

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

