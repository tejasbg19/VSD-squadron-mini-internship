# Task-1 : Installing & Setting Up The Tools

In this program we will be using **RISC-V GNU Compiler Toolchain** to compile our c programs into risc v instructions. 
Then we will be using **Iverilog** to compile & simulate our verilog files. 
We will be using **GTKwave** to view the relevant waveforms obtained from verilog simulation.
Also we will be using **Yosys** to synthesis our RTL.

## Steps to install Yosys

Assuming that `git` , `make` & `gcc` are already installed in your Ubuntu 20.04


```
$ sudo apt update
$ sudo apt install yosys
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

![tejas-bg-vsd-internship  Running  - Oracle VM VirtualBox 4_21_2024 5_24_30 PM](https://github.com/tejasbg19/VSD-squadron-mini-internship/assets/163899793/1e61c1bf-b2dc-4e6c-ada7-c56b623853a9)


The installation can be verified as shown below
![tejas-bg-vsd-internship  Running  - Oracle VM VirtualBox 4_22_2024 10_17_50 PM](https://github.com/tejasbg19/VSD-squadron-mini-internship/assets/163899793/a442363c-21db-4535-a462-064f1deb9050)


<br> 
<br>
<br>

## Steps to install RISC-V GNU Compiler Toolchain

We will be installing the tools from the [this github repo](https://github.com/riscv-collab/riscv-gnu-toolchain), you can refer that page if you face any unexpected errors in the process. 

```
# Prerequisites before we clone
$ sudo apt update
$ sudo apt install autoconf automake autotools-dev curl libmpc-dev libmpfr-dev \
   libgmp-dev gawk build-essential bison flex texinfo gperf libtool patchutils bc zlib1g-dev \ 
   libexpat-dev
$ sudo apt-get install python3-pyelftools


# Even though it is adviced in the toolchain repo to not use `--recursive` I have used it as the tools were not installed properly without it.
$ git clone --recurse-submodules https://github.com/riscv/riscv-gnu-toolchain  
$ cd riscv-gnu-toolchain
$ export RISCV=/home/tejas/Desktop/internship/riscv
# Intead of `/home/tejas/Desktop/internship/riscv` give the absolute path of the directory where you want to install the tools


# Configuring 32-bit tools
$ ./configure --prefix=$RISCV --with-arch=rv32imac --with-abi=ilp32
$ make -j$(nproc)
$ make install
# Above code only sets up riscv32-unknown-elf but not riscv32-unknown-linux-gnu so follow below code to set it up
$ make clean
$ ./configure --prefix=/opt/riscv --with-arch=rv32gc --with-abi=ilp32d
$ make linux


# Configuring 64-bits tools
$ make clean
$ ./configure --prefix=$RISCV --with-arch=rv64imac --with-abi=lp64
$ make -j$(nproc)
$ make install
# If above 64-bit command only creats riscv-unknown-elf but not riscv64-unknown-linux-gnu follow below commands to set it up
$ make clean
$ ./configure --prefix=$RISCV
$ make linux

# To universally access the tools from anywhere
$ echo 'export PATH=/home/tejas/riscv/bin:$PATH' >> ~/.bashrc
$ source ~/.bashrc
```

The output of above commands

![tejas-bg-vsd-internship  Running  - Oracle VM VirtualBox 4_21_2024 3_28_49 PM](https://github.com/tejasbg19/VSD-squadron-mini-internship/assets/163899793/e7f48a8d-7370-424f-81b2-667ec5b66648)


![tejas-bg-vsd-internship  Running  - Oracle VM VirtualBox 4_21_2024 3_29_16 PM](https://github.com/tejasbg19/VSD-squadron-mini-internship/assets/163899793/94884629-533a-470a-ac5c-af8ea534e21f)


![tejas-bg-vsd-internship  Running  - Oracle VM VirtualBox 4_21_2024 5_05_19 PM](https://github.com/tejasbg19/VSD-squadron-mini-internship/assets/163899793/cb3ac9de-3399-441e-999c-cc416ba2ab33)


![tejas-bg-vsd-internship  Running  - Oracle VM VirtualBox 4_21_2024 5_05_19 PM](https://github.com/tejasbg19/VSD-squadron-mini-internship/assets/163899793/e9ba9e52-1cba-474a-b79b-2b7f7f187cf5)


![tejas-bg-vsd-internship  Running  - Oracle VM VirtualBox 4_21_2024 5_05_19 PM](https://github.com/tejasbg19/VSD-squadron-mini-internship/assets/163899793/a6125c9a-06f4-4285-b04f-ef9cda00d4ec)

With this, the installation of tools is complete, To test the RISC-V GNU Compiler Toolchain, we will write a c program `hello.c` & compile it. Also if you donot have any text editor, follow the below commands to install `vim` text editor


## Installing vim text editor

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


We are facing an unexpected error, system couldn't find spike, so let us install it seperatly.
<br>



### Installing Spike, thus fixing error

Assuming **Device Tree Compiler** is already installed, if not just run `$ sudo apt-get install device-tree-compiler`.


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


![tejas-bg-vsd-internship  Running  - Oracle VM VirtualBox 4_21_2024 8_58_32 PM](https://github.com/tejasbg19/VSD-squadron-mini-internship/assets/163899793/91e4af05-6dc4-4404-b9d5-1b83affbe869)
<br> <br>

After this we expect **`spike`** to work properly, let us recomplie our **`hello.c`** & rerun **`spike`**

![tejas-bg-vsd-internship  Running  - Oracle VM VirtualBox 4_21_2024 9_32_32 PM](https://github.com/tejasbg19/VSD-squadron-mini-internship/assets/163899793/d24928aa-031a-4e17-a25c-ef4a1a79e7cf)

<br>


As we can see even though the compiler is running sucessfully, & even tough **`spike`** has been sucessfull installed, we are facing an unexpected error. **`spike`** is unable to locate **`pk (proxy kernal)`**. I tried to search for **`pk`** in **`usr/bin`** , **`/home/tejas/riscv/riscv64-unknown-elf/bin`** using  **`$ ls <absolute path>/pk`** but was unable to find it, so I decided to download & install it seperatly.



### Installing pk (proxy kernal), to fix pk error

```
$ cd riscv-gnu-toolchain
$ git clone https://github.com/riscv/riscv-pk
$ cd riscv-pk
$ mkdir build
$ cd build
$ ../configure --prefix=/home/tejas/riscv --host=riscv64-unknown-elf --with-arch=rv64gc_zifencei
$ make
$ make install
```

![tejas-bg-vsd-internship  Running  - Oracle VM VirtualBox 4_21_2024 10_46_33 PM](https://github.com/tejasbg19/VSD-squadron-mini-internship/assets/163899793/d12738a0-845f-4a1a-9bd1-e01812e14754)


![Editing VSD-squadron-mini-internship_Task_1 md at main · tejasbg19_VSD-squadron-mini-internship - Google Chrome 4_21_2024 10_48_15 PM](https://github.com/tejasbg19/VSD-squadron-mini-internship/assets/163899793/47eaec6e-a386-4a73-9ec4-44ea85f41aed)


![tejas-bg-vsd-internship  Running  - Oracle VM VirtualBox 4_21_2024 11_04_39 PM](https://github.com/tejasbg19/VSD-squadron-mini-internship/assets/163899793/66444b12-9295-47e1-ad25-08039bc5e009)


![Editing VSD-squadron-mini-internship_Task_1 md at main · tejasbg19_VSD-squadron-mini-internship - Google Chrome 4_21_2024 11_10_33 PM](https://github.com/tejasbg19/VSD-squadron-mini-internship/assets/163899793/38b14022-e996-46b3-9dda-cafaafb9354f)


![tejas-bg-vsd-internship  Running  - Oracle VM VirtualBox 4_21_2024 11_11_15 PM](https://github.com/tejasbg19/VSD-squadron-mini-internship/assets/163899793/6582451c-6687-498f-8c4e-2d20e0955e00)

<br>


As we can see, we are facing an error while **`make`**, & this is due to mismatched-floating point, let us clean `built` directory once using **`$ make clean`** & try to configure once again using the code mentioned in the above bash block as shown below.
<br>

![tejas-bg-vsd-internship  Running  - Oracle VM VirtualBox 4_21_2024 11_58_01 PM](https://github.com/tejasbg19/VSD-squadron-mini-internship/assets/163899793/11405a04-967f-4342-a75d-eaedb5b01d04)
<br> <br>


As we can see, we have sucessfully configured the file, let us run **`$ make`** command as shown below.
![tejas-bg-vsd-internship  Running  - Oracle VM VirtualBox 4_21_2024 11_59_22 PM](https://github.com/tejasbg19/VSD-squadron-mini-internship/assets/163899793/ee4d086e-9d79-4aa9-8e5a-fdd2db60b5cd)

<br>

![Editing VSD-squadron-mini-internship_Task_1 md at main · tejasbg19_VSD-squadron-mini-internship - Google Chrome 4_22_2024 12_02_51 AM](https://github.com/tejasbg19/VSD-squadron-mini-internship/assets/163899793/49b0e338-010f-47cb-861a-8085422a718a)


As we can see from the above image, **`$ make`** was sucessfully executed, & even **`$ sudo make install`** was successful. Hence **`pk`** has been sucessfully built.

<br>

It has come to my attention that **`qemu`** emulator has not been installed with our earlier steps. So let's seperatly install it 


### Installing qemu emulator for 64-bit processors

```
sudo apt install qemu-system-riscv64
# use qemu-system-misc to install for both 32 & 64 bits
```

or

```
git clone https://git.qemu.org/git/qemu.git
cd qemu
./configure --target-list=riscv64-softmmu,riscv32-softmmu
make -j $(nproc)
sudo make install
```


![tejas-bg-vsd-internship  Running  - Oracle VM VirtualBox 4_22_2024 1_55_42 AM](https://github.com/tejasbg19/VSD-squadron-mini-internship/assets/163899793/f788f96f-2ace-4c12-8f14-f455dd4741a9)

The above image also shows how i have verified the installation of qemu.



### Final testing of RISC-V GNU Compiler Toolchain


We have already verified the sucessful functionaning of compiler, now we verify the functanilty of spike & pk as shown below. 
<br>
Assuming you have already created **`hello.c`** as instructed in **`vim text editor`** subsection.

```
$ riscv64-unknown-elf-gcc -o hello hello.c
$ spike pk hello
$ qemu-system-riscv64 -machine virt -nographic -bios default -kernel hello
```

![Editing VSD-squadron-mini-internship_Task_1 md at main · tejasbg19_VSD-squadron-mini-internship - Google Chrome 4_22_2024 12_14_52 AM](https://github.com/tejasbg19/VSD-squadron-mini-internship/assets/163899793/36676871-8abd-425d-9602-9ca03cb7ef9e)

As we can see the output !!!! *Hello world!* we can say all our tools are at last working perfectly ! 




