# PYNQ-Z2

This repository is to assist master Smart Systems Engineering students in their third assignment of the Data Centric Architectures course.

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

Note, if one is interested in High Level Synthesis (HLS), an installation of Vits HLS (*not* Vivado HLS, that's the old software) would also be required. More on that in the [adder example](/adder/).

## Connecting

To really get going start with connecting to your PYNQ Z2 via the browser:
1. Connect your laptop to the PYNQ Z2 Jupyter Notebook environment.
      - At school we can**not** use Hanze's connection and therefore need a direct ethernet connection to your pc.
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

## Getting started

Here is a list of things to try, the order is recommended:
1. [Base Overlay](/base_overlay/)
1. [Adder Example](/adder/)
1. [FIR Filter Example](/FIR_filter/)
1. [Community Projects](/community_projects/)

## What's next?

Besides getting inspiration from the commmunity (see above), one can also look around in the available IP blocks in Vivado.

For the more adventurous type, there is the [hls4ml](https://fastmachinelearning.org/hls4ml/), which previous students have succesfully used to transfer a keras model onto the PYNQ Z2's FPGA. If you are considering this route, please contact me, I can provide more information.  

## Some useful references

- https://pynq.readthedocs.io/en/latest/getting_started.html
- https://nandland.com/fpga-101/
- https://is.muni.cz/el/1433/jaro2015/PV191/um/The_Zynq_Book_ebook.pdf
- https://pynq.tue.nl/
