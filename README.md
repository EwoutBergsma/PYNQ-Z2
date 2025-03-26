# PYNQ-Z2

## Installing the software

Two main steps need to be taken to in terms of installing software for the PYNQ Z2:

1. Install PYNQ Z2 sofware on its SD Card.
   1. Download the software for the PYNQ Z2 from [here](https://github.com/Xilinx/PYNQ/releases).
      - (At the time of writing the newest version was: `PYNQ-Z2 v3.0.0 SDCard image`).
   1. Unzip it!
   1. Insert the SD Card into your pc.
   1. Using your favourite disk imager (mine is [Rufus](https://rufus.ie/en/)), flash the .img to the SD Card.
   1. Once it is done, insert the SD card into the PYNQ Z2.
2. Install Vivado on your computer.
    1. For Windows, download from [here](https://www.xilinx.com/support/download/index.html/content/xilinx/en/downloadNav/vivado-design-tools.html), Linux is available elsewhere, MacOS is unavailable.
        - Unfortunately you will have to make an account (you can put Hanze's information).
    2. Launch the downloaded executable, download Vivado ML Standard (you can prevent it from installing unnessecary stuff, that can save a lot of time. The downloader asks you to disable your antivirus software, we do not recommend this).
    3. After download, make sure to also install Vivado (it require 55GB of free space).

## Getting started

To really get going start with connecting to your PYNQ Z2 via the browser:
1. Connect your laptop to the PYNQ Z2 Jupyter Notebook environment.
      - At school we can**not** use school's connection and therefore need a direct ethernet connection to your pc.
          1. Connect an ethernet cable between your PC and PYNQ Z2.
          1. Power your board using the power adapter.
          1. On your Windows 11 machine, navigate: `settings > network & internet > advanced network settings > unidentified network > edit more adapter options > select IPv4 > Properties`, copy these settings: ![](ethernet_settings_at_Hanze.png)
          Press OK, then Close.
          1. Open this in the browser: http://192.168.2.99:9090/
              - Be patient. If it does not work, reboot your PYNQ Z2. Then be _very_ patient, the PYNQ Z2 is booted when the LEDs blink for a few times.
          1. The default password is `xilinx`.
      - At home you can probably hook up your PYNQ Z2 to your router.
          - The benefit to this is that the PYNQ Z2 will then also have internet access.
          - Find the IP address of your PYNQ Z2 through your router's admin panel (or by scanning your local network).
2. In the Jupyter Notebooks environment you can find some example files. Feel invited to look at those, but do not spend too much time on them, they are of limited use.

## Base example

1. Through your browser, visit the Jupyter Notebook GUI and make a new notebook.
1. Put this code in a notebook:
```python
from pynq.overlays.base import BaseOverlay
base = BaseOverlay("base.bit")

help(base)  # This provides info about the overlay
```
3. Run the code. The overlay will get loaded onto the FPGA, essentially configuring the internal hardware of the FPGA. This simple overlay merely allows you to interact with the peripherals (LEDs, switches, etc.) that are on the PYNQ Z2. Note, almost all of the peripherals on the board are only connected to the FPGA. This base overlay allows the CPU to interact with these peripherals through the FPGA.
3. Try to turn on/off the LEDs, and read out the switches. You can use `help()` and/or `dir()`.
    - Or, for more information [see the docs](https://pynq.readthedocs.io/en/v2.6.1/pynq_overlays/loading_an_overlay.html).

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

##  FIR Filter

So far we have only used provided overlays. Let's now make our own, using Vivado!

1. If you have not already, we first need to add our board (PYNQ Z2) to Vivado.
    - You can [download from this page](https://www.tulembedded.com/FPGA/ProductsPYNQ-Z2.html#:~:text=Z2%20Board%20File), or find them in this repository. Copy and paste the `pynq-z2` folder into `<Xilinx installation directory>/Vivado/<version>/data/boards/board_files`. 
    - If `board_files` does not exist in the `board` folder, create it.
1. Open Vivado
    - (I used version 2024.2)
1. Create Project
1. `Next > give project name and a directory > next > RLT Project > Next > Next > Next > Boards > search pynq-z2 and select it > next > finish`
1. Follow [this tutorial](https://youtu.be/PwG037LuNvA?si=rXmCiVVOlwD1N3on&t=173) from 2:52 onward
1. Note, around 11:08, you are interested in a `*.hwh` file (**not** `*.tcl`) and a `*.bit`.
1. Also, after that, the video uploads the files over the network using file explorer. Alternatively the upload button in Jupyter Notebooks can be used.

## Community Projects

We can also use the power of the community, like [here](https://www.pynq.io/community.html) or [here](https://www.pynq.io/embedded.html). 
- Note, since [version 2.6 .tcl files are deprecated](https://pynq.readthedocs.io/en/latest/changelog.html#:~:text=Tcl%20parsing%20removed%20%2D%20please%20generate%20and%20use%20an%20HWH%20file%20for%20Overlays). This means that only `*.hwh` files are currently supported. Ignore any (online) project that do not provide `*.hwh` files, `*.bit` files are also still necessary.

`More information about community projects TBA`