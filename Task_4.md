
# Task-3 : Verifying the outputs of gcc & riscv64 compiled program outputs & debugging them.


## Observing The Outputof riscv compilation:


When we compiled our `sum1ton.c` in normal gcc compiler, we used to generate a `a.out` file. Executing that file using the command `./a.out` would give us output of our `c program`. But viewing the output riscv64 compiled program is not so easy. We need a seperate tool called `spike` and in the below instructions we will get to know how to call spike to observe the output of riscv64 compiled file. 


```
$ riscv64-unknown-elf-gcc -Ofast -mabi=lp64 -march=rv64imac -o program_name.o program_name.c
$ spike pk program_name.o
```
Below we can see the outputs of normal gcc & spike. As we can see they are equal as they are supposed to be .


|  GCC Output             |  riscv64 Output  |
|:-------------------------:|:-------------------------:|
| ![trial 20  Running  - Oracle VM VirtualBox 5_3_2024 7_59_15 PM](https://github.com/tejasbg19/VSD-squadron-mini-internship/assets/163899793/35fc49e2-dbef-4140-a868-e729b8ec12a5) |  ![trial 20  Running  - Oracle VM VirtualBox 5_3_2024 7_59_55 PM](https://github.com/tejasbg19/VSD-squadron-mini-internship/assets/163899793/27cb2bd6-f8c6-4f0a-9282-3ff428be3012)
 |



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


To instruct the spike to exceute the instructions until `main()` we can give the command 


```
(spike) until pc 0 address_of_your_first_main()_instruction
# in my case it is 
(spike) until pc 0 10104
```
![trial 20  Running  - Oracle VM VirtualBox 5_3_2024 8_08_36 PM](https://github.com/tejasbg19/VSD-squadron-mini-internship/assets/163899793/9f62de1b-ad6f-4a80-998f-b3fbb90fed66)





`a0` register 
![trial 20  Running  - Oracle VM VirtualBox 5_3_2024 9_18_26 PM](https://github.com/tejasbg19/VSD-squadron-mini-internship/assets/163899793/f0911bb3-0c9e-4a62-ac4b-e4a8c3903bd5)


