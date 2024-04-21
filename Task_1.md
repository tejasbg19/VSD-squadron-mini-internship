# Task-1 : Installing & Setting Up The Tools

In this program we will be using **RISC-V GNU Compiler Toolchain** to compile our c programs into risc v instructions. 
Then we will be using **Iverilog** to compile & simulate our verilog files. 
We will be using **GTKwave** to view the relevant waveforms obtained from verilog simulation.
Also we will be using **Yosys** to synthesis our RTL.

## Steps to install Yosys

Assuming that `git` , `make` & `gcc` are already installed in your Ubuntu 20.04


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


<br>

### Steps to install gcc 

```
$ sudo apt update
$ sudo apt install gcc
```

![tejas-bg-vsd-internship  Running  - Oracle VM VirtualBox 4_20_2024 11_48_18 PM](https://github.com/tejasbg19/VSD-squadron-mini-internship/assets/163899793/d511cc76-c5a7-41e6-895d-ca528712243b)


you can verify gcc installation as shown below
![tejas-bg-vsd-internship  Running  - Oracle VM VirtualBox 4_20_2024 11_48_33 PM](https://github.com/tejasbg19/VSD-squadron-mini-internship/assets/163899793/c1a47345-545a-4273-a9cd-239e9321a3d1)

<br>


### Steps to install git

```
$ sudo apt update
$ sudo apt install git
```

![Tejas_B_G_vsd_mini_internship  Running  - Oracle VM VirtualBox 4_20_2024 8_34_10 PM](https://github.com/tejasbg19/VSD-squadron-mini-internship/assets/163899793/0335cf76-3980-4854-9be8-cf9e56c98de0)

<br>
<br>
<br>


## Steps to install Iverilog


```
$ sudo apt-get update
$ sudo apt-get -y install iverilog
```

![tejas-bg-vsd-internship  Running  - Oracle VM VirtualBox 4_21_2024 5_24_30 PM](https://github.com/tejasbg19/VSD-squadron-mini-internship/assets/163899793/9de7728a-8fe7-4c14-b5e7-2c77f02891cc)


The installation can be verified as shown below

![tejas-bg-vsd-internship  Running  - Oracle VM VirtualBox 4_21_2024 5_26_34 PM](https://github.com/tejasbg19/VSD-squadron-mini-internship/assets/163899793/2b9d8b80-7610-4459-a803-409154fa3734)
<br>
<br>
<br>




## Steps to install gtkwave

```
$ sudo apt update
$ sudo apt install gtkwave
```

The installation can be verified as shown below

![tejas-bg-vsd-internship  Running  - Oracle VM VirtualBox 4_21_2024 5_24_30 PM](https://github.com/tejasbg19/VSD-squadron-mini-internship/assets/163899793/1e61c1bf-b2dc-4e6c-ada7-c56b623853a9)

<br> 
<br>
<br>

## Steps to install RISC-V GNU Compiler Toolchain

We will be installing the tools from the [this github repo](https://github.com/riscv-collab/riscv-gnu-toolchain), you can refer that page if you face any unexpected errors in the process. 

```
$ sudo apt update
$ sudo apt install autoconf automake autotools-dev curl libmpc-dev libmpfr-dev \
   libgmp-dev gawk build-essential bison flex texinfo gperf libtool patchutils bc zlib1g-dev \ 
   libexpat-dev

# Even though it is adviced in the toolchain repo to not use `--recursive` I have used it as the tools were not installed properly without it.

$ git clone --recursive https://github.com/riscv-collab/riscv-gnu-toolchain  
$ cd riscv-gnu-toolchain

# Intead of `/home/tejas` give the absolute path of the directory where you want to install the tools

$ ./configure --prefix=/home/tejas/riscv
$ sudo make linux
$ echo 'export PATH=/home/tejas/riscv/bin:$PATH' >> ~/.bashrc
$ source ~/.bashrc
```



