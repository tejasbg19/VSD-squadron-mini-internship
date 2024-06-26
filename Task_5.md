# Task-5: Functional Simulation Of Processor Using The Given Testbench & Analysing The Thus Obtained Waveform


## The RTL Code:

The RTL code for our hardware which needs to be tested & simulated is taken from [here](https://github.com/vinayrayapati/rv32i/blob/main/iiitb_rv32i.v) 

```
module iiitb_rv32i(clk,RN,NPC,WB_OUT);
input clk;
input RN;
//input EN;
integer k;
wire  EX_MEM_COND ;

reg 
BR_EN;

//I_FETCH STAGE
reg[31:0] 
IF_ID_IR,
IF_ID_NPC;                                

//I_DECODE STAGE
reg[31:0] 
ID_EX_A,
ID_EX_B,
ID_EX_RD,
ID_EX_IMMEDIATE,
ID_EX_IR,ID_EX_NPC;      

//EXECUTION STAGE
reg[31:0] 
EX_MEM_ALUOUT,
EX_MEM_B,EX_MEM_IR;                        

parameter 
ADD=3'd0,
SUB=3'd1,
AND=3'd2,
OR=3'd3,
XOR=3'd4,
SLT=3'd5,

ADDI=3'd0,
SUBI=3'd1,
ANDI=3'd2,
ORI=3'd3,
XORI=3'd4,

LW=3'd0,
SW=3'd1,

BEQ=3'd0,
BNE=3'd1,

SLL=3'd0,
SRL=3'd1;


parameter 
AR_TYPE=7'd0,
M_TYPE=7'd1,
BR_TYPE=7'd2,
SH_TYPE=7'd3;


//MEMORY STAGE
reg[31:0] 
MEM_WB_IR,
MEM_WB_ALUOUT,
MEM_WB_LDM;                      


output reg [31:0]WB_OUT,NPC;

//REG FILE
reg [31:0]REG[0:31];                                               
//64*32 IMEM
reg [31:0]MEM[0:31];                                             
//64*32 DMEM
reg [31:0]DM[0:31];   


//assign EX_MEM_COND = (EX_MEM_IR[6:0]==BR_TYPE) ? 1'b1 : 1'b0;
                     //1'b1 ? (ID_EX_A!=ID_EX_RD) : 1'b0;

always @(posedge clk or posedge RN) begin
    if(RN) begin
    NPC<= 32'd0;
    //EX_MEM_COND <=1'd0;
    BR_EN<= 1'd0; 
    REG[0] <= 32'h00000000;
    REG[1] <= 32'd1;
    REG[2] <= 32'd2;
    REG[3] <= 32'd3;
    REG[4] <= 32'd4;
    REG[5] <= 32'd5;
    REG[6] <= 32'd6;
    end
    //else if(EX_MEM_COND)
    //NPC <= EX_MEM_ALUOUT;

    //else if (EX_MEM_COND)begin
    //NPC = EX_MEM_COND ? EX_MEM_ALUOUT : NPC +32'd1;
    //NPC <= EX_MEM_ALUOUT;
    //EX_MEM_COND = BR_EN;
    //NPC = BR_EN ? EX_MEM_ALUOUT : NPC +32'd1;
    //BR_EN = 1'd0;
    //EX_MEM_COND <= 1'd0;
    //end
    else begin
    NPC <= BR_EN ? EX_MEM_ALUOUT : NPC +32'd1;
    BR_EN <= 1'd0;
    //NPC <= NPC +32'd1;
    //EX_MEM_COND <=1'd0;
    IF_ID_IR <=MEM[NPC];
    IF_ID_NPC <=NPC+32'd1;
    end
end

always @(posedge RN) begin
    //NPC<= 32'd0;
MEM[0] <= 32'h02208300;         // add r6,r1,r2.(i1)
MEM[1] <= 32'h02209380;         //sub r7,r1,r2.(i2)
MEM[2] <= 32'h0230a400;         //and r8,r1,r3.(i3)
MEM[3] <= 32'h02513480;         //or r9,r2,r5.(i4)
MEM[4] <= 32'h0240c500;         //xor r10,r1,r4.(i5)
MEM[5] <= 32'h02415580;         //slt r11,r2,r4.(i6)
MEM[6] <= 32'h00520600;         //addi r12,r4,5.(i7)
MEM[7] <= 32'h00209181;         //sw r3,r1,2.(i8)
MEM[8] <= 32'h00208681;         //lw r13,r1,2.(i9)
MEM[9] <= 32'h00f00002;         //beq r0,r0,15.(i10)
MEM[25] <= 32'h00210700;         //add r14,r2,r2.(i11)
//MEM[27] <= 32'h01409002;         //bne r0,r1,20.(i12)
//MEM[49] <= 32'h00520601;         //addi r12,r4,5.(i13)
//MEM[50] <= 32'h00208783;         //sll r15,r1,r2(2).(i14)
//MEM[51] <= 32'h00271803;         //srl r16,r14,r2(2).(i15) */

//for(k=0;k<=31;k++)
//REG[k]<=k;
/*REG[0] <= 32'h00000000;
REG[1] <= 32'd1;
REG[2] <= 32'd2;
REG[3] <= 32'd3;
REG[4] <= 32'd4;
REG[5] <= 32'd5;
REG[6] <= 32'd6;
REG[7] = 32'd7;
REG[6] = 32'd6;
REG[7] = 32'd7;
REG[8] = 32'd8;
REG[9] = 32'd9;
REG[10] = 32'd10;
REG[11] = 32'd11;
REG[12] = 32'd12;
REG[13] = 32'd13;
REG[14] = 32'd14;
REG[15] = 32'd15;
REG[16] = 32'd16;
REG[17] = 32'd17;*/
/*end
else begin
    if(EX_MEM_COND==1 && EX_MEM_IR[6:0]==BR_TYPE) begin
    NPC=EX_MEM_ALUOUT;
    IF_ID=MEM[NPC];
    end

    else begin
    NPC<=NPC+32'd1;
    IF_ID<=MEM[NPC];
    IF_ID_NPC<=NPC+32'd1;
    end
end*/
end
//I_FECT STAGE

/*always @(posedge clk) begin

//NPC <= rst ? 32'd0 : NPC+32'd1;

if(EX_MEM_COND==1 && EX_MEM_IR[6:0]==BR_TYPE) begin
NPC=EX_MEM_ALUOUT;
IF_ID=MEM[NPC];
end

else begin
NPC<=NPC+32'd1;
IF_ID<=MEM[NPC];
IF_ID_NPC<=NPC+32'd1;
end
end*/


//FETCH STAGE END

//I_DECODE STAGE 
always @(posedge clk) begin

ID_EX_A <= REG[IF_ID_IR[19:15]];
ID_EX_B <= REG[IF_ID_IR[24:20]];
ID_EX_RD <= REG[IF_ID_IR[11:7]];
ID_EX_IR <= IF_ID_IR;
ID_EX_IMMEDIATE <= {{20{IF_ID_IR[31]}},IF_ID_IR[31:20]};
ID_EX_NPC<=IF_ID_NPC;
end
//DECODE STAGE END

/*always@(posedge clk) begin
if(ID_EX_IR[6:0]== BR_TYPE)
EX_MEM_COND <= EN;
else
EX_MEM_COND <= !EN;
end*/


//EXECUTION STAGE

always@(posedge clk) begin

EX_MEM_IR <=  ID_EX_IR;
//EX_MEM_COND <= (ID_EX_IR[6:0] == BR_TYPE) ? 1'd1 :1'd0;


case(ID_EX_IR[6:0])

AR_TYPE:begin
    if(ID_EX_IR[31:25]== 7'd1)begin
    case(ID_EX_IR[14:12])

    ADD:EX_MEM_ALUOUT <= ID_EX_A + ID_EX_B;
    SUB:EX_MEM_ALUOUT <= ID_EX_A - ID_EX_B;
    AND:EX_MEM_ALUOUT <= ID_EX_A & ID_EX_B;
    OR :EX_MEM_ALUOUT <= ID_EX_A | ID_EX_B;
    XOR:EX_MEM_ALUOUT <= ID_EX_A ^ ID_EX_B;
    SLT:EX_MEM_ALUOUT <= (ID_EX_A < ID_EX_B) ? 32'd1 : 32'd0;

    endcase
    end
    else begin
        case(ID_EX_IR[14:12])
        ADDI:EX_MEM_ALUOUT <= ID_EX_A + ID_EX_IMMEDIATE;
        SUBI:EX_MEM_ALUOUT <= ID_EX_A - ID_EX_IMMEDIATE;
        ANDI:EX_MEM_ALUOUT <= ID_EX_A & ID_EX_B;
        ORI:EX_MEM_ALUOUT  <= ID_EX_A | ID_EX_B;
        XORI:EX_MEM_ALUOUT <= ID_EX_A ^ ID_EX_B;
        endcase
    end

end

M_TYPE:begin
    case(ID_EX_IR[14:12])
    LW  :EX_MEM_ALUOUT <= ID_EX_A + ID_EX_IMMEDIATE;
    SW  :EX_MEM_ALUOUT <= ID_EX_IR[24:20] + ID_EX_IR[19:15];
    endcase
end

BR_TYPE:begin
    case(ID_EX_IR[14:12])
    BEQ:begin 
    EX_MEM_ALUOUT <= ID_EX_NPC+ID_EX_IMMEDIATE;
    BR_EN <= 1'd1 ? (ID_EX_IR[19:15] == ID_EX_IR[11:7]) : 1'd0;
    //BR_PC = EX_MEM_COND ? EX_MEM_ALUOUT : 1'd0; 
end
BNE:begin 
    EX_MEM_ALUOUT <= ID_EX_NPC+ID_EX_IMMEDIATE;
    BR_EN <= (ID_EX_IR[19:15] != ID_EX_IR[11:7]) ? 1'd1 : 1'd0;
end
endcase
end

SH_TYPE:begin
case(ID_EX_IR[14:12])
SLL:EX_MEM_ALUOUT <= ID_EX_A << ID_EX_B;
SRL:EX_MEM_ALUOUT <= ID_EX_A >> ID_EX_B;
endcase
end

endcase
end


//EXECUTION STAGE END
		
//MEMORY STAGE
always@(posedge clk) begin

MEM_WB_IR <= EX_MEM_IR;

case(EX_MEM_IR[6:0])

AR_TYPE:MEM_WB_ALUOUT <=  EX_MEM_ALUOUT;
SH_TYPE:MEM_WB_ALUOUT <=  EX_MEM_ALUOUT;

M_TYPE:begin
case(EX_MEM_IR[14:12])
LW:MEM_WB_LDM <= DM[EX_MEM_ALUOUT];
SW:DM[EX_MEM_ALUOUT]<=REG[EX_MEM_IR[11:7]];
endcase
end

endcase
end

// MEMORY STAGE END


//WRITE BACK STAGE
always@(posedge clk) begin

case(MEM_WB_IR[6:0])

AR_TYPE:begin 
WB_OUT<=MEM_WB_ALUOUT;
REG[MEM_WB_IR[11:7]]<=MEM_WB_ALUOUT;
end

SH_TYPE:begin
WB_OUT<=MEM_WB_ALUOUT;
REG[MEM_WB_IR[11:7]]<=MEM_WB_ALUOUT;
end

M_TYPE:begin
case(MEM_WB_IR[14:12])
LW:begin
WB_OUT<=MEM_WB_LDM;
REG[MEM_WB_IR[11:7]]<=MEM_WB_LDM;
end
endcase
end



endcase
end
//WRITE BACK STAGE END

endmodule
```


## The Test Bench 

We will be using the below testbench to verify the functionality of the above `Verilog` code & Verify the execution of instructions we analysed in task-02 is taken from this [repo](https://github.com/vinayrayapati/rv32i/blob/main/iiitb_rv32i_tb.v) :

```
module iiitb_rv32i_tb;

reg clk,RN;
wire [31:0]WB_OUT,NPC;

iiitb_rv32i rv32(clk,RN,NPC,WB_OUT);


always #3 clk=!clk;

initial begin 
RN  = 1'b1;
clk = 1'b1;

$dumpfile("iiitb_rv32i.vcd");
$dumpvars(0, iiitb_rv32i_tb.clk, iiitb_rv32i_tb.RN, iiitb_rv32i_tb.WB_OUT, iiitb_rv32i_tb.NPC,
               iiitb_rv32i_tb.rv32.ID_EX_A, iiitb_rv32i_tb.rv32.ID_EX_B,
               iiitb_rv32i_tb.rv32.ID_EX_IR, iiitb_rv32i_tb.rv32.ID_EX_RD);
  
  
  #5 RN = 1'b0;
  
  #300 $finish;

end
endmodule
```

## Functional Simulation

To verify the functionality, first create new verilog files with the above RTL & testbench codes and save them.

![trial 20  Running  - Oracle VM VirtualBox 5_8_2024 4_12_15 PM](https://github.com/tejasbg19/VSD-squadron-mini-internship/assets/163899793/48486c90-f7c1-47c1-9e35-6225ee28cafc)
saving the RTL code to be verified.


![trial 20  Running  - Oracle VM VirtualBox 5_8_2024 4_13_05 PM](https://github.com/tejasbg19/VSD-squadron-mini-internship/assets/163899793/fe5aadd5-fc95-46f4-b510-ecc829fdc7aa)
Saving the testbench.

<br>
We will be using `iverilog` to compile our RTL & `gtkwave` which we downloaded in task-1to view the waveforms. To simulate the RTL through our testbench & view the waveform, 
follow the below instructions.


```
$ iverilog -o name_for_waveform RTL_code_filename.v Testbench_name.v
$ vvp output name_for_waveform
$ gtkwave iiitb_rv32i.vcd
```

![trial 20  Running  - Oracle VM VirtualBox 5_8_2024 4_14_41 PM](https://github.com/tejasbg19/VSD-squadron-mini-internship/assets/163899793/1b11b8e6-36d8-491c-822a-df311354c134)


## The Waveforms 

It is important to note that the riscv instructions are hardcodded in verilog & are not the same even tough they perform same functions. Also "hardcoded" simply means that the behavior of each instruction is explicitly defined in the Verilog code. <br>
Double click on the signals which needed to be added to the waveform.

![trial 20  Running  - Oracle VM VirtualBox 5_8_2024 11_36_36 PM](https://github.com/tejasbg19/VSD-squadron-mini-internship/assets/163899793/21da9ef5-8cf4-4251-91ab-e56a848d7b31)



#### Instruction_1 

```
add r6,r2,r1
```

![trial 20  Running  - Oracle VM VirtualBox 5_8_2024 11_51_42 PM](https://github.com/tejasbg19/VSD-squadron-mini-internship/assets/163899793/3f37efcb-213a-46c9-816b-eb96bf87b089)



#### Instruction_2 

```
sub r7,r1,r2
```

![trial 20  Running  - Oracle VM VirtualBox 5_9_2024 5_05_17 PM](https://github.com/tejasbg19/VSD-squadron-mini-internship/assets/163899793/103b0848-d233-40d9-ab6d-64d402eadfb1)



#### Instruction_3 

```
and r8,r1,r3
```

![Captures 5_9_2024 5_08_22 PM](https://github.com/tejasbg19/VSD-squadron-mini-internship/assets/163899793/0b59201f-a819-4608-b403-71b4f3eb5d9a)



#### Instruction_4

```
or r9,r2,r5
```

![Photos 5_9_2024 5_09_34 PM](https://github.com/tejasbg19/VSD-squadron-mini-internship/assets/163899793/c606cd3a-b388-46a1-a3ca-0b5df0b83de5)



#### Instruction_5

```
xor r10,r1,r4
```

![trial 20  Running  - Oracle VM VirtualBox 5_9_2024 5_10_43 PM](https://github.com/tejasbg19/VSD-squadron-mini-internship/assets/163899793/f7ff7988-5ef3-43b8-9cde-9836f5f53f0a)



#### Instruction_6

```
slt r11,r2,r4
```

![trial 20  Running  - Oracle VM VirtualBox 5_9_2024 5_15_11 PM](https://github.com/tejasbg19/VSD-squadron-mini-internship/assets/163899793/a69e79ac-02cf-405c-95b2-b511f11f51a4)



#### Instruction_7

```
addi r12,r4,5
```

![trial 20  Running  - Oracle VM VirtualBox 5_9_2024 5_16_30 PM](https://github.com/tejasbg19/VSD-squadron-mini-internship/assets/163899793/118d3932-45d5-4b13-b025-7140a50b5cac)



#### Instruction_8

```
sw r3,r1,2
```

![trial 20  Running  - Oracle VM VirtualBox 5_9_2024 5_18_11 PM](https://github.com/tejasbg19/VSD-squadron-mini-internship/assets/163899793/708b606e-11f6-4ab5-a62f-0c7481ac47fb)


#### Instruction_9

```
lw r13,r1,2
```

![trial 20  Running  - Oracle VM VirtualBox 5_9_2024 5_34_23 PM](https://github.com/tejasbg19/VSD-squadron-mini-internship/assets/163899793/98fc48d4-2e79-4c28-8f10-9021c4b7ea58)


#### Instruction_10

```
beq r0,r0,15 
```

![trial 20  Running  - Oracle VM VirtualBox 5_9_2024 5_37_43 PM](https://github.com/tejasbg19/VSD-squadron-mini-internship/assets/163899793/30549f6d-9053-40d8-a2d6-aa9d5ddbc42e)



#### Instruction_11

```
bne r0,r1,20
```

![trial 20  Running  - Oracle VM VirtualBox 5_9_2024 5_40_23 PM](https://github.com/tejasbg19/VSD-squadron-mini-internship/assets/163899793/ea08bd4e-798b-4c11-80fc-fcfc9543e281)



#### Instruction_12

```
sll r15,r1,r2(2)
```

![trial 20  Running  - Oracle VM VirtualBox 5_9_2024 6_20_54 PM](https://github.com/tejasbg19/VSD-squadron-mini-internship/assets/163899793/16ba7f06-c790-4a20-b254-521be35e5107)

<!--
#### Instruction_13

```
srl r16,r14,r2(2)
```
-->

#### Output Waveform Of All The Instructions

![Photos 5_9_2024 6_24_10 PM](https://github.com/tejasbg19/VSD-squadron-mini-internship/assets/163899793/897bcc34-a3ac-4d23-8348-2a4b42df3f46)
