# Task-3: Verifying Outputs of `gcc` and `riscv64` Compiled Programs, Debugging `rv64imac` Compiled Assembly Object File Instruction by Instruction


## Observing The Outputof riscv compilation:


When we compiled our `sum1ton.c` in normal gcc compiler, we used to generate a `a.out` file. Executing that file using the command `./a.out` would give us output of our `c program`. But viewing the output riscv64 compiled program is not so easy. We need a seperate tool called `spike` and in the below instructions we will get to know how to call spike to observe the output of riscv64 compiled file. 


```
$ riscv64-unknown-elf-gcc -Ofast -mabi=lp64 -march=rv64imac -o program_name.o program_name.c
$ spike pk program_name.o
```
Below we can see the outputs of normal gcc & spike. As we can see they are equal as they are supposed to be .
