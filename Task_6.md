# Task-5: Verifying The Functionality of VSD Mini Squadron Board By Implementing a Centade (0-99) BCD Counter


## BCD 

**BCD** stands for ***Binary-Coded Decimal***. A BCD counter is a type of counter used in digital electronics and computing to represent decimal numbers using binary-coded decimal format. In BCD format, each decimal digit (0-9) is represented by a 4-bit binary code. 

<br>
Example:

- Decimal `0` is represented as **`0000`** in BCD.
- Decimal `4` is represented as **`0100`** in BCD.
- Decimal `15` is represented as **`0001 0101`** in BCD.

## The Counter

### Overview 

Counters are fundamental components in digital electronics that are used to count, sequence, or track events. They play a crucial role in various electronic systems and have several applications across different fields including Frequency measurement & division, Event counting and monitoring etc,. I have created a BCD counter that counts from 0 to 99. When a push button (which act as clock) is pressed, the counter increments by one.


### Components Required

- VSD Mini Squadron Board
- 8 LEDs ( 4 Blue & 4 Red )
- Eight 220 ohm Resistors 
- Push button switch
- Jumper cables
- Bread board
- USB type-C or a 3.3V DC power source


### Hardware Connections

![bboard](https://github.com/tejasbg19/VSD-squadron-mini-internship/assets/163899793/f71ed023-2e25-4544-b357-91ea77e5aa35)


As we can see from the above image, 

- A push button which act as `trigger` is connected between **`GND`** & **`PD1`**.
- All the 8 LEDs have a common **`GND`** & each of their Anode is connected to a 220 ohms resistors.
- Ports `PC0` to `PC3` forms the `unit` digit & are connected to their respective LEDs with `PC0` being **LSB (Least Significant Bit)** & `PC3` being **MSB (Most Significant Bit)**
