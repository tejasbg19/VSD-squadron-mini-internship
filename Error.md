# Error while debugging instructions of `main()`


This is the instructions under `main()` in my `.o` file.
![trial 20  Running  - Oracle VM VirtualBox 5_5_2024 12_18_25 AM](https://github.com/tejasbg19/VSD-squadron-mini-internship/assets/163899793/cfc6b8fc-3ab8-4d94-bd7c-49a7b19df2e9)

<br>

Even `spike` executes each instruction perfectly fine until `jal`,
![trial 20  Running  - Oracle VM VirtualBox 5_5_2024 12_19_04 AM](https://github.com/tejasbg19/VSD-squadron-mini-internship/assets/163899793/687ca384-f9df-468c-9873-c64869fe30ec)

<br>

As per `jal pc + 0x3b8` instruction even the program will be transferred to address `104ca` which is the address for `print` function and the instructions of `print()` are shown below
![trial 20  Running  - Oracle VM VirtualBox 5_5_2024 12_19_39 AM](https://github.com/tejasbg19/VSD-squadron-mini-internship/assets/163899793/a454720a-4000-44e7-beb8-53aba025e572)

<br>

# The Error

All the instructions till `jal` under `print()` are executed in spike, but when the program has to transfer control to the address specified in `jal` ( pc + d6a = 11256)<sub>HEX</sub>, I get the below error.
![trial 20  Running  - Oracle VM VirtualBox 5_5_2024 12_20_24 AM](https://github.com/tejasbg19/VSD-squadron-mini-internship/assets/163899793/a651cdee-584e-4b44-9b41-3a7791e03128)
<br>




The control was supposed to be transfered to <_vfprintf_r> function as per `.o` file
![trial 20  Running  - Oracle VM VirtualBox 5_5_2024 12_20_56 AM](https://github.com/tejasbg19/VSD-squadron-mini-internship/assets/163899793/635fed85-7204-4c56-bd01-9a327fe7b822)



Also I verified the <_vfprintf_r> function, it exixts at the same address specified in `jal`
![trial 20  Running  - Oracle VM VirtualBox 5_5_2024 12_21_33 AM](https://github.com/tejasbg19/VSD-squadron-mini-internship/assets/163899793/3f4e006f-3364-4735-90a8-2203627aa7cb)




If I continue to press `enter` random instructions are executed. 

![trial 20  Running  - Oracle VM VirtualBox 5_5_2024 12_22_02 AM](https://github.com/tejasbg19/VSD-squadron-mini-internship/assets/163899793/3aead82f-cb97-488c-8572-75fa4c87787f)

