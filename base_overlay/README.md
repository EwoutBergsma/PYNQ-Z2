# Preliminary info

At this point it is important to understand the main hardware concepts of the PYNQ Z2. The System on a Chip (SoC) that is at the heart of the PYNQ Z2 belongs to the AMD ZYNQ 7000 family. On the PYNQ Z2 this chip is located underneath the black heatsink. Most importantly it features two subsystems:
- Processing System (PS): An ARM processor that runs a linux operating system, hosting the Jupyter Notebook webserver.
- Programmable Logic (PL): Essentially the Field Programmable Gate Array (FPGA).

Secondly, it is important to realise that most of the peripherals (LEDs, switches, buttons etc.) and connectors (Arduino headers, Raspberry Pi headers, PMOD, SPI, HDMIs) on the PYNQ Z2 are connected to the PL.

[This video](https://youtu.be/ynCTTG0G3Wc?si=_L_mwLgAm63jsrAk) does a nice job at explaning the above and more.

The PS works as one would expect, it facilitates the user interface that allows us to run Python code on the PS, through the usage of Jupyter Notebooks environment. The PL on the other hand is trickier. For it to do anything one must first configure it. This can be done by loading an overlay to it.

# Base overlay

The base overlay comes already installed on your PYNQ Z2 (assuming you followed [this](/README.md#installing-the-software)). To play around with it one can do the following:

1. Create a new Jupyter Notebooks, by connecting and interfacing with the Jupyter Notebooks environment as explained [here](/README.md#connecting)
1. In a code cell add the following code:
```python
from pynq.overlays.base import BaseOverlay
base = BaseOverlay(base.bit)  # This uploads the provided base overlay to the FPGA of the PYNQ's SoC

help(base)  # This prints more information about the overlay
```
3. Part of the printed output there is a bit that says:
```
leds : AxiGPIO

     4-bit output GPIO for interacting with the green LEDs LD0-3
```
4. To further investigate it one can do:
```python
help(base.leds)
```
5. From that output we can learn that these are addressable, one of the examples informs that one can do:
```python
base.leds[0].on()
delay(100)
base.leds[0].off()
```
6. Another useful trick is to use Python's build-in dir() function to find properties and methods of the specified object (more info about dir() [here](https://www.w3schools.com/python/ref_func_dir.asp)):
```python
dir(base.leds[0])
```
7. Can you find some more interesting functions to call? 
7. Perhaps play around with the switches and buttons too!

Some more documentation on the base overlay can be found [here](https://pynq.readthedocs.io/en/latest/pynq_overlays/loading_an_overlay.html) and [some here](https://pynq.readthedocs.io/en/latest/pynq_overlays/pynqz2/pynqz2_base_overlay.html).