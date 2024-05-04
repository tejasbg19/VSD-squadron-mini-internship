
# Task-3: Verifying Outputs of `gcc` and `riscv64` Compiled Programs, Debugging `rv64imac` Compiled Assembly Object File Instruction by Instruction


## Observing The Outputof riscv compilation:


When we compiled our `sum1ton.c` in normal gcc compiler, we used to generate a `a.out` file. Executing that file using the command `./a.out` would give us output of our `c program`. But viewing the output riscv64 compiled program is not so easy. We need a seperate tool called `spike` and in the below instructions we will get to know how to call spike to observe the output of riscv64 compiled file. 


```
$ riscv64-unknown-elf-gcc -Ofast -mabi=lp64 -march=rv64imac -o program_name.o program_name.c
$ spike pk program_name.o
```
Below we can see the outputs of normal gcc & spike. As we can see they are equal as they are supposed to be .


|  GCC Output             |  riscv64 Output  |
|:-------------------------:|:-------------------------:|
| ![trial 20  Running  - Oracle VM VirtualBox 5_3_2024 7_59_15 PM](https://github.com/tejasbg19/VSD-squadron-mini-internship/assets/163899793/35fc49e2-dbef-4140-a868-e729b8ec12a5) |  ![trial 20  Running  - Oracle VM VirtualBox 5_3_2024 7_59_55 PM](https://github.com/tejasbg19/VSD-squadron-mini-internship/assets/163899793/27cb2bd6-f8c6-4f0a-9282-3ff428be3012)|



## Debugging Using Spike:

To open spike in debug mode, use the below code.

```
$ spike -d pk program_name.o
```

![trial 20  Running  - Oracle VM VirtualBox 5_3_2024 8_08_28 PM](https://github.com/tejasbg19/VSD-squadron-mini-internship/assets/163899793/04f83cc3-c502-4e62-8af8-dbe375563d26)

 



Now we know how to obtain the assembly instructions of our `object file` 
(using `$ riscv64-unknown-elf-objdump -d program_name.o | less`). keeping the address of `main()` as a reference from the above code, let us debug our program instruction register by register in spike. 


![trial 20  Running  - Oracle VM VirtualBox 5_3_2024 8_07_51 PM](https://github.com/tejasbg19/VSD-squadron-mini-internship/assets/163899793/57c21472-ab4d-46ad-8c46-0de7c6305e7d)



From the above image the riscv instructions present in `main()` are 

```
   10104:       6565                    lui     a0,0x19
   10106:       1141                    addi    sp,sp,-16
   10108:       02400613                li      a2,36
   1010c:       45a1                    li      a1,8
   1010e:       38050513                addi    a0,a0,896 # 19380 <__clzdi2+0x40>
   10112:       e406                    sd      ra,8(sp)
   10114:       3b8000ef                jal     104cc <printf>
   10118:       60a2                    ld      ra,8(sp)
   1011a:       4501                    li      a0,0
   1011c:       0141                    addi    sp,sp,16
   1011e:       8082                    ret
```

## Analysing Each Instruction:


To instruct spike to execute instructions until main(), we command spike to run until the address of the first instruction in our main() function as shown below.


```
(spike) until pc 0 address_of_your_first_main()_instruction
# in my case it is 
(spike) until pc 0 10104
```
![trial 20  Running  - Oracle VM VirtualBox 5_3_2024 8_08_36 PM](https://github.com/tejasbg19/VSD-squadron-mini-internship/assets/163899793/9f62de1b-ad6f-4a80-998f-b3fbb90fed66)

<br>
<br>
 
 ### Instruction - 01


```
c.lui     a0,0x19
```

To know the value stored in `a0` register before the execution of first instruction we use the below command 

```
(spike) reg 0 a0
```

To run the ***1<sup>st</sup>*** instruction, just press `enter`. After running the first instruction, let us check the content of `register a0` again using 

```
(spike) reg 0 a0
```
<br>

|  Value of `reg a0` before the execution of 1<sup>st</sup> instruction   |  Value of `reg a0` after the execution of 1<sup>st</sup> instruction  |
|:-------------------------:|:-------------------------:|
| ![trial 20  Running  - Oracle VM VirtualBox 5_3_2024 9_18_26 PM](https://github.com/tejasbg19/VSD-squadron-mini-internship/assets/163899793/f0911bb3-0c9e-4a62-ac4b-e4a8c3903bd5) | ![image](https://github.com/tejasbg19/VSD-squadron-mini-internship/assets/163899793/8b5bdeb4-1a5b-4a81-9a2a-e3aff931e0a2)|

<br>

- It is also important to observe that value of `reg a0` is `0x0000000000000001` where each of the 16 positions is a 4bit data hence, we can confirm that the program is compiled into `64-bit riscv oject file` as **16*4 = 64**.
- As we can see the content of a0 has been modified as per the instruction `c.lui     a0,0x19` which dictates to load load upper immediate value **(19)<sub>16</sub>** to the upper bits of `register a0`.
- Also the `c.` in my instructions just indicates that the instruction is in  compressed format as I have used **`-march=rv64imac`** target architecture flag while compilation of the program instead of **`Standard Base Interger `** **`rv64i`** ISA.
- "0x19" is a hexadecimal value. The `0x` prefix signifies that the following number is in hexadecimal notation.
- This is a `I-type instruction`.

<br>
<br>

### Instruction - 02


```
 addi    sp,sp,-16
```

The above instruction involves `sp(stack pointer)` so let us check its value before running/executing it, using 

```
(spike) reg 0 sp
```

To execute the ***2<sup>nd</sup>*** instruction again press `enter`. To check the `sp` value of the execution of ***2<sup>nd</sup>*** instruction use,

```
(spike) reg 0 sp
```

<br>

|  Value of `sp` before the execution of 2<sup>nd</sup> instruction   |  Value of `sp` after the execution of 2<sup>nd</sup> instruction  |
|:-------------------------:|:-------------------------:|
| ![trial 20  Running  - Oracle VM VirtualBox 5_3_2024 10_16_32 PM](https://github.com/tejasbg19/VSD-squadron-mini-internship/assets/163899793/eaacb1e6-fd49-4617-9a87-d7f8983daebe) |![RV_D1SK2_L3_spikeSimulationAndDebug mp4 - OneDrive and 19 more pages - Personal - Microsoft​ Edge 5_3_2024 10_39_23 PM](https://github.com/tejasbg19/VSD-squadron-mini-internship/assets/163899793/a48e86e2-31d3-4ba8-add3-6762ebb37f93)|

<br>

- The `sp` previously held the value `3ffffffb50`.
- The instruction `c.addi sp, -16` is a compressed instruction set (rv64c) performs an addition of the immediate value **(-16)<sub>10</sub>** to the `stack pointer (sp)`, which in a nutshell subracts decimal 16 from `stack pointers` current value. 
- **(16)<sub>10</sub> = (10)<sub>16</sub>**, `sp` value before exceution of `c.addi sp, -16` was **3ffffffb50** & we know that **(3ffffffb50 - 10 = 3ffffffb40)<sub>16</sub>**
- This is a `I-type instruction`.

<br>
<br>

### Instruction - 03

```
 li      a2,36
```

The  ***3<sup>rd</sup>*** instruction involves `reg a2`, so to check its value before the execution of ***3<sup>rd</sup>*** instruction use,

```
(spike) reg 0 a2
```
To execute the ***3<sup>rd</sup>*** instruction again press `enter`. Then check the value of `reg a2` using 

```
(spike) reg 0 a2
```

<br>

|  Value of `reg a2` before the execution of 3<sup>rd</sup> instruction   |  Value of `reg a2` after the execution of 3<sup>rd</sup> instruction  |
|:-------------------------:|:-------------------------:|
| ![Editing VSD-squadron-mini-internship_Task_4 md at main · tejasbg19_VSD-squadron-mini-internship and 18 more pages - Personal - Microsoft​ Edge 5_3_2024 10_46_16 PM](https://github.com/tejasbg19/VSD-squadron-mini-internship/assets/163899793/2d23f473-8cad-4dca-a843-a7e46d0508c6)|![trial 20  Running  - Oracle VM VirtualBox 5_3_2024 10_15_21 PM](https://github.com/tejasbg19/VSD-squadron-mini-internship/assets/163899793/9afb6df2-5308-416c-95cc-7c65dc710c62)|

<br>

- The `register a2` stores `0000000000000000` before the exceution of the ***3<sup>rd</sup>*** instruction of `main()`.
- The instruction `li a2, 36` sets the value of register a2 to decimal 36 (0x24 in hexadecimal).
-  `li` stands for `load immidiate`.
-  This is a  `I-type instruction`. 

<br>
<br>

### Instruction - 04

```
li      a1,8
```

The  ***4<sup>th</sup>*** instruction involves `reg a1`, so to check its value before the execution of ***4<sup>th</sup>*** instruction use,

```
(spike) reg 0 a1
```

To execute the ***4<sup>th</sup>*** instruction again press `enter`. Then check the value of `reg a1` using 

```
(spike) reg 0 a1
```

<br>

|  Value of `reg a1` before the execution of ***4<sup>th</sup>*** instruction   |  Value of `reg a1` after the execution of ***4<sup>th</sup>*** instruction |
|:-------------------------:|:-------------------------:|
| ![trial 20  Running  - Oracle VM VirtualBox 5_4_2024 6_06_10 PM](https://github.com/tejasbg19/VSD-squadron-mini-internship/assets/163899793/16bb32dd-8574-4d3e-8bd9-981ebff49ddb)|![trial 20  Running  - Oracle VM VirtualBox 5_4_2024 6_07_03 PM](https://github.com/tejasbg19/VSD-squadron-mini-internship/assets/163899793/2439a5e9-0bbc-4642-b624-d1f46e4db5a5)|

<br>

- The `register a1` stores `0000003ffffffb58` before the execution of the fourth instruction of `main()`.
- The instruction `li a1, 8` sets the value of `register a1` to decimal 8 (0x8 in hexadecimal).
- `li` stands for "load immediate."
- This is an `I-type instruction`.

<br>
<br>

### Instruction - 05

```
 addi    a0,a0,896 
```

The  ***5<sup>th</sup>*** instruction involves `reg a0`, so to check its value before the execution of ***5<sup>th</sup>*** instruction use,

```
(spike) reg 0 a0
```

To execute the ***5<sup>th</sup>*** instruction again press `enter`. Then check the value of `reg a0` using 

```
(spike) reg 0 a0
```

<br>

|  Value of `reg a0` before the execution of ***5<sup>th</sup>*** instruction   |  Value of `reg a0` after the execution of ***5<sup>th</sup>*** instruction |
|:-------------------------:|:-------------------------:|
|![Photos 5_4_2024 6_16_33 PM](https://github.com/tejasbg19/VSD-squadron-mini-internship/assets/163899793/822996ec-4113-499e-840b-d5c05582c66f)|![trial 20  Running  - Oracle VM VirtualBox 5_4_2024 6_17_19 PM](https://github.com/tejasbg19/VSD-squadron-mini-internship/assets/163899793/41511a78-ee66-4466-8833-6bfb670c8dfd)|

<br>

- The `register a0` stores `0000000000019000` before the execution of the fifth instruction of `main()`.
- The instruction `addi a0, a0, 896` adds the immediate value decimal value 896 to the current value of `register a0`.
-  **0000000000019000 + 390 = 0000000000019390** in hexadecimal.
- This is an `I-type instruction`.

<br>
<br>

### Instruction - 06

```
 sd      ra,8(sp)
```

The  ***6<sup>th</sup>*** instruction involves involves storing the value of the return address `register ra` at the memory address calculated as the sum of the stack pointer `sp` and an offset of `8` that is (sp + 8).


To check the value of `register ra` & `sp` before the execution of this instruction, use:

```
(spike) reg 0 ra
(spike) reg 0 sp
```
Press `enter` again to execute the instruction. 

<br>

|  Value of `reg ra` & `sp` |  Execution of the instruction |
|:-------------------------:|:-------------------------:|
|![trial 20  Running  - Oracle VM VirtualBox 5_4_2024 6_31_47 PM](https://github.com/tejasbg19/VSD-squadron-mini-internship/assets/163899793/e80ea9cc-66be-4b6b-a7f8-1324bdc949ac)|![Editing VSD-squadron-mini-internship_Task_4 md at main · tejasbg19_VSD-squadron-mini-internship and 17 more pages - Personal - Microsoft​ Edge 5_4_2024 6_56_29 PM](https://github.com/tejasbg19/VSD-squadron-mini-internship/assets/163899793/b2a166c5-613c-4793-83e7-028389aedd05)|

<br>





<br> 

To **QUIT** `spike`, simply press `q` followed by `enter`. If you happen to miss noting down the value of a `register` or `sp` before running an instruction, you can always quit `spike` and rerun it in debug mode. Instead of providing the first instruction address for `main()`, you can input the address one step earlier than the instruction whose register value you wish to examine before executing that specific instruction.

![trial 20  Running  - Oracle VM VirtualBox 5_3_2024 10_15_21 PM](https://github.com/tejasbg19/VSD-squadron-mini-internship/assets/163899793/5e879eb4-8321-4e81-aecc-83eb48487b20)


<br>


