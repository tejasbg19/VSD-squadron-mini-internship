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




