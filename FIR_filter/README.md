#  FIR Filter

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

