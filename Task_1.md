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

You can verify the installation of yosys as shown below

![openlane  Running  - Oracle VM VirtualBox 4_20_2024 11_29_35 PM](https://github.com/tejasbg19/VSD-squadron-mini-internship/assets/163899793/7a5c36b0-7832-4c81-bbd8-bda9f40f44bb)


### Steps to install gcc 


```
$ sudo apt update
$ sudo apt install gcc
```

![tejas-bg-vsd-internship  Running  - Oracle VM VirtualBox 4_20_2024 11_48_18 PM](https://github.com/tejasbg19/VSD-squadron-mini-internship/assets/163899793/d511cc76-c5a7-41e6-895d-ca528712243b)


### Steps to install git

```
$ sudo apt update
$ sudo apt install git
```

![Tejas_B_G_vsd_mini_internship  Running  - Oracle VM VirtualBox 4_20_2024 8_34_10 PM](https://github.com/tejasbg19/VSD-squadron-mini-internship/assets/163899793/0335cf76-3980-4854-9be8-cf9e56c98de0)




