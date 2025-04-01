# Base Overlay


The base overlay comes already installed on your PYNQ Z2 (assuming you followed the installation guide found in the `README.md` file in the root of this repository). To play around with it one can do the following:

1. Create a new Jupyter Notebooks, by connecting and interfacing with the Jupyter Notebooks environment as explained in the `README.md` found in the root of this repository.
1. In a code cell add the following code:
```python
from pynq.overlays.base import BaseOverlay
base = BaseOverlay(base.bit)  # This uploads a provided overlay to the FPGA of the PYNQ's SoC

help(base)  # This prints more information about the overlay
```

TBA: more information about the base overlay