# Task-1 : Installing & Setting Up The Tools

In this program we will be using **RISC-V GNU Compiler Toolchain** to compile our c programs into risc v instructions. 
Then we will be using **Iverilog** to compile & simulate our verilog files. 
We will be using **GTKwave** to view the relevant waveforms obtained from verilog simulation.
Also we will be using **Yosys** to synthesis our RTL.

## Steps to install Yosys

Assuming the `git` , `make` & `gcc` are already installed in your Ubuntu 20.04


```
$ git clone https://github.com/YosysHQ/yosys.git
$ cd yosys
$ sudo apt-get install build-essential clang bison flex \
    libreadline-dev gawk tcl-dev libffi-dev git \
    graphviz xdot pkg-config python3 libboost-system-dev \
    libboost-python-dev libboost-filesystem-dev zlib1g-dev
$ make config-gcc
$ make 
$ sudo make install
```


