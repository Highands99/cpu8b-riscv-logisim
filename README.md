# cpu8b-riscv-logisim
Risc-v based cpu's logic circuit realized with logisim 2.7.1.

## Genera information
- There are 4 register + pc.
- x0 register is set permanently to 0.
- Instruction memory is set to 16 bit width instead of 8 bit, if you want use 8 bit width, remember to increment pc with +2 instead of +1 as it is now and implementing a shift left for a more accurat simulation. 

## Instruction encoding
16 bit per instruction
### Operation code, funct3, funct7
Format  : instruction : Opcode : funct3 : funct7 : ALU Action : ALUctrl
-----------------------------------------------------------------------
I-type  : lb          : 00     : xx     : xx     : add        : 10

SB-type : beq         : 01     : xx     : xx     : sub        : 11

R-type  : add         : 10     : 00     : 00     : add        : 10
R-type  : sub         : 10     : 00     : 01     : sub        : 11
R-type  : and         : 10     : 11     : 00     : and        : 00
R-type  : or          : 10     : 10     : 00     : or         : 01

S-type  : lb          : 11     : xx     : xx     : add        : 10

### Instruction format
I-type:
imm[7:0] | rs1 | funct3 | rd | op
8b       | 2b  | 2b     | 2b | 2b

S-type:
imm[7:2] | rs2 | rs1 | funct3 | imm[1:0] | op
6b       | 2b  | 2b  | 2b     | 2b       | 2b

SB-type:
imm[0,7,5:2] | rs2 | rs1 | funct3 | imm[1:6] | op
6b           | 2b  | 2b  | 2b     | 2b       | 2b

R-type:
XXX      | funct7 | rs1 | rs2 |funct3 | rd | op
4b       | 2b     | 2b  | 2b  | 2b    | 2b | 2b
