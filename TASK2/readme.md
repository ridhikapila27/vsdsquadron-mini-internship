# RISC-V INSTRUCTION TYPES
## R TYPE
RISC-V R-type instructions are a category of instructions used for arithmetic and logic operations where the operation involves only registers. These instructions typically have the following format:

```
  31       25 24      20 19      15 14      12 11      7 6        0
+------------+--------+--------+--------+--------+--------+--------+
|   funct7   |   rs2  |   rs1  |  funct3|    rd  | opcode |   R    |
+------------+--------+--------+--------+--------+--------+--------+
```

- **`funct7` (7 bits):** This field provides additional function bits for certain instructions, allowing for extended functionalities or distinguishing between different variants of an operation.
  
- **`rs2` (5 bits):** This field contains the register number of the second operand/source register.
  
- **`rs1` (5 bits):** This field contains the register number of the first operand/source register.
  
- **`funct3` (3 bits):** This field further specifies the operation to be performed, providing finer granularity within the instruction set.
  
- **`rd` (5 bits):** This field contains the register number of the destination register where the result will be stored.

- **`opcode` (7 bits):** This field specifies the overarching category of the instruction, indicating the type of operation to be performed (e.g., arithmetic, logical, etc.).

These instructions are called "R-type" because they only involve registers (hence "R") for both source operands and the result. Examples of R-type instructions include `add`, `sub`, `and`, `or`, `xor`, `sll`, `slt`, `sra`, `srl`, and others.

# I TYPE:
RISC-V I-type instructions are a category of instructions used for operations that involve an immediate value (i.e., a constant) and a register. These instructions typically have the following format:

```
  31       25 24      20 19      15 14      12 11      7 6        0
+------------+--------+--------+--------+--------+--------+--------+
|  imm[11:0] |   rs1  |  funct3|    rd  | opcode |   I    |  imm[11:0]
+------------+--------+--------+--------+--------+--------+--------+
```

- **`imm[11:0]` (12 bits):** This field contains an immediate value (constant) that is part of the instruction. It can represent values from -2048 to 2047, inclusive.
  
- **`rs1` (5 bits):** This field contains the register number of the source register.
  
- **`funct3` (3 bits):** This field further specifies the operation to be performed, providing finer granularity within the instruction set.
  
- **`rd` (5 bits):** This field contains the register number of the destination register where the result will be stored.
  
- **`opcode` (7 bits):** This field specifies the overarching category of the instruction, indicating the type of operation to be performed (e.g., arithmetic, logical, etc.).

- **`I` (1 bit):** This bit indicates that it's an I-type instruction.

These instructions are called "I-type" because they involve an immediate value and a register. Examples of I-type instructions include loads (`lw`, `lh`, `lb`, `lhu`, `lbu`), stores (`sw`, `sh`, `sb`), arithmetic operations with immediates (`addi`, `slti`, `andi`, etc.), and control transfer instructions (`jalr`).

# S TYPE:
RISC-V S-type instructions are a category of instructions used for storing data from a register to memory. These instructions typically have the following format:

```
  31       25 24      20 19      15 14      12 11      7 6        0
+------------+--------+--------+--------+--------+--------+--------+
| imm[11:5] |   rs2  |   rs1  |  funct3| imm[4:0]|  opcode|    S    |
+------------+--------+--------+--------+--------+--------+--------+
```

- **`imm[11:5]` (7 bits):** This field contains the offset immediate value (constant) that is added to the base address stored in `rs1` to calculate the memory address where the data will be stored.

- **`rs2` (5 bits):** This field contains the register number of the source register whose value will be stored in memory.

- **`rs1` (5 bits):** This field contains the register number of the base address register.

- **`funct3` (3 bits):** This field specifies the type of store operation to be performed (e.g., byte, halfword, word).

- **`opcode` (7 bits):** This field specifies the overarching category of the instruction, indicating the type of operation to be performed (e.g., store).

- **`S` (1 bit):** This bit indicates that it's an S-type instruction.

S-type instructions are used for storing data from a register (`rs2`) into memory using an offset immediate value (`imm[11:5]`) added to the base address stored in register `rs1`. The size of the stored data (byte, halfword, word) is determined by the `funct3` field. Examples of S-type instructions include `sb`, `sh`, and `sw`, which respectively store a byte, halfword, or word from `rs2` to memory at the address calculated from the sum of the base address in `rs1` and the offset immediate value.

# B TYPE:
RISC-V B-type instructions are a category of instructions used for conditional branch operations. These instructions typically have the following format:

```
  31       25 24      20 19      15 14      12 11      7 6        0
+------------+--------+--------+--------+--------+--------+--------+
| imm[12]    | imm[10:5]|   rs2  |   rs1  |  funct3| imm[4:1]| imm[11] |
+------------+--------+--------+--------+--------+--------+--------+
```

- **`imm[12]` (1 bit):** This bit represents the most significant bit of the immediate offset, which is used for sign extension to allow for branching both forwards and backwards.

- **`imm[10:5]` (6 bits):** This field contains the offset immediate value (constant) that is added to the program counter (PC) to calculate the branch target address.

- **`rs2` (5 bits):** This field contains the register number of the second operand/source register.

- **`rs1` (5 bits):** This field contains the register number of the first operand/source register.

- **`funct3` (3 bits):** This field specifies the type of branch operation to be performed (e.g., equal, not equal, less than).

- **`imm[4:1]` (4 bits):** This field contains bits 4 to 1 of the immediate offset value.

- **`imm[11]` (1 bit):** This bit represents the least significant bit of the immediate offset value.

B-type instructions are used for conditional branches based on the comparison of two register values (`rs1` and `rs2`). The branch target address is calculated by adding the immediate offset value to the PC. The specific branch condition (e.g., equal, not equal, less than) is determined by the `funct3` field. Examples of B-type instructions include `beq` (branch if equal), `bne` (branch if not equal), `blt` (branch if less than), and `bge` (branch if greater than or equal).

# U TYPE:
RISC-V U-type instructions are a category of instructions used for unconditional jumps and setting upper immediate values. These instructions typically have the following format:

```
  31       25 24      20 19      15 14      12 11      7 6        0
+------------+-------------------------+--------+--------+--------+
| imm[31:12] |           rd            |  opcode|    U    | imm[31:12]|
+------------+-------------------------+--------+--------+--------+
```

- **`imm[31:12]` (20 bits):** This field contains the immediate value (constant) that is used for setting upper bits of a 32-bit value, or as the jump target address in the case of unconditional jumps.

- **`rd` (5 bits):** This field contains the register number of the destination register where the result will be stored, if applicable.

- **`opcode` (7 bits):** This field specifies the overarching category of the instruction, indicating the type of operation to be performed (e.g., jump, setting upper immediate value).

- **`U` (1 bit):** This bit indicates that it's a U-type instruction.

U-type instructions are used for operations such as unconditional jumps (`jal`) and setting upper immediate values (`lui`). The immediate value (`imm[31:12]`) is typically used for specifying the upper bits of a 32-bit value (in the case of `lui`), or as the jump target address (in the case of `jal`).

 # J TYPE:
 RISC-V J-type instructions are a category of instructions used for unconditional jumps. These instructions typically have the following format:

```
  31       25 24      20 19      15 14      12 11      7 6        0
+------------+-------------------------+--------+--------+--------+
| imm[20]    | imm[10:1] | imm[11]  | imm[19:12] |  rd    | opcode |   J    |
+------------+-------------------------+--------+--------+--------+
```

- **`imm[20]` (1 bit):** This bit represents the most significant bit of the immediate offset, which is used for sign extension to allow for jumping both forwards and backwards.

- **`imm[10:1]` (10 bits):** This field contains bits 10 to 1 of the immediate offset value, which represents the jump target address.

- **`imm[11]` (1 bit):** This bit represents bit 11 of the immediate offset value.

- **`imm[19:12]` (8 bits):** This field contains bits 19 to 12 of the immediate offset value.

- **`rd` (5 bits):** This field contains the register number of the destination register where the return address will be stored.

- **`opcode` (7 bits):** This field specifies the overarching category of the instruction, indicating the type of operation to be performed (e.g., jump).

- **`J` (1 bit):** This bit indicates that it's a J-type instruction.

J-type instructions are used for unconditional jumps, with the jump target address being calculated by combining bits from the instruction itself and the program counter (PC). The immediate offset value is calculated by concatenating bits from different parts of the instruction, followed by sign extension to form a 21-bit signed offset. Examples of J-type instructions include `jal` (jump and link), which jumps to a specified target address and stores the return address in a register.


## IDENTIFICATION OF INSTRUCTION TYPE AND ITS CORRESPONDING BIT PATTERN
1. add r6, r2, r1
   Type: R
   
  31       25 24     20 19    15 14   12 11     7 6       0
+------------+--------+--------+--------+--------+--------+
|  0000000   |  00010 |  00001 |   000  | 00110  | 0110011 | 
+------------+--------+--------+--------+--------+--------+
