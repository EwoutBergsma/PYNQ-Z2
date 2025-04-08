#  FIR Filter

So far we have only used provided overlays. Let's now make our own, using Vivado!

1. If you have not already, we first need to add our board (PYNQ Z2) to Vivado.
    - You can [download from this page](https://www.tulembedded.com/FPGA/ProductsPYNQ-Z2.html#:~:text=Z2%20Board%20File), or find them in this repository. Copy and paste the `pynq-z2` folder into `<Xilinx installation directory>/Vivado/<version>/data/boards/board_files`. 
    - If `board_files` does not exist in the `board` folder, create it.
1. Open Vivado
    - (I used version 2024.2)
1. Create Project
1. `Next > give project name and a directory > next > RLT Project > Next > Next > Next > Boards > search pynq-z2 and select it > next > finish`
1. Follow [this tutorial](https://youtu.be/PwG037LuNvA?si=_ieIkane3-Y2PiZm&t=145) from 2:25 onward
    - At around 04:10 the tutorial uses [this website](http://t-filter.engineerjs.com/) for creating the filter coefficients (note, he uses mHz, **not** MHz).
    - At around 7:51 you may get critical warnings [here you can read more about them](https://forum.digilent.com/topic/21356-getting-warnings-while-creating-vivado-project-with-zynq-boards/)
1. Note, around 11:08, be interested in creating a `*.hwh` and a `*.bit` file (**not** `*.tcl`). This can be achieved by navigating `File > Export > Export bitstream file`.
1. After doing that I found the `*.hwh`file in the directory: `\FIR_filter.gen\sources_1\bd\FIR_filter\hw_handoff` and the `*.bit` file in the location you when exporting the bitstream (default is in the root of the Vivado project). **Note**, make sure to have identical file names, for example `fir_filter.bit` and `fir_filter.hwh`.
1. Also, after that, the video uploads the files over the network using file explorer. Alternatively the upload button in Jupyter Notebooks can be used.
1. Now upload the overlay to the FPGA and interact with it. To get started you can take a look at `FIR_accel.ipynb`  ([original source](https://github.com/soheilbh/fir_accel_pynq/tree/main)).
