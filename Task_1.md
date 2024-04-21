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
$ sudo apt-get install python3-pyelftools
```

The output of above commands

![tejas-bg-vsd-internship  Running  - Oracle VM VirtualBox 4_21_2024 3_28_49 PM](https://github.com/tejasbg19/VSD-squadron-mini-internship/assets/163899793/e7f48a8d-7370-424f-81b2-667ec5b66648)


![tejas-bg-vsd-internship  Running  - Oracle VM VirtualBox 4_21_2024 3_29_16 PM](https://github.com/tejasbg19/VSD-squadron-mini-internship/assets/163899793/94884629-533a-470a-ac5c-af8ea534e21f)


![tejas-bg-vsd-internship  Running  - Oracle VM VirtualBox 4_21_2024 5_05_19 PM](https://github.com/tejasbg19/VSD-squadron-mini-internship/assets/163899793/cb3ac9de-3399-441e-999c-cc416ba2ab33)


![tejas-bg-vsd-internship  Running  - Oracle VM VirtualBox 4_21_2024 5_05_19 PM](https://github.com/tejasbg19/VSD-squadron-mini-internship/assets/163899793/e9ba9e52-1cba-474a-b79b-2b7f7f187cf5)


![tejas-bg-vsd-internship  Running  - Oracle VM VirtualBox 4_21_2024 5_05_19 PM](https://github.com/tejasbg19/VSD-squadron-mini-internship/assets/163899793/a6125c9a-06f4-4285-b04f-ef9cda00d4ec)

With this, the installation of tools is complete, To test the RISC-V GNU Compiler Toolchain, we will write a c program `hello.c` & compile it. Also if you donot have any text editor, follow the below commands to install `vim` text editor

```
$ sudo apt update
$ sudo apt install vim
```

Once `vim` is installed, navigate to your desired directory an create `hello.c` as shown below
```
$ cd Documents
$ vim hello.c
```
![tejas-bg-vsd-internship  Running  - Oracle VM VirtualBox 4_21_2024 6_48_34 PM](https://github.com/tejasbg19/VSD-squadron-mini-internship/assets/163899793/3918e88b-59fa-4cdb-b2b4-8d4991f2fa54)
<br><br>
inside the `vim` press `i` to start inserting text and type the below code
```
#include <stdio.h>

int main() {
    printf("Hello, World!\n");
    return 0;
}
```
![tejas-bg-vsd-internship  Running  - Oracle VM VirtualBox 4_21_2024 6_48_44 PM](https://github.com/tejasbg19/VSD-squadron-mini-internship/assets/163899793/76dcedfe-e8ce-4030-a664-dcbfc8c56e30)
<br> <br>
After typing is done, press `Esc` to come back to command mode. To save and exit the file type `:wq` & press `Enter`,if you donot want to save your work, you can simply exit using `:q!`. After this compile & simulate the file

```
$ riscv64-unknown-elf-gcc -o hello hello.c
$ spike pk hello
```

![Screenshot 4_21_2024 6_53_40 PM](https://github.com/tejasbg19/VSD-squadron-mini-internship/assets/163899793/cc50abc7-4e37-4a6a-bac1-53433acf1333)
![Screenshot 4_21_2024 6_53_40 PM](https://github.com/tejasbg19/VSD-squadron-mini-internship/assets/163899793/bf276d24-90a2-41ae-80b7-5475e45433b0)

We are facing an unexpected error, system couldn't find spike, so let us install it seperatly.
<br>



### Installiong Spike, thus fixing error

Assuming **Device Tree Compiler** is already installed, if not refer just run `$ sudo apt-get install device-tree-compiler`.

![tejas-bg-vsd-internship  Running  - Oracle VM VirtualBox 4_21_2024 7_41_50 PM](https://github.com/tejasbg19/VSD-squadron-mini-internship/assets/163899793/5b09ccfb-0fcc-4908-8776-2a9b4556c030)



```
$ git clone https://github.com/riscv/riscv-isa-sim.git
$ cd riscv-isa-sim
$ mkdir build
$ cd build

#change `home/tejas/riscv` to your prefered directory

$ ../configure --prefix=/home/tejas/riscv
$ make
$ make install
$ echo 'export PATH=/path/to/install/bin:$PATH' >> ~/.bashrc
$ source ~/.bashrc
```


![tejas-bg-vsd-internship  Running  - Oracle VM VirtualBox 4_21_2024 7_41_24 PM](https://github.com/tejasbg19/VSD-squadron-mini-internship/assets/163899793/0cd531bd-1014-47e1-b86b-bfc782d58772)





