# Task-3 : Compile A C Program Using Riscv Compiler


## Installing Leafpad Text Editor:


We will be using `leafpad` text editor to write our `c` program. The text editor can be installed as shown below (applicable for ubuntu 22.04 version).


```
$ sudo apt update
$ sudo snap install leafpad 
```
![Screenshot 4_29_2024 7_37_16 PM](https://github.com/tejasbg19/VSD-squadron-mini-internship/assets/163899793/d13190db-f138-4465-8e73-549f18c9f342)




## The Program:

Navigate to the home directory and create a new `.c` file in leafpad as shown below,

```
$ cd 
$ leafpad sum1ton.c &
```

 ![trial2  Running  - Oracle VM VirtualBox 4_30_2024 11_14_50 PM](https://github.com/tejasbg19/VSD-squadron-mini-internship/assets/163899793/9cdac6c2-2a70-4427-9f6d-522f25913734)



write a `c program` and use the `save button`or use `ctrl + s`  to save the file. 

```
#include <stdio.h>
int main(){
    int sum = 0, i, n = 8;
    for (i=1; i<=n; ++i){
        sum += i;
    }
    printf("Sum of numbers from 1 to %d is %d \n", n, sum);
    return 0;
}

```


![trial2  Running  - Oracle VM VirtualBox 4_30_2024 11_19_19 PM](https://github.com/tejasbg19/VSD-squadron-mini-internship/assets/163899793/ead6df7d-478c-4db2-9b46-ef1aeff1930f)



## Compilation & Execution


Compile and run the program as below

```
$ gcc program_name.c 
$ ./a.out 
```

![trial2  Running  - Oracle VM VirtualBox 4_30_2024 11_21_28 PM](https://github.com/tejasbg19/VSD-squadron-mini-internship/assets/163899793/8492837b-54db-4aa8-bda1-40c0702bafa3)



To compile the program in riscv gcc compiler follow the below instruction.

```
$ riscv64-unknown-elf-gcc -O1 -mabi=lp64 -march=rv64i -o program_name.o program_name.c
```

![trial2  Running  - Oracle VM VirtualBox 4_30_2024 11_55_18 PM](https://github.com/tejasbg19/VSD-squadron-mini-internship/assets/163899793/948daa3a-738f-4b79-a395-648ebd3e87c9)


Now open a new tab in terminal using `ctrl + shift + T` and follow below instruction to open the assembly code for the c program we had executed earlier.

```
$ riscv64-unknown-elf-objdump -d program_name.o
```
![Photos 5_1_2024 12_01_28 AM](https://github.com/tejasbg19/VSD-squadron-mini-internship/assets/163899793/f594b5ce-505b-435a-9968-07e09a666e8d)

![trial2  Running  - Oracle VM VirtualBox 5_1_2024 12_06_22 AM](https://github.com/tejasbg19/VSD-squadron-mini-internship/assets/163899793/b572341c-d106-423c-9505-5aa117a29910)

to search for `main()` section of our program below the below step,

```
$ riscv64-unknown-elf-objdump -d program_name.o | less
: /main
```

press `n` key to scrolldown & press `q` to quit.


![trial2  Running  - Oracle VM VirtualBox 5_1_2024 12_06_56 AM](https://github.com/tejasbg19/VSD-squadron-mini-internship/assets/163899793/7af02f39-f5b1-432a-a320-12d8300a1a54)

![trial2  Running  - Oracle VM VirtualBox 5_1_2024 12_17_48 AM](https://github.com/tejasbg19/VSD-squadron-mini-internship/assets/163899793/0aeba1b1-2e4d-4983-8d48-d79dc7ea9e56)

![trial2  Running  - Oracle VM VirtualBox 5_1_2024 12_18_11 AM](https://github.com/tejasbg19/VSD-squadron-mini-internship/assets/163899793/bd295160-43b0-4628-9c2a-db43a4f608ab)

The above image shows the `main()` section of my program. And as we can see there are 11 instructions in the `main()`. Address of each instruction can be seen. The address of the next instruction is `current address + 4 bytes`. <br>
<br> 
**Total Number of Instructions = (Address of the first instruction of the next instruction block -  Address of the first instruction of the current instruction block) / 4**
<br>
<br>
Therefore, Total number of instructions in main() =  (101b0 - 10184)/4 = (B/4)<sub>**16**</sub> = (**11**)<sub>**10**</sub>


## Role of -O1: 

**-O** is a flag which directs the compiler to what extent it needs to optimize a given program, the optimization may be in terms of reducing binary size of the program while compramizing of the speed of execution or optimize the speed of exceution while increasing the binary program size. There are various levels of optimization,
<br>
**-O0** : This flag disables most optimizations and thus generated assembly code will be most human readable hence easy to debug. <br>
**-O1** : This flag offers basic optimization, balances binary code size as well as speed. <br>
**-Ofast** : This flag offers aggressive optimizations. It prioritizes speed of execution over the size of compiled binary program size. <br>
**-Os** : This flag sacrifices execution speed to reduce binary size. <br>
<br>

Let us compile the same program with **-Ofast** flag.


```
$ riscv64-unknown-elf-gcc -Ofast -mabi=lp64 -march=rv64i -o program_name.o program_name.c
# In a new terminal tab
$ riscv64-unknown-elf-objdump -d program_name.o | less
: /main
```

![Editing VSD-squadron-mini-internship_Task_3 md at main · tejasbg19_VSD-squadron-mini-internship and 14 more pages - Personal - Microsoft​ Edge 5_1_2024 1_05_44 AM](https://github.com/tejasbg19/VSD-squadron-mini-internship/assets/163899793/9bb811d6-1838-48a7-8f21-1e5eb8cf17df)

![trial2  Running  - Oracle VM VirtualBox 5_1_2024 1_08_11 AM](https://github.com/tejasbg19/VSD-squadron-mini-internship/assets/163899793/c5909fa6-ee99-49f5-8623-813fa72fb6f1)




**Number of Instructions =** (Address of the first instruction of the next instruction block -  Address of the first instruction of the current instruction block) / 4 

Therefore, Number of Instructions = (100dc - 100b0)\4 = (2C/4)<sub>**16**</sub> = (11)<sub>**10**</sub>
<br>

Even tough the number of instructions remain the same, the size of the program has reduced, which we can observe by the byte adress of the main(), earlier it began with 101XX but now it is beginning with 100XX.




