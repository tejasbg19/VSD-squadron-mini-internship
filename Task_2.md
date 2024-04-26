# Task-2 : Identify instruction type and exact 32-bit instruction code in the instruction type format. Upload the 32-bit pattern on Github 

And the given instructions are in the below image 

![Screenshot_20240417_222748_Chrome](https://github.com/tejasbg19/VSD-squadron-mini-internship/assets/163899793/ece4505e-cee7-47ca-92f1-07aefaca42e3)
Source : VSD google form



To complete this task we first need to understand 32-bit RISC V (**RV32I**) instructions, their types & how they work.

# RV32I (Risc V 32-bit Non-Embedded) :

  RISC V is an open standard instruction set architecture (ISA) based on established **reduced instruction set computer (RISC)** principles. 
 And it has different versions of instruction set & we will be looking into a **Base Integer Instruction Set**. Based on the level of access and control the instructions provide to the executing program, we can classify the ISAs into **Privilaged** & **Unprivilaged**. Here we will be dealing with unprivilaged instruction sets.
 <br>
 RV32I as the name suggests deals with the 32-bit instruction set. Since our VSD squadron mini has 32-bit processor, let us know more about it.

 Just like any other instruction set architecture (ISA) riscv instructions can be classified into various types below image explains about one such classificatio based on the core **instruction formats**(that is basically on data type being passed & operation of the instruction).
<br>


![Screenshot (443)](https://github.com/tejasbg19/VSD-squadron-mini-internship/assets/163899793/ca09ea17-a7c5-417a-a610-4953d962e3b7)
Source: A screenshot from Wikipedia


It is alos important to note thta The RISC-V ISA keeps the source (rs1 and rs2) and destination (rd) registers at the same position
in all formats to simplify decoding. Except for the 5-bit immediates used in CSR (control & status register) instructions

## The Classes:

We can classify the base integer ISA into 6 types:

### 1.  **R-Type (Register Type):** 

- R-type instructions operate on the data within the source registers, and typicall arithmeic, logical & shifting operations can be performed in this formate.
- **syntax:**

            | 31 30 | 25 24 | 21 20 | 19 15 | 14 12 | 11  7 |  6  0 |
            |:------:|:------:|:------:|:------:|:------:|:------:|:------:|
            | funct7 |   rs2  |   rs1  | funct3 |    rd  | opcode |        |
            









