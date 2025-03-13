## Pipelining in RISC-V CPU
Pipelining allows multiple instructions to be processed simultaneously, divided into stages:
- Instruction Fetch (IF) – Fetch instruction from memory.
- Instruction Decode (ID) – Decode instruction, read registers.
- Execute (EX) – ALU computation or address calculation.
- Memory Access (MEM) – Load/store operations.
- Write-Back (WB) – Write results back to registers.

  **images**
### Pipeline Performance
Ideally, an N-stage pipeline achieves an N times speedup, but hazards reduce efficiency.
Techniques like hazard detection units, branch prediction, and forwarding optimize pipelining
| Cycle | IF | ID | EX | MEM| WB |
|--------|---|----|----|----|----|
| 1 | I1 | | | |
| 2 | I2 | I1 |  | | |
| 3 | I3 | I2 | I1 | | |
| 4 | I4 | I3 | I2 | I1 | |
| 5 | I5 | I4 | I3 |I2 | I1 |
- Each instruction moves through different stages simultaneously.
- Hazards (Control, RAW) can cause stalls or slow execution.

## Introduction to Control Flow Hazards and Read-After-Write (RAW) Hazards in RISC-V CPU Pipelining
Modern RISC-V processors use pipelining to enhance performance by overlapping instruction execution. However, pipelining introduces hazards, which are situations where the next instruction cannot execute correctly due to dependencies or changes in the control flow.

## 1. Control Flow Hazards (Branch Hazards)
Control flow hazards occur when the CPU encounters a branch (conditional/unconditional jump), making it uncertain which instruction to fetch next.
Example: BEQ (Branch if Equal), JAL (Jump and Link)
- If a branch is taken, the PC needs to change to the branch target address.
- If the branch is not taken, the next sequential instruction should execute.
- The problem: The processor may fetch the wrong instruction before resolving the branch.
- This leads to pipeline stalls or incorrect execution.
## 2. Read-After-Write (RAW) Hazard (Data Hazard)
A RAW hazard occurs when an instruction needs data from a register before the previous instruction writes it.
Example :
```asm
ADD x5, x1, x2  # x5 = x1 + x2
SUB x3, x5, x4  # x3 = x5 - x4  (x5 not updated yet!)
```
- The second instruction depends on x5, but the first instruction hasn't written the result yet.
- This causes incorrect data usage and pipeline stalls.

## Register File Address-to-Address Read After Write (RAW) Hazard
- A Read After Write (RAW) hazard occurs when an instruction depends on the result of a previous instruction that has not yet been written back to the register file.
- This can cause incorrect data being read by subsequent instructions.
- A common solution to this problem is data forwarding (bypassing), where the result from an earlier instruction is directly forwarded to dependent instructions without waiting for it to be written to the register file.
- Another solution is stalling, where the pipeline delays execution until the required data is available.

## Handling Branches to Get the Branch Target Path
- Branch instructions (e.g., BEQ, BNE, JAL, etc.) introduce control hazards, as the correct instruction path depends on the branch outcome.
- The processor must decide whether to fetch the next sequential instruction or jump to a new address.

## Load and Store Instructions in RISC-V CPU
RISC-V follows a Load-Store Architecture, meaning all data manipulations occur in registers, and memory access is performed explicitly using load and store instructions. This helps keep the instruction set simple and efficient for pipelining.

### 1. Load Instructions (Reading from Memory to Registers)
Load instructions transfer data from memory to a register. The format for a load instruction is:
```asm
LW x1, offset(x2)
```
Here, x1 is the destination register, x2 is the base address register, and offset is a 12-bit immediate value added to x2 to compute the memory address.

#### Common Load Instructions:
|Instruction|	Meaning	|Description|
|-----------|---------|-----------|
|LB|	Load Byte|	Loads a signed byte (8-bit) from memory to a register|
|LBU |	Load Byte Unsigned|	Loads an unsigned byte from memory.|
|LH|	Load Halfword|	Loads a signed halfword (16-bit).|
|LHU|	Load Halfword Unsigned|	Loads an unsigned halfword.|
|LW|	Load Word|	Loads a 32-bit word from memory.|
Example:
```asm
LW x10, 8(x5)   # Load 32-bit data from memory address (x5 + 8) into register x10
```
### 2. Store Instructions (Writing from Registers to Memory)
Store instructions transfer data from a register to memory. The format for a store instruction is:
```asm
SW x1, offset(x2)
```
Here, x1 is the source register whose data will be stored, x2 is the base address register, and offset is an immediate value.

#### Common Store Instructions:
|Instruction|	Meaning	|Description|
|-----------|---------|-----------|
|SB|	Store Byte	|Stores a byte (8-bit) from a register to memory.|
|SH|	Store Halfword|	Stores a halfword (16-bit) from a register.|
|SW|	Store Word|	Stores a word (32-bit) from a register to memory.|
Example:
```asm
SW x10, 8(x5)   # Store 32-bit data from register x10 to memory address (x5 + 8)
```

###  Load and Store in a Pipeline CPU
**Load-Use Hazard:** If an instruction tries to use a register immediately after a load, the pipeline may need to stall.
**Forwarding (Bypassing):** In some cases, forwarding techniques can be used to avoid stalls.
**Memory Dependencies:** Loads and stores must be correctly ordered to avoid data inconsistency.


