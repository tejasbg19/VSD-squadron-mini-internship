
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
| ![trial 20  Running  - Oracle VM VirtualBox 5_3_2024 7_59_15 PM](https://github.com/tejasbg19/VSD-squadron-mini-internship/assets/163899793/35fc49e2-dbef-4140-a868-e729b8ec12a5)
 |  ![trial 20  Running  - Oracle VM VirtualBox 5_3_2024 8_08_28 PM](https://github.com/tejasbg19/VSD-squadron-mini-internship/assets/163899793/7c81f364-3d2e-4c64-bc4c-1e51db12f25f) |



## Debugging Using Spike:

To open spike in debug mode, use the below code.

```
$ spike -d pk program_name.o
```

image 



Now we know how to obtain the assembly instructions of our `object file` 
(using `$ riscv64-unknown-elf-objdump -d program_name.o | less`). keeping the address of `main()` as a reference from the above code, let us debug our program instruction register by register in spike. 

image of obj file


To instruct the spike to exceute the instructions until `main()` we can give the command 


```
(spike) until pc 0 address_of_your_first_main()_instruction
# in my case it is 
(spike) until pc 0 10104
```
