# Task-2 : Identify instruction type and exact 32-bit instruction code in the instruction type format. Upload the 32-bit pattern on Github 

And the given instructions are in the below image 

![Screenshot_20240417_222748_Chrome](https://github.com/tejasbg19/VSD-squadron-mini-internship/assets/163899793/ece4505e-cee7-47ca-92f1-07aefaca42e3)

To complete this task we first need to understand 32-bit RISC V (**RV32I**) instructions, their types & how they work.

# RV32I :

 RISC V is an open standard instruction set architecture (ISA) based on established **reduced instruction set computer (RISC)** principles. 
 And it has different types of instruction set we will be looking into a **Base Integer Instruction Set**. Based on the level of access and control the instructions provide to the executing program, we can classify the ISAs into **Privilaged** & **Unprivilaged**.
 RV32I as the name suggests deals with the 32-bit instruction set. RV32I utilizes 32 x registers with each register being 32 bits wide to execute instructions , i.e., XLEN=32. Register x0 is hardwired with all bits equal to 0. General purpose registers x1–x31 hold values that various instructions interpret as a collection of Boolean values, or as two’s complement signed binary integers or unsigned binary integers. And this also has one extra unprivilaged register called **PC (program counter)**.
 Since our VSD squadron mini has 32-bit processor, let us know more about it.

 Just like any other instruction set architecture (ISA) riscv too has a syntax. Below image explains the syntax of a RV32I.


![Screenshot (443)](https://github.com/tejasbg19/VSD-squadron-mini-internship/assets/163899793/85644069-e90f-4631-a68d-9a060d697b12)
Source: A screenshot from Wikipedia






