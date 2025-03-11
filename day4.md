# Simple RISCV Micro-architecture

A simple RISC-V microarchitecture follows a 5-stage pipeline, using registers, ALU, memory, and control logic. It optimizes execution through pipelining, forwarding, and branch prediction to improve performance.

A simple RISC-V microarchitecture consists of the essential components needed to execute RISC-V instructions efficiently. It follows the RISC (Reduced Instruction Set Computing) principle, meaning that instructions are simple and execute in a few cycles.


### 1. Key Components of RISC-V Microarchitecture
A basic 5-stage RISC-V processor pipeline includes:

#### Instruction Fetch (IF)

Fetches the instruction from memory.
Uses the Program Counter (PC) to track the next instruction.
#### Instruction Decode (ID)

Decodes the instruction to determine the opcode, source registers, and destination register.
Reads values from the Register File.
### Execute (EX)

Performs arithmetic and logic operations using the ALU (Arithmetic Logic Unit).
Calculates memory addresses for load/store instructions.
### Memory Access (MEM)

Accesses data memory for load and store instructions.
### Write Back (WB)

Writes results back to the register file.

### Designing program counter 
The Program Counter (PC) in a RISC-V microarchitecture is a register that holds the address of the next instruction to be executed. In a typical execution cycle, the PC increments by 4 (since RISC-V uses fixed 32-bit instructions) to fetch the next instruction from memory


