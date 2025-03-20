# PYNQ-Z2 How to get started

Three main steps need to be taken to develop for the PYNQ Z2 

1. Install PYNQ Z2 sofware on its SD Card
   1. Download the software for the PYNQ Z2 from [here](https://github.com/Xilinx/PYNQ/releases)
     - (At the time of writing the newest version was: `PYNQ-Z2 v3.0.0 SDCard image`)
   2. Unzip it!
   3. Insert the SD Card into your pc
   4. Using your favourite disk imager (mine is [Rufus](https://rufus.ie/en/)), flash the .img to the SD Card
   5. Once it is done, insert the SD card into the PYNQ Z2
2. Install Vivado on your computer
  - For Windows, download from [here](https://www.xilinx.com/support/download/index.html/content/xilinx/en/downloadNav/vivado-design-tools.html), Linux is available elsewhere, MacOS is unavailable.
  - Unfortunately you will have to make an account (you can put Hanze's information).
  - Launch the downloaded executable, download Vivado ML Standard (you can prevent it from installing unnessecary stuff, that can save a lot of time. The downloader asks you to disable your antivirus software, we do not recommend this.)
  - After download the executable should also install Vivado
3. Connect your laptop to the PYNQ Z2
  - At school the only way of connecting is through a USB connection
  - At home you can connect through the ethernet connection
