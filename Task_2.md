# Task-2 : Identify instruction type and exact 32-bit instruction code in the instruction type format. Upload the 32-bit pattern on Github 

And the given instructions are: 
<br>  add r6,r2,r1
<br>  sub r7,r1,r2
<br>  and r8,r1,r3
<br>  or r9,r2,r5
<br>  xor r10,r1,r4
<br>  slt r11,r2,r4
<br>  addi r12,r4,5
<br>  sw r3,r1,2
<br>  lw r13,r1,2
<br>  beq r0,r0,15
<br>  bne r0,r1,20
<br>  sll r15,r1,r2(2)
<br>  srl r16,r14,r2(2)
<br> <br>
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



## The Classes:

We can classify the base integer ISA into 6 types:


### 1.  **R-Type (Register Type):** 

- R-type instructions operate on the data within the source registers, and typicall arithmeic, logical & shifting operations can be performed in this formate.
- **syntax:**


| 31-25 | 24-20 | 19-15 | 14-12 | 11-7 | 6-0 |    
|:-----:|:-----:|:-----:|:-----:|:----:|:---:|
| funct7|  rs2  |  rs1  | funct3|  rd  |opcode|

-eg: add rd, rs1, rs2 (addition operation)


<br>

### 2.  **I-Type (Immediate Type):** 

- I-type instructions operate on immediate values in their operation, and typicall arithmeic & load operations can use this formate.
- **syntax:**


| 31-20 | 19-15 | 14-12 | 11-7 | 6-0 |  
|:----------:|:-----:|:-----:|:----:|:---:|
| imm [11:0] |  rs1  | funct3|  rd  |opcode|

-eg: add rd, rs1, rs2 (addition operation)             

### 3.  **S-Type (Store Type):** 

- S-type of instructions are used to store data froma register into memory.
- **syntax:**


| 31-25 | 24-20 | 19-15 | 14-12 | 11-7 | 6-0 |    
|:-----:|:-----:|:-----:|:-----:|:----:|:---:|
| imm[11:5]|  rs2  |  rs1  | funct3|  imm[4:0]  |opcode|


-eg: add rd, rs1, rs2 (addition operation)


<br>

### 4.  **B-Type (Branch Type):** 

- This is like a loop in c, which iterates based on a condition.
- **syntax:**


| 31-25 | 24-20 | 19-15 | 14-12 | 11-7 | 6-0 |    
|:-----:|:-----:|:-----:|:-----:|:----:|:---:|
| imm[12] imm[10:5]|  rs2  |  rs1  | funct3|  imm[4:1] [11]  |opcode|


-eg: beq rs1, rs2, offset (branch equal)


<br>


### 5.  **U-Type (Upper Immediate Type):** 

- This type of instruction is used to LOAD large constants/values into a register.
- **syntax:**


| 31-12 | 11-7 | 6-0 |    
|:-----:|:-----:|:-----:|
|  imm[31:12]|   rd |opcode|


-eg: lui rd, imm (load upper immediate)

<br>


### 6.  **J-Type (Jump Type):** 

- J-Type instructions are used for unconditional jumping to a target address.
- **syntax:**


| 31-25 | 24-20 | 19-12 | 11-7 | 6-0 |    
|:-----:|:-----:|:--------:|:----:|:---:|
| imm[20]|  imm[10:1]  |  lmm11 | imm[19:12]|  rd  |opcode|

-eg: jal rd, offset (jump and link)
<br>

It is also important to note that the ***RISC-V ISA keeps the source (rs1 and rs2) and destination (rd) registers at the same position
in all formats*** to simplify decoding. Except for the 5-bit immediates used in CSR (control & status register) instructions.

<br> <br>
Syntax for all instructions at one place.
![Screenshot (445)](https://github.com/tejasbg19/VSD-squadron-mini-internship/assets/163899793/1fd56bbd-f8a0-48c0-83f4-d0c5a86ebaef)
Source: The PDF volume1 Unprivilaged riscv ISA.


<br>

## The Opcodes for operations:

The below opcode table gives us the corresponting binary code for a specific operation. And can be found on official [**riscv website**](https://riscv.org/technical/specifications/) in volume1, unprivilaged PDF.

![Screenshot (444)](https://github.com/tejasbg19/VSD-squadron-mini-internship/assets/163899793/38908e80-3139-483c-bd7f-09bc8cc29317)
Source: The PDF volume1 Unprivilaged riscv ISA.

<br>

# The Task: identifying the instruction types.


1.  add r6,r2,r1 :
   - The above instruction is a **`R-type`** base instruction formate as the registers *r1* & *r2* which contain the data that are being passed as operand for the **`operation of addition`**. while the result will be stored in destination register *r6*.
   - | 31-25 | 24-20 | 19-15 | 14-12 | 11-7 | 6-0 |
      |:-----:|:-----:|:-----:|:-----:|:----:|:---:|
     | funct7|  rs2  |  rs1  | funct3|  rd  |opcode|
     | 0000000| 00001| 00010| 000 |00110| 0110011|

   -  RV32I instruction is `0000000 00001 00010 000 00110 0110011
`
    


2.  sub r7,r1,r2 :
    - The above instruction is a **`R-type`** base instruction formate as the registers *r1* & *r2* which contain the data that will be passed as operand for the **`operation of subtraction`**. while the result will be stored in destination register *r7*.
    -  | 31-25 | 24-20 | 19-15 | 14-12 | 11-7 | 6-0 |
       |:-----:|:-----:|:-----:|:-----:|:----:|:---:|
       | funct7|  rs2 |  rs1  | funct3|  rd  |opcode|
       |0100000| 00001| 00010| 000| 00111| 0110011|
    -  RV32I instruction is `0100000 00001 00010 000 00111 0110011`
   


3.  and r8,r1,r3 :
   - The above instruction is a **`R-type`** base instruction formate as the registers *r1* & *r3* which contain the data that will be passed as operand for **`Bitwise Logical AND operation`**. while the result will be stored in destination register *r8*.
   -  | 31-25 | 24-20 | 19-15 | 14-12 | 11-7 | 6-0 |
      |:-----:|:-----:|:-----:|:-----:|:----:|:---:|
      | funct7|  rs2 |  rs1  | funct3|  rd  |opcode|
      |0000000 |00001 |00011 |111| 01000| 0110011|

   -  RV32I instruction is `0000000 00001 00011 111 01000 0110011`

4.  or r9,r2,r5 :
    - The above instruction is a **`R-type`** base instruction formate as the registers *r2* & *r5* which contain the data that will be passed as operand for **`Bitwise Logical OR operation`**. while the result will be stored in destination register *r9*.
    - | 31-25 | 24-20 | 19-15 | 14-12 | 11-7 | 6-0 |
      |:-----:|:-----:|:-----:|:-----:|:----:|:---:|
      | funct7|  rs2 |  rs1  | funct3|  rd  |opcode|
      |0000000| 00101|00010 | 110 | 01001 |0110011 |

    - RV32I instruction is `0000000 00101 00010 110 01001 0110011`

5.  xor r10,r1,r4 :
    - The above instruction is a **`R-type`** base instruction formate as the registers *r1* & *r4* which contain the data that will be passed as operand for **`Bitwise Logical OR operation`**. while the result will be stored in destination register *r10*.
    - | 31-25 | 24-20 | 19-15 | 14-12 | 11-7 | 6-0 |
      |:-----:|:-----:|:-----:|:-----:|:----:|:---:|
      | funct7|  rs2 |  rs1  | funct3|  rd  |opcode|
      | 0000000| 00100| 00001| 100| 01010| 0110011|

    -  RV32I instruction is `0000000 00100 00001 100 01010 0110011`


6.  slt r11,r2,r4 :
   - The above instruction is a **`R-type`** base instruction formate as the registers *r2* & *r4* which contain the data that will be passed as operand for **`Set less than (Magnitude Comparision)`**. while the result will be stored in destination register *r11*. If `r2<r4 implies r11=1 else r11=0 `

   - | 31-25 | 24-20 | 19-15 | 14-12 | 11-7 | 6-0 |
      |:-----:|:-----:|:-----:|:-----:|:----:|:---:|
      | funct7|  rs2 |  rs1  | funct3|  rd  |opcode|
      |0000000| 00100| 00010| 010| 01011 |0110011 |
   - RV32I instruction is `0000000 00100 00010 010 01011 0110011 `

7.  addi r12,r4,5 :
   -  The above instruction is a **`I-type`** base instruction formate as a immediate value **`binary 5 will be added to r4`** and the result will be stored in destination register *r12*. 
   - | 31-20 | 19-15 | 14-12 | 11-7 | 6-0 |  
     |:----------:|:-----:|:-----:|:----:|:---:|
     | imm [11:0] |  rs1  | funct3|  rd  |opcode|
     |000000000101  |00100 |000 | 01100|0010011|

   - RV32I instruction is `000000000101 00100 000 01100 0010011`


8.  sw r3,r1,2 :
   - The above instruction is a **`S-type`** base instruction formate and the opcode `store word` specifies to **`move/save the 32-bit content of source register r3 to the memory location whose base address = r1 with an offset 2`**.
   - | 31-25 | 24-20 | 19-15 | 14-12 | 11-7 | 6-0 |    
    |:-----:|:-----:|:-----:|:-----:|:----:|:---:|
    | imm[11:5]|  rs2  |  rs1  | funct3|  imm[4:0]  |opcode|
     |0000000 |00001 |00011 |010 |00010 |0100011|    
   -  RV32I instruction is `0000000 00001 00011 010 00010 0100011`


9.  lw r13,r1,2 :
     - The above instruction is a **`S-type`** base instruction formate and the opcode `load word` specifies to **`load the 32-bit content of the memory location whose base address = r1 + offset 2 into the destination register r13`**.
     - | 31-25 20 | 19-15 | 14-12 | 11-7 | 6-0 |    
      |:-----:|:-----:|:-----:|:-----:|:-------:
      | imm[11:0]  |  rs1  | funct3|  imm[4:0]  |opcode|
       |000000000010 | 00001 |010| 01101| 0000011|     
     -  RV32I instruction is `000000000010 00001 010 01101 0000011`

     


10.  beq  r0,r0,15 :
     -  The above instruction is a **`B-type`** base instruction formate and the opcode `branch if equal` specifies to **`check if source1 register r0 is equal to source2 register r0 then branch to instructions at memory location 15 instructions ahead of current instruction`**.
     - | 31-25 | 24-20 | 19-15 | 14-12 | 11-7 | 6-0 |    
       |:-----:|:-----:|:-----:|:-----:|:----:|:---:|
      | imm[12] imm[10:5]|  rs2  |  rs1  | funct3|  imm[4:1] [11]  |opcode|
      | 0000000 000 |00000 |00000 |000 | 1111 |1100011|

     -  RV32I instruction is `00000 000 00000 00000 000 1111 1100011`


13. bne r0,r1,20 :
-  The above instruction is a **`B-type`** base instruction formate and the opcode `branch if equal` specifies to **`check if source1 register r0 is not equal to source2 register r1 then branch to instructions at memory location 20 instructions ahead of current instruction.`**.
- | 31-25 | 24-20 | 19-15 | 14-12 | 11-7 | 6-0 |    
   |:-----:|:-----:|:-----:|:-----:|:----:|:---:|
  | imm[12] imm[10:5]|  rs2  |  rs1  | funct3|  imm[4:1] [11]  |opcode|
   |0000000 00001 |00000 |00001 |001 |0100 |1100011|
-  RV32I instruction is `0000000 00001 00000 00001 001 0100 1100011`



15.  sll r15,r1,r2(2) :
     - The above given instruction is a **`Logical Left Shift`** operator and uses register, hence a **R-type**, where the contentents of source1 register r1 is shifted by content of  `r2*2`. And the result is stored in destination register r15.
     - | 31-25 | 24-20 | 19-15 | 14-12 | 11-7 | 6-0 |    
       |:-----:|:-----:|:-----:|:-----:|:----:|:---:|
        | funct7|  rs2  |  rs1  | funct3|  rd  |opcode|
        |0000000 |00010 |00001 |001 |01111 |0110011|
     -  RV32I instruction is `0000000 00100 00001 001 01111 0110011`

    

17. srl r16,r14,r2(2) :
    -  The above given instruction is a **`Logical Right Shift`** operator and uses register, hence a **R-type**, where the contentents of source1 register r14 is shifted by content of  `r2*2`. And the result is stored in destination register r16.

    - | 31-25 | 24-20 | 19-15 | 14-12 | 11-7 | 6-0 |    
       |:-----:|:-----:|:-----:|:-----:|:----:|:---:|
        | funct7|  rs2  |  rs1  | funct3|  rd  |opcode|
        |0000000 |00010 |01110 |101 |01111 |0110011|
    -  RV32I instruction is `0000000 00010 01110 101 01111 0110011`
